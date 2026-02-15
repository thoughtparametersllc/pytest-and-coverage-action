# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial release of pytest-and-coverage-action
- Support for pytest with coverage reporting
- HTML, XML, and JSON coverage report generation
- GitHub Summary creation with coverage metrics
- Configurable coverage threshold checking
- Automatic artifact upload with retention settings
- Support for multiple Python versions (3.9+)
- Example workflows for various use cases
- Comprehensive documentation and troubleshooting guides

### Features
- Run pytest with customizable arguments
- Generate HTML, XML, and JSON coverage reports
- Create GitHub Summary with coverage status
- Upload coverage artifacts for later access
- Check coverage against configurable threshold
- Support for custom requirements files
- Multi-version testing support
- Flexible configuration with sensible defaults

### Documentation
- README with usage instructions
- Multiple example workflows (basic, CI/CD, advanced)
- Example requirements file with common dependencies
- Troubleshooting guide
- API documentation for inputs and outputs

## Standards

### Versioning
- MAJOR version for incompatible API changes
- MINOR version for new functionality (backward compatible)
- PATCH version for bug fixes (backward compatible)

### Release Process
1. Update version in action.yml
2. Update CHANGELOG.md
3. Create a git tag (e.g., v1.0.0)
4. Push tag to trigger release workflow
5. Update major version tag to point to latest release

## Future Enhancements

Potential features for future releases:
- Support for parallel test runs with pytest-xdist
- Integration with different coverage tools (e.g., coverage.py plugins)
- Custom report formatting and templates
- Slack/Teams notifications with coverage updates
- Coverage trend tracking and historical reporting
- Support for different testing frameworks (unittest, nose)
- Docker image for consistent testing environment
