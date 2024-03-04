---
title: 2024 winter Week 6
---

# Goals
**Weekly:**
- [x]  continue making python code
- [x]  made the sankey graph
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
python code
```
import pandas as pd
import plotly.graph_objects as go
import plotly.io as py

# Load the CSV file into a DataFrame
df = pd.read_csv('small.csv')

# Create lists to hold the source, target, and value data for the Sankey diagram
sources = [] # Each index contains one source to be matched to a target in the same index
targets = [] # Contains all the targets for the sankey graph
values = [] # All 1s since each ident is unique

# Define the hierarchy
hierarchy = ['family', 'genus', 'species', 'ident']

# Create a labels array to store all the different names for each level
labels = []

# Iterate over each row in the DataFrame to populate the sources, targets, and values lists
# Loop through each row
for _, row in df.iterrows():
    # Loop each family -> genus -> species in the row
    for i, level in enumerate(hierarchy[:-1]):
        # Set the current and next level according to the hierarchy
        current_label = row[level]
        next_label = row[hierarchy[i+1]]

        # Add labels if does not exist
        if current_label not in labels:
            labels.append(current_label)

        if next_label not in labels:
            labels.append(next_label)

        # Set the source to the current label
        sources.append(labels.index(current_label))
        # Set the target to the next label
        targets.append(labels.index(next_label))
        # Since each ident is unique there is only 1
        values.append(1)
# Create a Sankey diagram figure using Plotly
fig = go.Figure(data=[go.Sankey(
    # Set details for all the nodes (labels)
    node=dict(
        pad=15,
        thickness=20,
        line=dict(color="black", width=0.5),
        label=labels  # Use the updated labels list
    ),
    # Use the generated source target and value array for the graph
    link=dict(
        source=sources,
        target=targets,
        value=values
    )
)])

# Adjust the height of the graph to scale with the amount of labels
height_graph = len(labels) * 10

# Update layout
fig.update_layout(title_text="Sankey Diagram", font_size=10, height=height_graph)

# Save the Sankey diagram as an HTML file
py.write_html(fig, file='sankey_diagram.html', auto_open=True)
```
```
yuenchingshen@Yuens-Air sourmash % ls
filtered_data.csv	gtdb-rs214.lineages.csv	sankey_graph.html	script.py		slack.txt
filtered_data.csv2	sankey_diagram.png	sankey_graph.png	scriptpng.py
yuenchingshen@Yuens-Air sourmash % vi script.py 
yuenchingshen@Yuens-Air sourmash % cat sm
yuenchingshen@Yuens-Air sourmash % 
yuenchingshen@Yuens-Air sourmash % head -n 1000 gtdb-rs214.lineages.csv > small.csv
yuenchingshen@Yuens-Air sourmash % python script.py 
zsh: command not found: python
yuenchingshen@Yuens-Air sourmash % python3 script.py
yuenchingshen@Yuens-Air sourmash % head -n 100 gtdb-rs214.lineages.csv > small.csv 
yuenchingshen@Yuens-Air sourmash % python3 script.py 
```
9data: https://drive.google.com/file/d/1Pg25QUI35iNO1e0OKq-sUXrsO1Iak8-O/view?usp=sharing
1000data: https://drive.google.com/file/d/1TPktOJOt-3V5xRVmAzUc-zQ10vtdG2tb/view?usp=sharing
10000data: https://drive.google.com/file/d/1wh0iE6Ez2dksmILDN8IBg0FuZWpz9hjt/view?usp=sharing

# Discussion
the sankey graph seems to work now, should work with larger data set too, but I cannot run files that is too big with my computer.
 

# Journal
the presentation was going to be on march 4th, did not expect it to be that quick.moved the date to 18th
