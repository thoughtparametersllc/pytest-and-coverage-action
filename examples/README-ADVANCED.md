# Example: Advanced Pytest Configuration

This example shows how to use advanced pytest features with the action, including markers, fixtures, and parametrized tests.

## Workflow File

```yaml
name: Advanced Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Run unit tests
        uses: thoughtparametersllc/pytest-and-coverage-action@main
        with:
          python-version: '3.11'
          coverage-threshold: '90'
          pytest-args: |
            --verbose
            --strict-markers
            --tb=short
            -m "not integration and not slow"
      
      - name: Run integration tests
        uses: thoughtparametersllc/pytest-and-coverage-action@main
        if: github.event_name == 'push'
        with:
          python-version: '3.11'
          coverage-threshold: '70'
          pytest-args: '-m "integration" --tb=short'
          coverage-dir: '.coverage-integration'
```

## pytest.ini Configuration

```ini
[pytest]
testpaths = tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
markers =
    unit: Unit tests (fast, no external dependencies)
    integration: Integration tests (may require external services)
    slow: Slow running tests
    db: Tests requiring database
addopts = 
    -v
    --strict-markers
    --disable-warnings
```

## conftest.py Example

```python
import pytest
from unittest.mock import Mock

@pytest.fixture
def sample_fixture():
    """Sample fixture for tests."""
    return {"key": "value"}

@pytest.fixture
def mock_external_service():
    """Mock external service."""
    return Mock()
```

## Key Features

- **Marker-based test selection**: Run unit, integration, or slow tests separately
- **Multiple test runs**: Different thresholds for unit vs integration tests
- **Custom pytest configuration**: Full pytest.ini support
- **Pytest plugins**: Compatibility with pytest-xdist, pytest-asyncio, etc.

## Sample Test File

```python
import pytest

@pytest.mark.unit
def test_addition():
    assert 2 + 2 == 4

@pytest.mark.unit
def test_subtraction():
    assert 5 - 3 == 2

@pytest.mark.integration
def test_external_api(mock_external_service):
    mock_external_service.get.return_value = {"status": "ok"}
    result = mock_external_service.get()
    assert result["status"] == "ok"

@pytest.mark.slow
def test_long_running():
    # This test is slow and can be skipped in CI
    pass
```
