# Context Portal MCP in Python

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python:** Version 3.8 or higher is recommended.
  - [Download Python](https://www.python.org/downloads/)
  - Ensure Python is added to your system's PATH during installation (especially on Windows).
- **uv:** (Highly Recommended) A fast Python environment and package manager. Using `uv` significantly simplifies virtual environment creation and dependency installation.
  - [Install uv](https://github.com/astral-sh/uv#installation)

## Installation and Configuration

The recommended way to install and run ConPort is by using `uvx` to execute the package directly from PyPI. This method avoids the need to manually create and manage virtual environments.


### `uvx` Configuration

In the `mcp.json` file of your `.vscode` folder, change the conport configuration to the following:

```json
{
    ...
    "conport": {
        "command": "uvx",
        "type": "stdio",
        "args": [
            "--from",
            "context-portal-mcp",
            "conport-mcp",
            "--mode",
            "stdio",
            "--workspace_id",
            "${workspaceFolder}",
            "--log-file",
            "./logs/conport.log",
            "--log-level",
            "INFO"
        ]
    }
    ...
}
```

- **`command`**: `uvx` handles the environment for you.
- **`args`**: Contains the arguments to run the ConPort server.
- `${workspaceFolder}`: This IDE variable is used to automatically provide the absolute path of the current project workspace.
- `--log-file`: Optional: Path to a file where server logs will be written. If not provided, logs are directed to `stderr` (console). Useful for persistent logging and debugging server behavior.
- `--log-level`: Optional: Sets the minimum logging level for the server. Valid choices are `DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`. Defaults to `INFO`. Set to `DEBUG` for verbose output during development or troubleshooting.

### Update the `copilot-instructions.md`

Finally, you'll need to update the copilot instructions file. We currently hardcode the Workspace Id for ConPort to be `/app/workspace` as that is the workspace we use within the Docker container to connect to your code. Since you are running the code locally, you will need to change this to `${workspaceFolder}`. So do a find-replace of `/app/workspace` and replace with `${workspaceFolder}`. This should allow VS Code to automatically send the correct workspace ID to your ConPort process.