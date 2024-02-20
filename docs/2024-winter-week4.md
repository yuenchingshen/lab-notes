---
title: 2024 winter Week 1
---

# Goals
**Weekly:**
- [x] Play with parameter, stick with a set k value (k=31), try to see/ visualize different database
- [ ] Run gather result
- [ ] the different between using 3 data base (family, genius, specie) and normal
 
 
**Quarterly:**
- [ ] Present my work to the lab, presentation on March 18th
- [ ] write some snakemake files
- [ ] have an organized notebook

**Yearly:**
- [ ] have a general understand of what a bioinformatic project is like
- [ ] build experience, present analysis, annotate like scientist
- [ ] Have a well documented project in github that is functional 
 
# Results
include text on what's confusing
Links 
CAMISM: https://github.com/CAMI-challenge/CAMISIM/wiki/User-manual
Sourmash, gather: https://sourmash.readthedocs.io/en/latest/command-line.html#sourmash-gather-find-metagenome-members
Sourmash, signatures, comparing, and searching:
https://sourmash.readthedocs.io/en/latest/tutorial-basic.html

[ x ]install mamba module: https://sourmash.readthedocs.io/en/latest/tutorial-install.html
[  ]Play with parameter, stick with a set k value k=31, try to see, visualize different database
-?What data am I using as reference genome?
-?where to get the data to make a database? E Coli reference genome from the sourmash tutorial/ Ncbi page/ from CAMISIM, get the simulated metagenomic dataset (?)
Configuration file?, what should the number of abundance, specie be

[  ]Run gather result
Download and unzip the sourmash database:
curl -L https://osf.io/4f8n3/download -o genbank-k31.lca.json.gz
gunzip genbank-k31.lca.json.gz
And then run gather
sourmash gather -o SRR1976948_gather.csv SRR1976948.sig genbank-k31.lca.json

[  ]See the different between using 3 data base (family, genius, specie) and normal. Make a box plot to visualize the difference.
Can visualize these three aspect. 
‘overlap’, the first column, is the estimated number of base pairs shared between the match and the query, based on the number of shared hashes.
‘p_query’ is the percentage of the query that overlaps with the match; it is the amount of the metagenome “explained” by this match. It is typically a lower bound on the percent of metagenomes reads that will map to this genome.
‘p_match’ is the percentage of the match that overlaps with the query; it is the “detection” of the match in the metagenome. It is typically a lower bound on the number of base pairs that will be covered by read mapping.

# Discussion
Quite confused and don’t know where to start.
How to improve: understand project goal before starting, familiarize with tool, seek help

# Journal
I saved my organic chemistry from a F to an D+ to a C now. Hopefully it wil then get back track as time goes on.
