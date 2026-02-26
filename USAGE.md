# Template Usage Guide

This guide provides detailed information about using the python-cli-template.

## Quick Start

```bash
# Install copier if you haven't already
pip install copier

# Create a new project from this template
copier copy gh:bengineerdavis/python-cli-template my-awesome-cli

# Follow the prompts to configure your project
```

## Template Questions Explained

### Project Name
The display name of your project. Can contain spaces, hyphens, or underscores.
- Example: `my-awesome-tool`, `My Awesome Tool`

### Project Slug
Auto-generated from project name. Used for:
- Directory names
- Import statements
- Package distribution name

### Package Name
The Python package name. By default, same as project slug.
- Must be a valid Python identifier
- Will be used in `import` statements

### Project Description
A one-line description of what your project does.
- Appears in `pyproject.toml`
- Shown in CLI help text
- Used in README

### Author Name & Email
Your contact information.
- Added to `pyproject.toml`
- Appears in package metadata

### CLI Framework

#### Click
- More traditional, decorator-based API
- Widely used in the Python ecosystem
- Good for complex CLI applications
- Better for nested command groups

**Choose Click if:**
- You prefer explicit control over CLI behavior
- You're building a complex CLI with many subcommands
- You want maximum flexibility in command configuration

#### Typer
- Modern, type-hint based API
- Built on top of Click
- Automatic help text generation from type hints
- Better IDE support with type checking

**Choose Typer if:**
- You prefer type hints and modern Python features
- You want cleaner, more readable code
- You value strong IDE support and autocompletion
- You're building a simpler CLI or prefer less boilerplate

### Python Version
Minimum Python version required by your project.
- Affects `requires-python` in `pyproject.toml`
- Determines available language features
- Sets tool configuration (black, ruff)

## Project Structure Details

### src-layout
This template uses the "src-layout" which is a Python packaging best practice:
- Prevents accidentally importing from the source directory
- Ensures tests run against the installed package
- Clearer separation between source and other files

### pyproject.toml
Modern Python projects use `pyproject.toml` for:
- Build system configuration
- Project metadata
- Tool configuration (pytest, black, ruff)
- Dependency management

### Entry Points
The template configures entry points so your CLI is available as a command:
```toml
[project.scripts]
my_tool = "my_tool.cli:main"
```

After installation, users can run `my_tool` directly from the command line.

## Customizing the Template

### Adding New Commands

#### For Click:
```python
@main.command()
@click.option("--option", "-o", help="An option")
def new_command(option: str):
    """Description of the command"""
    # Your logic here
```

#### For Typer:
```python
@app.command()
def new_command(
    option: str = typer.Option(None, "--option", "-o", help="An option")
):
    """Description of the command"""
    # Your logic here
```

### Adding Dependencies

Edit `pyproject.toml`:
```toml
dependencies = [
    "click>=8.0.0",  # or typer>=0.9.0
    "requests>=2.28.0",  # Add new dependencies here
]
```

### Adding Development Tools

Add to the `dev` optional dependencies:
```toml
[project.optional-dependencies]
dev = [
    "pytest>=7.0.0",
    "pytest-cov>=4.0.0",
    "black>=23.0.0",
    "ruff>=0.1.0",
    "mypy>=1.0.0",  # Add new dev tools here
]
```

## Best Practices

### Separation of Concerns
- Keep CLI code in `cli.py` (parsing arguments, handling I/O)
- Keep business logic in `logic.py` (actual functionality)
- This makes testing easier and code more reusable

### Testing
- Test business logic independently in `test_logic.py`
- Test CLI behavior with the testing utilities provided by Click/Typer
- Aim for high test coverage

### Documentation
- Use docstrings for all functions
- Keep README.md up to date
- Document complex behavior or edge cases

### Type Hints
- Add type hints to function signatures
- Helps with IDE support and catches bugs early
- Consider adding mypy for static type checking

## Troubleshooting

### Import Errors
If you get import errors after installation:
```bash
# Reinstall in editable mode
pip install -e .
```

### Tests Not Found
Ensure pytest is installed:
```bash
pip install -e ".[dev]"
```

### Command Not Available
After installation, you may need to:
```bash
# Refresh your shell's PATH
hash -r  # bash/zsh
rehash   # fish
```

## Advanced Usage

### Pre-commit Hooks
Consider adding pre-commit for automatic code formatting:
```bash
pip install pre-commit
# Create .pre-commit-config.yaml with black, ruff, etc.
pre-commit install
```

### Continuous Integration
Add GitHub Actions or other CI to:
- Run tests on multiple Python versions
- Check code formatting
- Verify type hints
- Build and publish releases

### Distribution
When ready to share your project:
```bash
# Build distributions
python -m build

# Upload to PyPI
python -m twine upload dist/*
```

## Resources

- [Click Documentation](https://click.palletsprojects.com/)
- [Typer Documentation](https://typer.tiangolo.com/)
- [Python Packaging Guide](https://packaging.python.org/)
- [Copier Documentation](https://copier.readthedocs.io/)
