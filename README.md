# lab-notes
A simple, easy lab notebook website

> - Note: Consider integrating your HackMD or Obsidian with your GitHub account. This ***could*** make formatting each of your markdown files a simpler task.
> - Check out [Issue #1](https://github.com/ccbaumler/lab-notes-template/issues/1)

## Intended Use
To create your own website!

Start by:

1. Fork this repo as `lab-notes`
2. Click `Settings` > `Pages`
3. In the `Source` dropdown, select `Deploy from a branch`
4. In the `Branch` dropdown, select `main` then click `Save`
5. Update the title in `index.md` with `<YourName>'s Lab Notebook`

To update your website with your markdown documents:

1. Consider removing the template file in the `docs` directory... or don't and just delete it.
2. Add any number of your own **markdown** documents the `docs` directory
   - The document file name should not contain any whitespaces and must end in `.md`
   	- ~~no whitespaces in file names.md~~
   	- ~~must-contain-.-md-at-the-end~~
   - 2024-week-1.md

Each markdown document added to the `docs` directory will become a link on your webpage landing page. Each link will take you to the rendered markdown document.

A basic document template:

```
---
title: Year Week number
---

# Goals
In this section I will list the weekly, quarterly, and yearly goals I hope to achieve or have completed this week.

**Weekly:**
- [x]  Create a lab notebook repo
- [ ]  Read the docs

**Quarterly:**
- [ ] Present my work to the lab
- [ ] Write some python code
- [ ] Write some snakemake files

**Yearly:**
- [ ] Have a well documented project in github that is functional (if not perfect)

# Results
In this section write the verbatim results (eg. copy the code chunks, error reports, plots) that relate to the goals you have achieved this week.

example:
This week I created a lab notebook repo using this method (include the cli arguments and the process below)

# Discussion
In this section explain your results and how they relate to you goals

example:
I am applying for credit this quarter. Therefore, I chose to create a lab notebook repo in github to continue practicing git and github as it is an important tool for biotech/bioinformatics.

# Journal
In this section add anything else you may wish to include.

example:
Nothing additional to comment this week. Work has been taken allot of my time this week. It's finals, I was not able to complete the goals I thought I would. I got a new hamster and it is very fluffy.
```

## Resources

1. [github actions commit bot](https://github.com/orgs/community/discussions/26560#discussioncomment-3531273)
2. [github markdown syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
3. [github jekyll themes](https://pages.github.com/themes/)
4. [github theme title fix](https://github.com/pages-themes/cayman/issues/134#issuecomment-1000227220)
5. [easy markdown to github pages](https://nicolas-van.github.io/easy-markdown-to-github-pages/)
