# Implement Today I Learned (TIL) Pattern using Github Actions 

Knowledge management is hard.  Especially when you're working with very small bits of knowledge.  Gists tend to accrete but they're hard to locate after the fact. It's easier when you can rely Github to manage the versioning and use their built in tools to create tables of content.  Table of contents?

This is a very sweet solution using [Github Actions](https://help.github.com/en/actions/reference/workflow-syntax-for-github-actions) documented by [Simon Willison](https://simonwillison.net/2020/Apr/20/self-rewriting-readme/).

**Process**

| Step  | Action | Notes |
| ----- | ------ | ----- |
| 1.    | Build new 'til' Repository in Github | |
| 2.    | Create .github/workflows directory | note the dot |
| 3.    | Add in [build.yml](/.github/workflows/build.yml) file |  |
| 4.    | Add [requirements file](/requirements.txt) | at the root |
| 5.    | Add [Build Database File](/build_database.py) | Correct any hardcoded paths |
| 6.    | Add [Update Readme File](/update_readme.py)   | We'll get this right... |


Along the way, I monitored the results in the Actions tab.

![Screen shot](/img/2020.04.20.11.19.0001.jpg "Monitor Actions Tab")

This really helped with debugging obvious errors, but it didn't work where the code ran but didn't actually do anything.   I'm thinking there's a path or credentials issue.