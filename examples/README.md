# Examples Guide

This directory contains example workflows and configurations for using the pytest-and-coverage-action GitHub Action.

## Quick Navigation

### [Basic Setup](README-BASIC.md)
The simplest way to get started with pytest-and-coverage-action. Perfect for small projects or getting started quickly.

**Includes:**
- Minimal workflow configuration
- Default settings (Python 3.11, 80% coverage threshold)
- Automatic artifact upload

### [CI/CD Integration](README-CICD.md)
Complete CI/CD pipeline with multi-version testing, linting, and Codecov integration.

**Includes:**
- Testing on multiple Python versions (3.9-3.12)
- Codecov integration for coverage tracking
- Automated PR comments with coverage results
- Separate linting job

### [Advanced Pytest Configuration](README-ADVANCED.md)
Advanced testing scenarios including markers, fixtures, and parametrized tests.

**Includes:**
- Unit vs integration test separation
- Custom pytest configuration (pytest.ini)
- Pytest fixtures and conftest.py examples
- Different coverage thresholds for different test types

## Sample Files

### requirements-dev.txt
Example development dependencies file with testing and code quality tools:
- pytest, pytest-cov, coverage
- Code quality tools (flake8, black, isort, mypy)
- Testing utilities (pytest-mock, pytest-asyncio, pytest-xdist)
- Data generation (factory-boy, faker)

## Common Use Cases

### 1. Basic Python Project Testing

Use the **Basic Setup** example with:
- A `requirements.txt` file containing project dependencies
- Test files in root or `tests/` directory
- 80% minimum coverage threshold

### 2. Monorepo with Multiple Services

Modify the workflow to run tests in specific directories:
```yaml
pytest-args: '--verbose tests/service_a --cov=service_a'
```

### 3. Docker-based Testing

Use `runs-on: [ubuntu-latest]` (default) or specify custom runners:
```yaml
runs-on: ubuntu-latest  # Works for most projects
runs-on: macos-latest   # For macOS-specific testing
runs-on: windows-latest # For Windows-specific testing
```

### 4. Scheduled Comprehensive Testing

Add a schedule trigger to the workflow:
```yaml
on:
  schedule:
    - cron: '0 2 * * *'  # Daily at 2 AM UTC
```

### 5. Only Run on Specific Branches or Paths

Add path filtering:
```yaml
on:
  push:
    branches: [main, develop]
    paths:
      - 'src/**'
      - 'tests/**'
      - 'requirements.txt'
```

## Customization

### Python Version
Change in the workflow:
```yaml
python-version: '3.11'  # Default
python-version: '3.12'  # Latest
```

### Coverage Threshold
Set different thresholds for different scenarios:
```yaml
coverage-threshold: '80'   # Minimum for public libraries
coverage-threshold: '90'   # Recommended for critical code
```

### Pytest Arguments
Add custom pytest arguments:
```yaml
pytest-args: '--verbose --tb=long -k "not slow"'
```

### Coverage Reports Directory
Change where reports are stored:
```yaml
coverage-dir: 'coverage-reports'  # Default: '.coverage'
```

### Disable Artifact Upload
For lightweight workflows:
```yaml
upload-artifacts: 'false'
```

## Troubleshooting

### Tests not discovered
Ensure your test files follow the pytest naming convention:
- Test files: `test_*.py` or `*_test.py`
- Test functions: `test_*`
- Test classes: `Test*`

### Coverage below threshold but passing locally
This usually means your local setup differs from CI. Check:
- Python version differences
- Missing test dependencies
- Environment variables

### Artifacts not uploading
Verify:
- `upload-artifacts: 'true'` (default)
- Coverage reports are generated successfully
- You have GitHub Actions artifacts storage quota available

## Getting Help

- Check the [main README](../README.md) for full documentation
- Review GitHub Actions [documentation](https://docs.github.com/en/actions)
- Open an issue in the repository
