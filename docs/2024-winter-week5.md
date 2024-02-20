---
title: 2024 winter Week 1
---

# Goals
**Weekly:**
- [ ] follow the pangenome guide https://github.com/ctb/2022-database-covers/blob/pangenome/simple-use-case.md
- [ ] get some idea on how to make sankey diagram
- [ ] change lab notebook style and make it to a website

 
**Quarterly:**
- [ ] Present my work to the lab, presentation on March 18th
- [ ] write some snakemake files
- [ ] have an organized notebook

**Yearly:**
- [ ] have a general understand of what a bioinformatic project is like
- [ ] build experience, present analysis, annotate like scientist
- [ ] Have a well documented project in github that is functional 
 
# Results(base) 

yc22@farm:~$ srun -p bmm -J pangene -t 5:00:00 --mem=10G --pty bash
tmux new -s pan
Thought there is some issue with my private and public key, because when I try to clone it keep declining me
```(base) yc22@farm:~$ git clone -b pangenomes git@github.com:yuenchingshen/2022-database-covers.git
Cloning into '2022-database-covers'...
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.```
Then realised that there is a typo and remember that Colton mentioned about the type during last meeting…
git clone -b pangenomes git@github.com:ccbaumler/2022-database-covers.git
should be
git clone -b pangenome git@github.com:ccbaumler/2022-database-covers.git
Then realised that there is a typo and remember that Colton mentioned about the type during last meeting…

# Discussion 
The result should be
```
sourmash tax prepare --taxonomy-csv /group/ctbrowngrp/sourmash-db/gtdb-rs214/gtdb-rs214.lineages.csv -F sql -o gtdb-rs214.lineages.sqldb
```

Yay, we get the correct output:
```
== This is sourmash version 4.8.5. ==
== Please cite Brown and Irber (2016), doi:10.21105/joss.00027. ==

loading taxonomies...
...loaded 402709 entries.
saving to 'gtdb-rs214.lineages.sqldb', format sql...
done!
```
 

I tried using the absolute path/ location of the file in my computer, and it did not work
```
(base) yc22@farm:~/2022-database-covers$ ls
README.md	    gtdb-rs214.lineages.csv  make-pangenome-sketches.py  run.sh
gtdb-rs214-k21.zip  make-db-cover.py	     make-pangenome.sh		 simple-use-case.md
(base) yc22@farm:~/2022-database-covers$ pwd
/home/yc22/2022-database-covers
(base) yc22@farm:~/2022-database-covers$ sourmash tax prepare --taxonomy-csv /home/yc22/2022-database-covers/gtdb-rs214.lineages.csv -F sql -o gtdb-rs214.lineages.sqldb
sourmash: command not found
```

I was thinking maybe I was in the wrong branch, cause it said sourmash command not found, so I changed directory and tried again. But it still did not work.
```
(base) yc22@farm:~$ ls
2022-database-covers	    miniforge3	      sourmash
Miniforge3-Linux-x86_64.sh  pangenomeproject  spacegraphcats
(base) yc22@farm:~$ sourmash tax prepare --taxonomy-csv /group/ctbrowngrp/sourmash-db/gtdb-rs214/gtdb-rs214.lineages.csv -F sql -o gtdb-rs214.lineages.sqldb
sourmash: command not found
```

 
# Journal
My roommate helped break down and explained to me some concepts in the guide document that I found confusing. He identified the typo for me after I got stuck in step 1 of the guide for over an hour. Haha, felt so lucky to have a computer science major roommate.
