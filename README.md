# pytest-and-coverage-action

A GitHub Action to run pytest with coverage reporting, artifact uploading, and GitHub Summary integration.

## Features

- 🧪 **Run pytest** with customizable arguments
- 📊 **Generate coverage reports** (HTML, XML, JSON)
- ⬆️ **Upload artifacts** for easy access to coverage reports
- 📝 **Create GitHub Summary** with coverage metrics and threshold validation
- ✅ **Coverage threshold checking** to ensure code quality standards
- 🔄 **Flexible configuration** with sensible defaults

## Usage

### Basic Usage

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

### Advanced Usage with Custom Inputs

```yaml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - uses: thoughtparametersllc/pytest-and-coverage-action@main
        with:
          python-version: '3.11'
          requirements-file: 'requirements-test.txt'
          coverage-threshold: '85'
          pytest-args: '--verbose --strict-markers -m "not slow"'
          coverage-dir: 'coverage-reports'
          upload-artifacts: 'true'
          artifact-retention-days: '30'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `python-version` | Python version to use | No | `3.11` |
| `requirements-file` | Path to requirements file | No | `requirements.txt` |
| `coverage-threshold` | Minimum coverage percentage threshold | No | `80` |
| `pytest-args` | Additional arguments to pass to pytest | No | `--verbose` |
| `coverage-dir` | Directory to store coverage reports | No | `.coverage` |
| `upload-artifacts` | Whether to upload coverage artifacts | No | `true` |
| `artifact-retention-days` | Number of days to retain artifacts | No | `30` |

## Outputs

| Output | Description |
|--------|-------------|
| `coverage-percentage` | Overall coverage percentage |
| `coverage-status` | Whether coverage meets threshold (success/failure) |
| `test-result` | Test result status (success/failure) |

## Generated Reports

The action generates the following coverage reports:

- **HTML Report**: Interactive HTML coverage report saved to `{coverage-dir}/html/`
- **XML Report**: Cobertura-compatible XML report for CI/CD integration at `{coverage-dir}/coverage.xml`
- **JSON Report**: Machine-readable JSON report at `{coverage-dir}/coverage.json`
- **Terminal Report**: Detailed terminal output with missing lines information

## GitHub Summary

The action automatically creates a GitHub Summary with:
- Overall coverage percentage
- Number of statements analyzed
- Number of missing and excluded lines
- Pass/fail status against the specified threshold
- Link to the uploaded coverage artifacts

## Example Workflow

Here's a complete example workflow using this action:

```yaml
name: Test Suite

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ['3.9', '3.10', '3.11']
    
    steps:
      - uses: actions/checkout@v4
      
      - uses: thoughtparametersllc/pytest-and-coverage-action@main
        with:
          python-version: ${{ matrix.python-version }}
          coverage-threshold: '80'
          pytest-args: '--verbose --cov-report=term-missing'
      
      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v3
        with:
          files: .coverage/coverage.xml
          fail_ci_if_error: true
```

## Requirements

The action automatically installs:
- `pytest`
- `pytest-cov`
- `coverage`

Any additional dependencies should be specified in your `requirements.txt` or the file specified by `requirements-file`.

## Outputs from Steps

The action provides three main outputs that can be used in subsequent steps:

```yaml
- uses: thoughtparametersllc/pytest-and-coverage-action@main
  id: test-coverage

- name: Check coverage output
  run: |
    echo "Coverage: ${{ steps.test-coverage.outputs.coverage-percentage }}"
    echo "Status: ${{ steps.test-coverage.outputs.coverage-status }}"
    echo "Test Result: ${{ steps.test-coverage.outputs.test-result }}"
```

## Troubleshooting

### Coverage reports not being generated

Ensure your tests are executable and that `pytest` and `pytest-cov` are installed. Check that your test files match the pytest discovery patterns (e.g., `test_*.py` or `*_test.py`).

### Artifacts not uploading

Verify that:
- `upload-artifacts` is set to `true` (default)
- The `coverage-dir` path exists and has content
- Your GitHub Actions permissions allow artifact uploads

### Coverage threshold check failing

The threshold check compares the total coverage percentage against the specified threshold. Ensure:
- Your threshold value is reasonable for your project
- Coverage reports are being generated correctly
- You have test cases covering your code

## License

See [LICENSE](LICENSE) for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.