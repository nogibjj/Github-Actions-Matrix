# Hongyi-Duan-Mini-Project-1

[![CI](https://github.com/nogibjj/Github-Actions-Matrix/actions/workflows/ci.yml/badge.svg)](https://github.com/nogibjj/Github-Actions-Matrix/actions/workflows/ci.yml)

Continuous Integration Setup
This repository uses GitHub Actions for Continuous Integration (CI) to ensure the code is automatically tested, formatted, and linted upon certain events, such as pushing changes to the main branch or creating a pull request.

Workflow Overview
The CI workflow is defined in the ci.yml file located in the .github/workflows/ directory. This workflow performs the following actions:

Events Triggering the Workflow
The workflow is triggered by the following events:

Push: When changes are pushed to the main branch.
Pull Requests: When a pull request is created for the main branch.
Manual Dispatch: The workflow can also be triggered manually using the workflow_dispatch event.
Supported Python Versions
The workflow is configured to run on the following versions of Python:

PyPy3.9
PyPy3.10
Python 3.9
Python 3.10
Python 3.11
Python 3.12
Build Job
Each time the workflow is triggered, it runs a build job that executes the following steps:

Checkout the Repository: The action checks out the code from the repository:

yaml
复制代码
- uses: actions/checkout@v4
Set Up Python: The specific Python version is set up for each job using the setup-python action:

yaml
复制代码
- name: Set up Python ${{ matrix.python-version }}
  uses: actions/setup-python@v5
  with:
    python-version: ${{ matrix.python-version }}
Install Packages: All necessary dependencies are installed using the make install command. This assumes that a Makefile exists with an install target defined.

yaml
复制代码
- name: install packages
  run: make install
Run Tests: The code is tested using the make test command. It is expected that the repository has a test target in the Makefile that runs the relevant test suite.

yaml
复制代码
- name: test
  run: make test
Code Formatting: The code is formatted according to predefined formatting rules using the make format command.

yaml
复制代码
- name: format
  run: make format
Linting: The code is checked for style and potential errors using a linter, invoked by the make lint command.

yaml
复制代码
- name: lint
  run: make lint
Running the CI Locally
To ensure consistency with the CI setup, you can run the following make commands locally:

Install dependencies:

bash
复制代码
make install
Run tests:

bash
复制代码
make test
Format the code:

bash
复制代码
make format
Lint the code:

bash
复制代码
make lint
