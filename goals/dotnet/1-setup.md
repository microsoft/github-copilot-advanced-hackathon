## 🚀 Setting up the AI Assisted Coding Framework in your project

This framework integrates two powerful MCP (Model Context Protocol) servers to supercharge your development workflow:

- **Context7 MCP**: Provides live documentation and code snippet retrieval for authoritative technical references
- **ConPort MCP**: Delivers persistent project memory, decision tracking, and knowledge graph capabilities

Together, they transform GitHub Copilot into an intelligent development assistant that remembers project context, tracks architectural decisions, and maintains comprehensive project knowledge across sessions.

## 📋 Prerequisites

- **Docker** or **Podman** (for ConPort MCP)
- **Node.js 16+** (for Context7 MCP server) - Optional, see step 2 below
- **VS Code** with GitHub Copilot extension
- **Git** for version control

## 🛠️ Installation & Setup

### Step 1: Clone and Copy Framework Files
#### Windows Terminal:
```powershell
# Clone this repository
git clone https://github.com/ChrisMcKee1/AI-Assisted-Coding.git
cd AI-Assisted-Coding

# Copy all framework files to your project's root directory
# Replace 'your-project-path' with the actual path to your project
robocopy . "C:\path\to\your-project" /E /XD .git
```

#### Linux / OSX Terminal:
```bash
git clone https://github.com/ChrisMcKee1/AI-Assisted-Coding.git
cd AI-Assisted-Coding

# Copy all framework files to your project's root directory
# Replace '/path/to/your-project' with the actual path to your project
rsync -av --exclude='.git' . /path/to/your-project/
```

### Step 2 (optional): Change the MCP Configuration

By default, we utilize the local Contex7 MCP server for caching and speed. However, if you don't have NodeJS installed, and do not wish to use NodeJS, you can instead utilize iether the public Context7 MCP server, or build and run the Docker version of the Context7 MCP tool. The `.vscode/mcp.json` file has commented out configuration options for these two paths.

See the [Context7 Docker Readme](../../context7-docker.md) for instructions on how to use Docker to host Context7 locally.

Also, we are using Docker for hosting the Context Portal MCP server. We recommend you pull the image locally before you start up VS Code. To pull the image:

`docker pull seiggy/context-portal-mcp:0.2.18`

If you are using Podman, replace `docker` with `podman` in both the command, and in the `mcp.json` file. If you do not have Docker installed, you can run the Context Portal MCP server locally using Python and UV. For further details on how to use the ConPort MCP server with Python, see the [Context Portal Python Readme](../../conportal-python.md).

### Step 3: Open Project in VS Code

```powershell
# Open your project in VS Code
code .
```
### Step 4: Update Your Project Brief

Before proceeding, overwrite the `projectBrief.md` in your project root that you copied from the AI-Assisted-Coding repository, with the `projectBrief.md` file we provided in this repository.

### Step 5: Verify GitHub Copilot Integration

1. Ensure GitHub Copilot extension is installed and activated
2. The framework will automatically detect the `copilot-instructions.md` file


### Step 6: Initialize ConPort MCP

After verifying Copilot integration, initialize the ConPort MCP memory system:

1. In the Copilot chat or comments, type:  
    ```
    Initialize ConPort
    ```
1. Follow the prompts to complete setup.  
    This step creates the persistent memory database and loads your project context before you start coding.

### Step 7: Have the AI conduct Architecture Review

Have Copilot Create an Architecture Review of the repo. Take a look at the `README.md` in the AI Assisted Coding framework for help on how to conduct the Architecture review. When it completes, you should end up with a new folder named `architectureDiagrams` that contains 5 ore more markdown files with charts, documentation, and more about the eShop Application! Make sure you pass the #codebase token in your command, so that VS Code will give the AI access to the codebase for the context!

## Next challenge

Now that you've setup the AI to be able to better understand and work within your repository, it's time to [understand how to write requirements!](./2-requirements.md)