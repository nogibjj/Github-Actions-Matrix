# Hongyi-Duan-Github-Actions-Matrix

[![CI](https://github.com/nogibjj/Github-Actions-Matrix/actions/workflows/ci.yml/badge.svg)](https://github.com/nogibjj/Github-Actions-Matrix/actions/workflows/ci.yml)

# Continuous Integration Setup

This repository uses **GitHub Actions** for Continuous Integration (CI) to ensure that the code is automatically tested, formatted, and linted when changes are pushed or pull requests are created.

## Workflow Overview

The CI workflow is defined in the `.github/workflows/ci.yml` file. The following details explain how the CI works:

### Events Triggering the Workflow

The workflow is triggered by the following events:
- **Push**: When changes are pushed to the `main` branch.
- **Pull Request**: When a pull request is created for the `main` branch.
- **Manual Dispatch**: The workflow can be manually triggered using **workflow_dispatch**.

### Supported Python Versions

The workflow runs the build and tests on the following Python versions:
- PyPy3.9
- PyPy3.10
- Python 3.9
- Python 3.10
- Python 3.11
- Python 3.12

### Build Job

Each time the workflow is triggered, it runs a **build** job. The steps in the build job are as follows:

1. **Checkout the Repository**  
   This action checks out the code from the repository:
   ```yaml
   - uses: actions/checkout@v4
   ```

2. **Set Up Python**  
   Python is set up for the specific versions listed in the matrix:
   ```yaml
   - name: Set up Python ${{ matrix.python-version }}
     uses: actions/setup-python@v5
     with:
       python-version: ${{ matrix.python-version }}
   ```

3. **Install Dependencies**  
   The necessary dependencies are installed using the `make install` command:
   ```yaml
   - name: Install packages
     run: make install
   ```

4. **Run Tests**  
   The test suite is run using the `make test` command:
   ```yaml
   - name: Run tests
     run: make test
   ```

5. **Code Formatting**  
   The code is automatically formatted using the `make format` command:
   ```yaml
   - name: Format code
     run: make format
   ```

6. **Linting**  
   The code is linted using the `make lint` command:
   ```yaml
   - name: Lint code
     run: make lint
   ```

## Running the CI Locally

To ensure consistency with the CI setup, you can run the following commands locally using `make`:

1. **Install dependencies**:
   ```bash
   make install
   ```

2. **Run tests**:
   ```bash
   make test
   ```

3. **Format the code**:
   ```bash
   make format
   ```

4. **Lint the code**:
   ```bash
   make lint
   ```

## Additional Notes

- The `Makefile` is expected to contain `install`, `test`, `format`, and `lint` targets. These targets should handle dependency installation, running tests, formatting code, and running linting checks respectively.
- The CI is designed to run on `ubuntu-latest` as the host environment.
