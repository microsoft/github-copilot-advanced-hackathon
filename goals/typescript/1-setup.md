## 🚀 Setting up the AI Assisted Coding Framework in your project

This framework integrates two powerful MCP (Model Context Protocol) servers to supercharge your development workflow:

- **Context7 MCP**: Provides live documentation and code snippet retrieval for authoritative technical references
- **Memory MCP**: Delivers persistent project memory, decision tracking, and knowledge graph capabilities

Together, they transform GitHub Copilot into an intelligent development assistant that remembers project context, tracks architectural decisions, and maintains comprehensive project knowledge across sessions.

## 📋 Prerequisites

- **Node.js 16+** (for MCP tools)
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

By default, we utilize the local MCP tools for caching and speed. However, if you don't have NodeJS installed, and do not wish to use NodeJS, you can instead utilize docker versions of each tool. To build and run the Docker version of the the tools, you will need to see the documentation for each to setup the docker config:

See the [Context7 Docker Readme](../../context7-docker.md) for instructions on how to use Docker to host Context7 locally.

See the [Playwright MCP Readme](https://github.com/microsoft/playwright-mcp) for details on advanced configuration and docker support for Playwright.

See the [Sequential Thinking MCP Readme](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking) for details on how to configure it using docker.

See the [Memory MCP Readme](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) for details on how to configure it using Docker

### Step 3: Open Project in VS Code

```powershell
# Open your project in VS Code
code .
```

### Step 4: Run the Analyze Workflow

Run the `/analyze-product` prompt to analyze your workspace and generate the documents that help the spec-driven development workflow operate smoothly.

### Step 5: Verify GitHub Copilot Integration

1. Ensure GitHub Copilot extension is installed and activated
2. The framework will automatically generate the `copilot-instructions.md` file
3. The framework should also generate a series of files in a folder named `.docs`


### Step 8: Have the AI conduct Architecture Review

Have Copilot Create an Architecture Review of the repo. Take a look at the `README.md` in the AI Assisted Coding framework for help on how to conduct the Architecture review. When it completes, you should end up with a new folder named `architectureDiagrams` that contains 5 ore more markdown files with charts, documentation, and more about the eShop Application! Make sure you pass the #codebase token in your command, so that VS Code will give the AI access to the codebase for the context!

## Next challenge

Now that you've setup the AI to be able to better understand and work within your repository, it's time to [understand how to write requirements!](./2-requirements.md)