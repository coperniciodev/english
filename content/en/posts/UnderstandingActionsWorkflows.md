---
title: "Understanding Jobs in GitHub Actions Workflows"
date: 2025-09-02
tags: ["github actions", "ci/cd", "yaml", "workflow", "tutorial"]
draft: false
---

## Introduction

In a GitHub Actions workflow, a **job** is the fundamental unit of work. It is a defined set of steps that execute on a single runner. A workflow can contain one or more jobs, which by default run in parallel, though they can be configured to run sequentially if needed. Understanding jobs is crucial for automating complex tasks and ensuring your build and deployment processes are organized and efficient.

### What Is a Job?

A job is essentially a container for all the steps required to complete a specific task. For example, a single workflow might have separate jobs for building a website, running tests, and deploying the final product. Each job has a unique identifier and is responsible for running on a specific virtual machine or "runner."

A job is defined within the `jobs:` key in your workflow's YAML file.

Here is a simple example of a single job named `build_and_deploy`:

```yaml
jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Build site with MkDocs
        run: mkdocs build
      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force