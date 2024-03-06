---
title: 2024 winter Week 1
---

# Goals
**Weekly:**
- [ ] try to get Titus' script to run on my own
 
**Quarterly:**
- [ ] Present my work to the lab, presentation on March 18th
- [ ] write some snakemake files
- [ ] have an organized notebook

**Yearly:**
- [ ] have a general understand of what a bioinformatic project is like
- [ ] build experience, present analysis, annotate like scientist
- [ ] Have a well documented project in github that is functional 
 
# Results
-I cleaned up some old files and now have more storage space available for new project
- Create new directory named “pangenomeproject”
- Tmux session for more secure connection: tmux new -s pan
- Work session: srun -p bmm -J runscript -t 5:00:00 --mem=10G --pty bash
- Inside the wrok session, installed sourmash: pip install sourmash
- nano make_pangenome_sketches.py
- annotated the script, to learn and understand what the codes do
      -  Argument is required if they are listed as required=True, or have a default value
      -  for n, ss in enumerate(db.signatures()):
         N is lndex(the position of variable on the list) and ss is the variables
      -  revtax_d = {}
         dictionary, value with key pair
      -  Manifests are catalogs of signature metadata - name, molecule type, k-mer size, and other information


annotated script, in case I lost the script in the directory again T^T : 
```
 GNU nano 6.2                          make-pangenome-sketches.py *                                 
#shebang sequence to tell the computer to execute the script with python in user's environment
#! /usr/bin/env python
import argparse #moduele to build comnand argument
import sys #module for python variable

from collections import defaultdict #default dictionary,default variable for value and key pair
import sourmash #to minhash and compute sketches
from sourmash import sourmash_args #to build sourmash command argument
from sourmash.tax import tax_utils #module to run taxonomy related data 


def main():
    p = argparse.ArgumentParser()
    p.add_argument(
        #argument name in diffrent formate, argument will be show in file
        '-t', '--taxonomy-file', '--taxonomy', metavar='FILE',
        #allow more than one argument, more than one variable, required to have a variable 
        action="extend", nargs='+', required=True,
        help='database lineages file'
    )
    p.add_argument(
        'sketches', nargs='+',
        help='sketches to combine'
    )
    p.add_argument('--scaled', default=1000, type=int)
    p.add_argument('-k', '--ksize', default=31, type=int)
    p.add_argument('-o', '--output', required=True)
    p.add_argument('-r', '--rank', default='species')
    args = p.parse_args()

    print(f"loading taxonomies from {args.taxonomy_file}")
    taxdb = sourmash.tax.tax_utils.MultiLineageDB.load(args.taxonomy_file)
    print(f"found {len(taxdb)} identifiers in taxdb.")

    #dictionary, value and their paired key values
    revtax_d = {}
    ident_d = {}

        for filename in args.sketches:
        print(f"loading file {filename} as index => manifest")
        db = sourmash_args.load_file_as_index(filename) #convert the sketch file to index file
        db = db.select(ksize=args.ksize) #select ksize, the smallest ksize?
        mf = db.manifest #Manifests are catalogs of signature metadata in sousrmash name,molecule ty>
        assert mf, "no matching sketches for given ksize!?"

        # load and merge
        for n, ss in enumerate(db.signatures()): # n is index(position of variable in list), ss is n>
            if n and n % 1000 == 0: #message print every 1000 loop
                print(f'...{n} - loading')
            name = ss.name #take sourmash signature variable as a variable  
            md5sum = ss.md5sum()  

            ident = tax_utils.get_ident(name)

            # grab relevant lineage name
            lineage_tup = taxdb[ident]
            lineage_tup = tax_utils.RankLineageInfo(lineage=lineage_tup)
            lineage_pair = lineage_tup.lineage_at_rank(args.rank)
            lineage_name = lineage_pair[-1].name

            # pick an ident to represent this set of pangenome sketches
            ident_d[lineage_name] = ident # ok if overwrite...

            # track merged sketches
            mh = revtax_d.get(lineage_name)
            if mh is None:
                mh = ss.minhash.to_mutable()
                revtax_d[lineage_name] = mh
            else: #merge to collect sketches related for same lineage or taxa
                mh += ss.minhash


    # save!
    with sourmash_args.SaveSignaturesToLocation(args.output) as save_sigs:
        for n, (lineage_name, ident) in enumerate(ident_d.items()):
            if n and n % 1000 == 0:
                print(f'...{n} - saving')
            sig_name = f'{ident} {lineage_name}'

            # retrieve merged MinHash
            mh = revtax_d[lineage_name]

            # make a signature
            ss = sourmash.SourmashSignature(mh, name=sig_name)

            # save!
            save_sigs.add(ss)


if __name__ == '__main__':
    sys.exit(main())
```
```
#shebang sequence to tell the computer to execute the script with python in user's environment
#! /usr/bin/env python
import argparse  # module to build command argument
import sys  # module for python variable

from collections import defaultdict  # default dictionary, default variable for value and key pair
import sourmash  # to minhash and compute sketches
from sourmash import sourmash_args  # to build sourmash command argument
from sourmash.tax import tax_utils  # module to run taxonomy related data 

def main():
    # Create an argument parser to handle command-line arguments
    p = argparse.ArgumentParser()
    
    # Add arguments to the parser
    p.add_argument(
        '-t', '--taxonomy-file', '--taxonomy', metavar='FILE',
        action="extend", nargs='+', required=True,
        help='database lineages file'
    )
    p.add_argument(
        'sketches', nargs='+',
        help='sketches to combine'
    )
    p.add_argument('--scaled', default=1000, type=int)
    p.add_argument('-k', '--ksize', default=31, type=int)
    p.add_argument('-o', '--output', required=True)
    p.add_argument('-r', '--rank', default='species')
    
    # Parse the command-line arguments
    args = p.parse_args()

    # Load taxonomies from the specified file(s)
    print(f"loading taxonomies from {args.taxonomy_file}")
    taxdb = sourmash.tax.tax_utils.MultiLineageDB.load(args.taxonomy_file)
    print(f"found {len(taxdb)} identifiers in taxdb.")

    # Create dictionaries to store data
    revtax_d = {}  # dictionary to store reverse taxonomy information
    ident_d = {}  # dictionary to store identifiers

    # Process each sketch file
    for filename in args.sketches:
        print(f"loading file {filename} as index => manifest")
        db = sourmash_args.load_file_as_index(filename)  # convert the sketch file to index file
        db = db.select(ksize=args.ksize)  # select ksize, the smallest ksize?
        mf = db.manifest  # Manifests are catalogs of signature metadata in sourmash
        assert mf, "no matching sketches for given ksize!?"

        # Load and merge sketches
        for n, ss in enumerate(db.signatures()):  # n is index, ss is signature
            if n and n % 1000 == 0:  # message print every 1000 loop
                print(f'...{n} - loading')
            name = ss.name  # take sourmash signature variable as a variable  
            md5sum = ss.md5sum()  

            ident = tax_utils.get_ident(name)

            # Grab relevant lineage name
            lineage_tup = taxdb[ident]
            lineage_tup = tax_utils.RankLineageInfo(lineage=lineage_tup)
            lineage_pair = lineage_tup.lineage_at_rank(args.rank)
            lineage_name = lineage_pair[-1].name

            # Pick an ident to represent this set of pangenome sketches
            ident_d[lineage_name] = ident  # ok if overwrite...

            # Track merged sketches
            mh = revtax_d.get(lineage_name)
            if mh is None:
                mh = ss.minhash.to_mutable()
                revtax_d[lineage_name] = mh
            else:  # merge to collect sketches related for same lineage or taxa
                mh += ss.minhash

    # Save the merged sketches
    with sourmash_args.SaveSignaturesToLocation(args.output) as save_sigs:
        for n, (lineage_name, ident) in enumerate(ident_d.items()):
            if n and n % 1000 == 0:
```
# Discussion
-tried running the script,umm error
```
yc22@farm:~/pangenomeproject$ ./make-pangenome-sketches.py
./make-pangenome-sketches.py: line 3: import: command not found
./make-pangenome-sketches.py: line 4: import: command not found
./make-pangenome-sketches.py: line 6: from: command not found
./make-pangenome-sketches.py: line 7: import: command not found
./make-pangenome-sketches.py: line 8: from: command not found
./make-pangenome-sketches.py: line 9: from: command not found
./make-pangenome-sketches.py: line 12: syntax error near unexpected token `('
./make-pangenome-sketches.py: line 12: `def main():'
```
-I edit my annotation making sure that the shebang line is the first line
```
yc22@farm:~/pangenomeproject$ ./make-pangenome-sketches.py
/usr/bin/env: ‘python’: No such file or directory
```

probably because I did not import the needed modules
"import argparse
import sys

from collections import defaultdict
import sourmash
from sourmash import sourmash_args
from sourmash.tax import tax_utils"

 
# Journal
2 quizes and 2 midterms on this coming friday. Considering dropping organic chemistry this quarter, but the class will not be offered till next school year. Pretty hard to decide, will see how the friday midterm go, then decide. I prefer not dropping because it is a prereequirement for a class, that is a prerequirement for many upper div class.
