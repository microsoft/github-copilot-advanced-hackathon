## 🚀 Setting up the AI Assisted Coding Framework in your project

This framework integrates several powerful MCP (Model Context Protocol) tools to supercharge your development workflow:

- **Context7 MCP**: Provides live documentation and code snippet retrieval for authoritative technical references
- **Memory MCP**: Delivers persistent project memory, decision tracking, and knowledge graph capabilities
- **Sequential Thinking MCP**: Assists the LLM with ordering tasks, and breaking down complex ideas
- **Microsoft.Learn MCP**: Give your LLM access to the entire Microsoft Learn knowledgebase!

Together, they transform GitHub Copilot into an intelligent development assistant that remembers project context, tracks architectural decisions, and maintains comprehensive project knowledge across sessions.

## 📋 Prerequisites

- **Node.js 16+** (for MCP tools)
- **IDE** with GitHub Copilot[^1]
- **Docker** is recommended, or you can use the devcontainer.
- **Git** for version control

## 🛠️ Installation & Setup

### Step 1: Clone The Framework Repository
#### Windows Terminal:
```powershell
# Clone this repository
git clone https://github.com/ChrisMcKee1/AI-Assisted-Coding.git
```

We will use the files in this repository once you've setup your local workspace. Keep them somewhere easy to access, we recommend a folder such as `C:\github\` or `~/github` on Linux & OSX.

### Step 2 (optional): Change the MCP Configuration

By default, we utilize the local MCP tools for caching and speed. However, if you don't have NodeJS installed, and do not wish to use NodeJS, you can instead utilize docker versions of each tool. To build and run the Docker version of the the tools, you will need to see the documentation for each to setup the docker config:

See the [Context7 Docker Readme](../../context7-docker.md) for instructions on how to use Docker to host Context7 locally.

See the [Playwright MCP Readme](https://github.com/microsoft/playwright-mcp) for details on advanced configuration and docker support for Playwright.

See the [Sequential Thinking MCP Readme](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking) for details on how to configure it using docker.

See the [Memory MCP Readme](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) for details on how to configure it using Docker

> [!IMPORTANT] 
> If you intend to do this, please do this before coming to the workshop, and ensure they are setup and configured. This can take time to setup and troubleshoot, so be prepared. Our recommendation is to use the NodeJS versions of the tools.

### Step 3: Clone the ngLibrary Repository

You'll be building this challenge using the ngLibrary demo repository. Clone the [ngLibrary](https://github.com/mrWh1te/ngLibrary/) Repository from github to an easy to access location on your machine.

### Step 4: Copy the Framework to the ngLibrary repository

Copy the `.github` and `.vscode` folders from the AI-Assisted-Coding repository to the root of your ngLibrary repository. An example script below assumes you cloned both repositories to the root of `C:\github` or `~/github` respectively.

#### Powershell
```powershell
cd c:\github\AI-Assisted-Coding
robocopy . "C:\github\ngLibrary" /E /XD .git
```

#### Bash
```bash
cd ~/github
rsync -av --exclude='.git' . ~/github/ngLibrary
```


### Step 5: Run the Analyze Workflow

Open the ngLibrary Solution using VS Code or your preferrred IDE.

Run the `/analyze-product` prompt in Copilot Agent Mode to analyze your woskpace and generate the documents that help the spec-driven development workflow operate smoothly.

### Step 6: Verify Framework setup is completed

1. Answer any questions that the AI prompts you with, and wait for it to complete.
2. The framework will automatically generate the `copilot-instructions.md` file
3. The framework should also generate a series of files in a folder named `.docs`
4. Review these documents for accuracy, and fix any problems you see.


### Step 7: Follow the instructions from the `README.md` file to run ngLibrary locally

Follow the instructions in the `README.md` file at the base of the ngLibrary Repository to setup the application locally. You'll want to ensure that you can reach the application, search inventory, and manage suppliers.

## Next challenge

Now that you've setup the AI to be able to better understand and work within your repository, it's time to [understand how to write requirements!](./2-requirements.md)