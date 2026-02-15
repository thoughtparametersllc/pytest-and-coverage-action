# Example: CI/CD Integration

This example shows how to integrate the pytest-and-coverage-action with other tools like Codecov and run tests on multiple Python versions.

## Workflow File

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - run: |
          pip install flake8
          flake8 src/ tests/

  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ['3.9', '3.10', '3.11', '3.12']
    
    steps:
      - uses: actions/checkout@v4
      
      - name: Run tests with coverage
        id: coverage
        uses: thoughtparametersllc/pytest-and-coverage-action@main
        with:
          python-version: ${{ matrix.python-version }}
          coverage-threshold: '85'
          pytest-args: '--verbose --tb=short'
      
      - name: Upload to Codecov
        uses: codecov/codecov-action@v3
        with:
          files: .coverage/coverage.xml
          fail_ci_if_error: true
      
      - name: Comment on PR
        if: github.event_name == 'pull_request'
        uses: actions/github-script@v6
        with:
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: `## Test Coverage Report\n\nCoverage: ${{ steps.coverage.outputs.coverage-percentage }}\nStatus: ${{ steps.coverage.outputs.coverage-status }}`
            })
```

## Key Features

- **Multi-version testing**: Tests on Python 3.9, 3.10, 3.11, and 3.12
- **Linting**: Runs flake8 to check code style
- **Codecov integration**: Uploads coverage to Codecov for badge and tracking
- **PR comments**: Automatically comments on pull requests with coverage results
- **Workflow status**: Fails the workflow if coverage is below threshold

## Requirements

- `requirements.txt`: Project dependencies
- `requirements-dev.txt` (optional): Development dependencies (linting tools, etc.)
- `.flake8` or similar config (optional): Linting configuration
