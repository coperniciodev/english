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
```

### Key Components of a Job

The example above highlights the most important parts of a job:

*   **runs-on**: This key specifies the type of machine or environment the job will run on. Common options include ubuntu-latest, windows-latest, and macos-latest. GitHub provides these hosted runners, but you can also use self-hosted runners.
    
*   **steps**: This is a list of all the individual commands or actions that a job will execute. Each step begins with a hyphen and can either run a command using run: or use a pre-built action with uses:.
    
*   **name**: An optional but highly recommended key that provides a descriptive name for the job, which makes it easier to track in the GitHub Actions dashboard.
    
*   **uses**: This is used to call a pre-defined action from the GitHub Marketplace. The @v4 indicates a specific version of the action.
    
*   **run**: This key allows you to execute shell commands directly on the runner.
    

By structuring your workflow into logical jobs, you can create robust, maintainable, and scalable automation pipelines that handle all the tasks for your static site deployment.
