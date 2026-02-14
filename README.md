# python-cli-template

A [Copier](https://copier.readthedocs.io/) template for creating Python CLI projects with your choice of [Click](https://click.palletsprojects.com/) or [Typer](https://typer.tiangolo.com/) framework.

📚 **[Read the detailed usage guide](USAGE.md)** for more information.

## Features

- Choice between Click or Typer CLI framework
- Modern Python project structure with `pyproject.toml`
- Source code in `src/` layout
- Pre-configured testing with pytest
- Code formatting with Black
- Linting with Ruff
- Example CLI commands and business logic
- Comprehensive test suite

## Prerequisites

Install Copier:

```bash
pip install copier
```

## Usage

Create a new project from this template:

```bash
copier copy gh:bengineerdavis/python-cli-template my-new-project
```

Or if you're working locally:

```bash
copier copy path/to/python-cli-template my-new-project
```

You'll be asked several questions:
- **Project name**: The name of your project (e.g., "my-tool")
- **Project slug**: Auto-generated from project name, used for directories and imports
- **Package name**: Auto-generated, the Python package name
- **Project description**: A short description of your project
- **Author name**: Your name
- **Author email**: Your email address
- **CLI framework**: Choose between `click` or `typer`
- **Python version**: Minimum Python version (3.8 to 3.12)

## Generated Project Structure

```
my_tool_project/
├── pyproject.toml         # Project metadata and dependencies
├── README.md              # Project documentation
├── .gitignore             # Files to exclude from Git
├── src/                   
│   └── my_tool/           # The actual package
│       ├── __init__.py    
│       ├── __main__.py    # Entry point for `python -m my_tool`
│       ├── cli.py         # CLI implementation
│       └── logic.py       # Business logic
└── tests/                 
    ├── __init__.py
    ├── test_cli.py        # CLI tests
    └── test_logic.py      # Logic tests
```

## Working with the Generated Project

### Installation

```bash
cd my-new-project
pip install -e .
```

For development with all dev dependencies:

```bash
pip install -e ".[dev]"
```

### Running the CLI

```bash
my-tool --help
my-tool hello --name "World"
my-tool process "data" --reverse
```

### Running Tests

```bash
pytest
```

### Code Formatting

```bash
black src/ tests/
```

### Linting

```bash
ruff check src/ tests/
```

## Example Commands

Both Click and Typer versions include these example commands:

- `hello`: Greets someone with optional uppercase flag
- `process`: Processes data with optional reverse flag

## License

MIT License
