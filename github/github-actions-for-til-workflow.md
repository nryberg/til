# Implement Today I Learned (TIL) Pattern using Github Actions 

Knowledge management is hard.  Especially when you're working with very small bits of knowledge.  Gists tend to accrete but they're hard to locate after the fact. It's easier when you can rely Github to manage the versioning and use their built in tools to create tables of content.  Table of contents?

This is a very sweet solution using [Github Actions](https://help.github.com/en/actions/reference/workflow-syntax-for-github-actions) documented by [Simon Willison](https://simonwillison.net/2020/Apr/20/self-rewriting-readme/).

Here's my action built on Simon's:

```yml
name: Build README and deploy Datasette

on:
  push:
    branches:
    - master
    paths-ignore:
    - README.md

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Check out repo
      uses: actions/checkout@v2
      # We need full history to introspect created/updated:
      with:
        fetch-depth: 0  
    - name: Set up Python
      uses: actions/setup-python@v1
      with:
        python-version: 3.8
    - uses: actions/cache@v1
      name: Configure pip caching
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
        restore-keys: |
          ${{ runner.os }}-pip-
    - name: Install Python dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Build database
      run: python build_database.py
    - name: Update README
      run: |-
        python update_readme.py --rewrite
        cat README.md
    - name: Commit and push if README changed
      run: |-
        git diff
        git config --global user.email "readme-bot@example.com"
        git config --global user.name "README-bot"
        git diff --quiet || (git add README.md && git commit -m "Updated README")
        git push

```
