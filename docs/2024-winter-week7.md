---
title: 2024 winter Week 6
---

# Goals
**Weekly:**
- [x]  start making python code
- [ ]  start making presentation slides
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
try to use sourmash gather to make a small file with only ecoli data, so I could work with smaller data to test out the sankey graph
I did not realise that I was following the wrong tutorial, was confused why the code did not work.

```
(sourmash) yc22@farm:~$ ln -s gtdb-rs214.lineages.csv ./
ln: failed to create symbolic link './gtdb-rs214.lineages.csv': File exists
(sourmash) yc22@farm:~$ sourmash sketch -o Ecoli.gather.sig --name "s__Escherichia coli" -p scaled=2000,k=21,abund Ecoli.gather_*fastq.gz
 sketch: error: argument subcmd: invalid choice: 'Ecoli.gather.sig' (choose from 'dna', 'rna', 'nucleotide', 'nt', 'fromfile', 'protein', 'aa', 'prot', 'translate')
```
Then use a code instead of gather to make the file, still works the same
```
grep 's__Escherichia coli' data.csv > filtered_data.csv 
```


the code for sankey graph:
```
import pandas as pd
import plotly.graph_objects as go
import plotly.io as py

# Load the CSV file into a DataFrame
df = pd.read_csv('filtered_data.csv')

# Create lists to hold the source, target, and value data for the Sankey diagram
sources = []
targets = []
values = []

# Define the hierarchy
hierarchy = ['superkingdom', 'phylum', 'class', 'order', 'family', 'genus', 'species', 'ident']

# Create a labels list using the hierarchy
labels = []

# Iterate over each row in the DataFrame to populate the sources, targets, and values lists
for _, row in df.iterrows():
    for i in range(len(hierarchy)-1):
        if row[hierarchy[i]] not in labels:
            labels.append(row[hierarchy[i]])
        if row[hierarchy[i+1]] not in labels:
            labels.append(row[hierarchy[i+1]])
        sources.append(labels.index(row[hierarchy[i]]))
        targets.append(labels.index(row[hierarchy[i+1]]))
        values.append(1)

# Create a Sankey diagram figure using Plotly
fig = go.Figure(data=[go.Sankey(
    node=dict(
        pad=15,
        thickness=20,
        line=dict(color="black", width=0.5),
        label=labels
    ),
    link=dict(
        source=sources,
        target=targets,
        value=values
    )
)])

fig.update_layout(title_text="Sankey Diagram", font_size=10, autosize=False, width=3000, height=5000)

# Save the figure as a PNG image
py.write_image(fig, 'sankey_diagram.png', scale=2)

# Open the saved image
import os
os.system("open sankey_diagram.png")
``` 
# Discussion

``` 
yuenchingshen@Yuens-Air sourmash % python3 script.py                     
yuenchingshen@Yuens-Air sourmash % cp sankey_diagram.png
yuenchingshen@Yuens-Air sourmash % 
yuenchingshen@Yuens-Air sourmash % cp filtered_data.csv2 filtered_data.csv
yuenchingshen@Yuens-Air sourmash % python3 script.py                      
yuenchingshen@Yuens-Air sourmash % ls
filtered_data.csv	sankey_diagram.png	sankey_graph.png
filtered_data.csv2	sankey_graph.html	script.py
yuenchingshen@Yuens-Air sourmash % vi filtered_data.csv
yuenchingshen@Yuens-Air sourmash % vi script.py 
yuenchingshen@Yuens-Air sourmash % python3 script.py 
``` 

I tried to plot sankey graph with 1/10 of the gtdb-rs214.lineages.csv data, cause it take quite a while to run and my mac, safari can not handel it.
The graph turns out looking a bit different from what I expected though, I expect there are different lineage from each hierarch('superkingdom', 'phylum', 'class', 'order', 'family', 'genus', 'species', 'ident'). But for the graph that I generated, only difference between 'species' and 'ident'. Maybe I wrote something wrong...
The graph:
https://drive.google.com/file/d/1r82PSofM0nDT-6NbXyul-VGzrJ4gVhmb/view?usp=sharing

When checking the data in the csv file, I know what that there should be more lineage difference.
``` 
ident,gtdb_representative,superkingdom,phylum,class,order,family,genus,species
GCA_000008085.1,t,d__Archaea,p__Nanoarchaeota,c__Nanoarchaeia,o__Nanoarchaeales,f__Nanoarchaeaceae,g__Nanoarchaeum,s__Nanoarchaeum equitans
GCA_000016605.1,t,d__Archaea,p__Thermoproteota,c__Thermoprotei_A,o__Sulfolobales,f__Sulfolobaceae,g__Metallosphaera,s__Metallosphaera sedula
GCA_000145985.1,t,d__Archaea,p__Thermoproteota,c__Thermoprotei_A,o__Sulfolobales,f__Ignisphaeraceae,g__Ignisphaera,s__Ignisphaera aggregans
```
But the graph just only show a straight thick line.

# Journal
I recieved many help to on making the sankey graph from my housemate, it is really nice of them.
 

