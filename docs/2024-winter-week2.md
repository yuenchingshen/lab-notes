---
title: 2024 winter Week 1
---

# Goals
**Weekly:**
- [x] do the reading
 
**Quarterly:**
- [ ] Present my work to the lab, presentation on March 18th
- [ ] write some snakemake files
- [ ] have an organized notebook

**Yearly:**
- [ ] have a general understand of what a bioinformatic project is like
- [ ] build experience, present analysis, annotate like scientist
- [ ] Have a well documented project in github that is functional 
 
# Results
learned more about the pangenome project, after doing more reading (how do sourmash work, https://sourmash.readthedocs.io/en/latest/), (github pangenome project branch:https://github.com/ctb/2022-database-covers/tree/pangenome)it is about:
Sourmash has a function called “gather”, it is used to compare and match sequences.
How it works is, for the input sequences(dna, rna, protein etc), it will break them into small chunks of “k-mers”. 
Then “hash” them into numeric output so the computer can understand. 
A subset of hash values is selected and within all those, the smallest one,"minhash" will be used to compare.
Question: (if they are all 1 k-mer long, how come some hash value is smaller?)
Hash function converts k-mer to number, the function results in a different number, k-mer length will not directly impact the number.
Using the “minhash”, sourmash compares it to a metagenome from SRA, and returns the first result.
Since it only returns the first result, it might return some things that share the same small chunk of DNA sequence but not what the input is. We would use that incorrect result without knowing that it is wrong.
In this case, the project’s idea is, to create a conda environment with pangenome data database. Pangenome contain gene sequences shared between the entire species/taxa. If sourmash uses the pangenome database, then it will help us locate where our input sample is from broader view. Also there would be less duplicate data.
Then, we can use the pangenome result to compare with the SRA result, to double check the output and minimize error occurring.

# Discussion
Discussion:
I am still a bit confused about how “gather” uses the “minhash”, so “minhash” represents 1 kmer of sequence in numeric format. It is picked over all other “hashes” because it has the smallest number, thus requiring the least amount of computation. “Gather”, compare “minhash”, this small chunk of sequence will all other sequences in the database. And return the first result of that match. Is that correct? It is only using one small chunk of sequence for the comparison, it does not feel very accurate for me. I thought it would include more statistics, like selecting a few “minhash”, then picking the one that has the most matching percentage.
After looking at some information about minhash sketching work, it kinda answered my question. Maybe one “minhash”is enough to figure out and match. In terms of speed and computation needed, that is the most cost/time benefit method??
 
# Journal
 I had organic chemistry this quarter and just had my first 2 assignments and test on jan18, just got the result back and it is horrible. Which resulted in a D for my grade… I have never got such a low score on a midterm/test. Organic chemistry is very different from chemistry and I need some time to pick it up…I spent most of this week preparing for the test already but still…Will definitely talk to TAs and go to office hours about how to do better.
Thought 14 units would make my schedule much more flexible, but… I guess I underestimated organic chemistry’s difficulties.

For the internship application, it turns out I never submitted the form, it was marked as “draft” and I thought it means that the faculty is still reviewing it… Now I’m contacting the advisor to see if there is a way to do it.
