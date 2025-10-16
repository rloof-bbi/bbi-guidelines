# Python

Python is a high-level programming language known for its readability and broad ecosystem. At BBI, we use Python primarily for backend development (e.g., with FastAPI), integrations, data processing, and automation tasks.

## Installation

1. Go to the [Python download page](https://www.python.org/downloads/) and select the latest stable version for Windows (e.g., Python 3.14.0 standalone installer).
2. Download and run the installer.
3. During installation, check the box "Add python.exe to PATH". You can use the default setup options for most cases.
4. After installation, verify your installation by running `python --version` in a terminal.
5. (Recommended) Install the package manager [uv](https://docs.astral.sh/uv/) with `pip install uv` for dependency management.

## Setting Up a New Project

1. Open VSCode and select the folder for your new project. It is recommended to name folders similar to our GitHub repositories, e.g., `customer-project-type` → `terstal-control-tower-backend`.
2. Open a terminal in VSCode (`Terminal` → `New Terminal`).
3. Run `uv init` to scaffold a new project. Add packages with `uv add <package_name>`.
4. Select the correct Python interpreter (`Ctrl+Shift+P` → `Python: Select Interpreter`) and choose the interpreter, usually inside the `.venv` folder of your project.

## Project Structure

After running `uv init`, a typical project structure looks like this:

```
.
├── app/                  # Main application package
│   └── ...
├── scripts/              # Utility scripts (e.g., evaluate_run.py)
│   └── ...
├── .env                  # Environment variables (see .env.sample)
├── .env.sample           # Template for the environment variables
├── .gitignore            # Files/folders to exclude from git, e.g. .env
├── .python-version       # Python version for the project
├── Dockerfile            # Containerizes the application
├── main.py               # Entry point for the application
├── pyproject.toml        # Project metadata and dependencies
├── README.md             # Project documentation
└── uv.lock               # Dependency lock file
```

## Guidelines

The guidelines below ensure that Python code is readable, maintainable, and consistent across all BBI projects.

-   Line Length, limit all lines to a maximum of 88 characters for readability.
-   Variable Naming:
    -   Use `snake_case` for variables and functions.
    -   Use `UPPER_CASE` for constants.
    -   Class names should use `CapWords` (PascalCase).
-   Always use [type hints](https://docs.python.org/3/library/typing.html) for function arguments and return values to improve code clarity and editor support.
-   Docstrings and Comments:

    -   Every function must have a docstring that describes its purpose.
    -   Start the docstring with `"""` on a new line, write the description, and close with `"""` on a new line.
    -   Example:

        ```python
        def add(a: int, b: int) -> int:
            """
            Add two integers and return the result.
            """
            return a + b
        ```

-   Use [Ruff](https://docs.astral.sh/ruff/) to automatically format and lint your code. This ensures consistency and catches common issues early.
-   Follow the [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html) for most conventions.
-   Always commit a `.env.sample` file with example environment variables for your project.

## VSCode Extensions & Settings

For a productive Python development environment, install these VSCode extensions:

-   Python (ms-python.python): Core Python support
-   Pylance (ms-python.vscode-pylance): Fast, feature-rich language server
-   Ruff (charliermarsh.ruff): Fast Python linter and formatter

Add the following to your `settings.json` for best results:

```jsonc
{
    "python.languageServer": "Pylance",
    "python.terminal.activateEnvironment": false,
    "python.analysis.typeCheckingMode": "basic",
    "python.analysis.diagnosticMode": "workspace",
    "[python]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "charliermarsh.ruff",
        "editor.codeActionsOnSave": {
            "source.fixAll": "explicit",
            "source.organizeImports": "explicit"
        }
    }
}
```

## Troubleshooting

-   If `python` is not recognized, ensure it is added to your PATH or restart your terminal.
