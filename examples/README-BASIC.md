# Example: Basic Setup

This example shows the simplest way to use the pytest-and-coverage-action.

## Workflow File

```yaml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: thoughtparametersllc/pytest-and-coverage-action@main
```

## Requirements

- A `requirements.txt` file with your project dependencies
- Test files matching the pattern `test_*.py` or `*_test.py` in the root or `tests/` directory

## Output

The action will:
1. Set up Python 3.11 (default)
2. Install dependencies from `requirements.txt`
3. Run pytest with coverage
4. Generate coverage reports (HTML, XML, JSON)
5. Create a GitHub Summary with coverage metrics
6. Upload coverage reports as artifacts
7. Fail if coverage is below 80% (default threshold)
