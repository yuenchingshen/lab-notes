---
title: 2024 winter Week 6
---

# Goals
**Weekly:**
- [x]  Create a lab notebook repo
- [x]  Move the previous notebook to the website and change the fomate to new notebook style
- [ ]  follow steps provided on simple-use-case.md
- [ ]  start planning on visualize data for the presentation
 
**Quarterly:**
- [ ] Present my work to the lab, presentation on March 18th
- [ ] Have an organized notebook
- [ ] Write some snakemake files 

**Yearly:**
- [ ] have a general understand of what a bioinformatic project is like
- [ ] build experience, present analysis, annotate like scientist
- [ ] Have a well documented project in github that is functional
      
# Results
```
(sourmash) yc22@farm:~$ ./make-pangenome-sketches.py gtdb-rs214-k21.zip -t gtdb-rs214.lineages.sqldb -o gtdb-rs214-k21.pangenomes.genus.zip -k 21 -r genus
-bash: ./make-pangenome-sketches.py: No such file or directory
(sourmash) yc22@farm:~$ ls
2022-database-covers	    gtdb-rs214.lineages.csv    pangenomeproject
Miniforge3-Linux-x86_64.sh  gtdb-rs214.lineages.sqldb  sourmash
gtdb-rs214-k21.zip	    miniforge3		       spacegraphcats 
```
I was able to make small adjustment to the code if my files are not excatly matching the guide provided. Although these are very basic level skills, I am still glad that I am able to do it. Cause I would not be able to do it last quarter.

```
(sourmash) yc22@farm:~$ ./pangenomeproject/make-pangenome-sketches.py gtdb-rs214-k21.zip -t gtdb-rs214.lineages.sqldb -o gtdb-rs214-k21.pangenomes.genus.zip -k 21 -r genus 
loading taxonomies from ['gtdb-rs214.lineages.sqldb']
found 402709 identifiers in taxdb.
loading file gtdb-rs214-k21.zip as index => manifest
...1000 - loading
...2000 - loading
...3000 - loading
...153000 - loading
...154000 - loading
...155000 - loading
```
 
# Discussion
 ```
...235000 - loading
```
It is taking a while to load these data, did not expect it to take more than 10 mintues. Now I wish that I open different tmux session, I could run all of these at the same time and do not need to worry about wifi disconnection...

Have a question

Should I use gtdb-rs214-k21.zip to run the command to get database for both genus, species and family?
Or use 'gtdb-rs214-k21.zip' to get database for genus, and run 'gtdb-rs214-k21.pangenomes.genus.zip' to get database to get species database, and then run 'gtdb-rs214-k21.pangenomes.species.zip' to get family database.

> ./pangenomeproject/make-pangenome-sketches.py gtdb-rs214-k21.zip -t gtdb-rs214.lineages.sqldb -o gtdb-rs214-k21.pangenomes.genus.zip -k 21 -r species
> 
>./pangenomeproject/make-pangenome-sketches.py gtdb-rs214-k21.pangenomes.genus.zip -t gtdb-rs214.lineages.sqldb -o gtdb-rs214-k21.pangenomes.genus.zip -k 21 -r species

because the script is working with the lower rank data and not merging set, turns out they give the same result
# Journal
This week is valentine day week, something great happened to me >v< .
