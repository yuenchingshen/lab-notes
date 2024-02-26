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

(sourmash) yc22@farm:~$ ln -s gtdb-rs214.lineages.csv ./
ln: failed to create symbolic link './gtdb-rs214.lineages.csv': File exists

(sourmash) yc22@farm:~$ sourmash sketch -o Ecoli.gather.sig --name "s__Escherichia coli" -p scaled=2000,k=21,abund Ecoli.gather_*fastq.gz
 sketch: error: argument subcmd: invalid choice: 'Ecoli.gather.sig' (choose from 'dna', 'rna', 'nucleotide', 'nt', 'fromfile', 'protein', 'aa', 'prot', 'translate')

grep 's__Escherichia coli' data.csv > filtered_data.csv 



 

mport pandas as pd
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


 
# Discussion
# Journal

 

