# Contributing to pytest-and-coverage-action

Thank you for your interest in contributing to pytest-and-coverage-action! This document provides guidelines and instructions for contributing.

## Code of Conduct

This project and everyone participating in it is governed by a Code of Conduct. By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the issue list as you might find out that you don't need to create one. When you are creating a bug report, please include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps which reproduce the problem**
- **Provide specific examples to demonstrate the steps**
- **Describe the behavior you observed after following the steps**
- **Explain which behavior you expected to see instead and why**
- **Include screenshots and animated GIFs if possible**

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, please include:

- **Use a clear and descriptive title**
- **Provide a step-by-step description of the suggested enhancement**
- **Provide specific examples to demonstrate the steps**
- **Describe the current behavior and expected behavior**
- **Explain why this enhancement would be useful**

### Pull Requests

- Fill in the required template
- Follow the Python PEP 8 style guide
- Include appropriate test cases
- Update documentation as needed
- End all files with a newline

## Development Setup

### Prerequisites
- Python 3.9 or higher
- Git

### Setting Up Development Environment

1. Fork and clone the repository:
```bash
git clone https://github.com/your-username/pytest-and-coverage-action.git
cd pytest-and-coverage-action
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install development dependencies:
```bash
pip install -r requirements-dev.txt
```

### Testing Changes

1. Test with pytest:
```bash
pytest tests/ --cov=. --cov-report=html
```

2. Check with linting tools:
```bash
flake8 src/ tests/
black src/ tests/
isort src/ tests/
mypy src/
```

### Commit Messages

- Use the present tense ("Add feature" not "Added feature")
- Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less
- Reference issues and pull requests liberally after the first line

## Action Development Guidelines

### Modifying action.yml

The `action.yml` file defines the GitHub Action interface. When modifying:

1. **Inputs**: Add proper descriptions and set reasonable defaults
2. **Outputs**: Ensure outputs are documented and tested
3. **Steps**: Keep the composite action steps clear and well-commented

### File Structure

- `action.yml` - Main action definition
- `README.md` - User-facing documentation
- `examples/` - Example workflows and configurations
- `.github/workflows/` - Self-testing workflows

### Testing the Action

You can test locally by:

1. Creating a test repository or branch
2. Referencing your local action in a workflow:
```yaml
- uses: ./
  with:
    coverage-threshold: '75'
```

3. Running the workflow locally with `act`:
```bash
brew install act  # or see https://github.com/nektos/act
act -j test
```

## Documentation

### README Updates

- Keep examples clear and up-to-date
- Update the documentation when adding new features
- Include troubleshooting sections for common issues

### Example Workflows

- Add examples in the `examples/` directory
- Include comments explaining key concepts
- Document any special requirements or setup

### Version Documentation

- Update CHANGELOG.md for all user-facing changes
- Include version numbers in release notes
- Document breaking changes clearly

## Release Process

1. Update version references in:
   - `action.yml` (if needed)
   - `CHANGELOG.md`

2. Create a semantic version tag:
```bash
git tag v1.x.x
git push origin v1.x.x
```

3. GitHub will automatically create a release from the tag

4. Update the major version tag (e.g., `v1`):
```bash
git tag -f v1
git push -f origin v1
```

## Style Guide

### YAML

- Use 2 spaces for indentation
- Be explicit with types (use quotes for strings when needed)
- Comment complex or non-obvious configurations

### Markdown

- Use appropriate heading levels
- Keep line lengths reasonable (80-120 characters)
- Use code blocks with language specification for clarity

## Questions?

Feel free to open an issue with the tag `question` if you have any questions about the project or how to contribute.

## License

By contributing to pytest-and-coverage-action, you agree that your contributions will be licensed under the same license as the project (see LICENSE file).

## Acknowledgments

Thanks to all contributors who have helped make this project better!
