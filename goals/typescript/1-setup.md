## 🚀 Setting up Spec-Kit in your project

[Spec-Kit](https://github.com/github/spec-kit) brings Spec-Driven Development to your workflow, giving GitHub Copilot structured context through specifications, implementation plans, and task breakdowns — all version-controlled alongside your code.

## 📋 Prerequisites

- [Python UV](https://docs.astral.sh/uv/) — required to install Spec-Kit
- **Node.js 16+** (for MCP tools and Angular)
- **IDE** with GitHub Copilot[^1]
- **Git** for version control

## 🛠️ Installation & Setup

### Step 1: Install the Specify CLI

Install Spec-Kit once and use it across all your projects. Pin to the latest stable release for reproducibility:

#### Windows (PowerShell)
```powershell
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@v0.8.7
```

#### macOS / Linux (Bash)
```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@v0.8.7
```

Verify the installation:

```bash
specify version
```

> [!TIP]
> Don't have `uv`? Install it first: https://docs.astral.sh/uv/getting-started/installation/

### Step 2 (optional): Change the MCP Configuration

By default, we utilize the local MCP tools for caching and speed. However, if you don't have NodeJS installed, and do not wish to use NodeJS, you can instead utilize docker versions of each tool. To build and run the Docker version of the the tools, you will need to see the documentation for each to setup the docker config:

See the [Context7 Docker Readme](../../context7-docker.md) for instructions on how to use Docker to host Context7 locally.

See the [Playwright MCP Readme](https://github.com/microsoft/playwright-mcp) for details on advanced configuration and docker support for Playwright.

See the [Sequential Thinking MCP Readme](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking) for details on how to configure it using docker.

See the [Memory MCP Readme](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) for details on how to configure it using Docker

> [!IMPORTANT] 
> If you intend to do this, please do this before coming to the workshop, and ensure they are setup and configured. This can take time to setup and troubleshoot, so be prepared. Our recommendation is to use the NodeJS versions of the tools.

### Step 3: Clone the ngLibrary Repository

You'll be building this challenge using the ngLibrary demo repository. Clone it to an easy-to-access location on your machine.

#### PowerShell
```powershell
git clone https://github.com/mrWh1te/ngLibrary.git C:\github\ngLibrary
```

#### Bash
```bash
git clone https://github.com/mrWh1te/ngLibrary.git ~/github/ngLibrary
```

### Step 4: Initialize Spec-Kit in the ngLibrary Repository

Navigate into the cloned repository and initialize Spec-Kit with the GitHub Copilot integration:

#### PowerShell
```powershell
cd C:\github\ngLibrary
specify init --here --integration copilot
```

#### Bash
```bash
cd ~/github/ngLibrary
specify init --here --integration copilot
```

This creates a `.specify/` folder containing templates, scripts, and memory files that power the Spec-Driven workflow.

> [!NOTE]
> Run `specify check` after initialization to verify all prerequisites are detected correctly.

### Step 5: Establish Project Principles

Open the ngLibrary project in VS Code.

Run the `/speckit.constitution` prompt in Copilot Agent Mode to analyze your workspace and generate the project governance document that guides all subsequent spec-driven work.

```text
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements. Include governance for how these principles should guide technical decisions and implementation choices.
```

### Step 6: Verify Spec-Kit Setup Is Completed

1. Answer any questions that Copilot prompts you with, and wait for it to complete.
2. Confirm that `.github/copilot-instructions.md` has been created (or updated).
3. Confirm the `.specify/` folder contains the following structure:

```text
└── .specify
    ├── memory
    │    └── constitution.md
    ├── scripts
    │    ├── check-prerequisites.sh
    │    └── common.sh
    ├── specs
    └── templates
        ├── plan-template.md
        ├── spec-template.md
        └── tasks-template.md
```

4. Review `constitution.md` and the generated `copilot-instructions.md` for accuracy. Correct any mistakes you notice.

### Step 7: Follow the README to Run ngLibrary Locally

Follow the instructions in the `README.md` at the root of the ngLibrary repository to set up the application locally. Ensure that you can:
- Reach the application in a browser
- Search the book catalog
- Check out a book

## Next challenge

Now that you've set up Spec-Kit and established project principles, it's time to [write your first spec!](./2-requirements.md)

[^1]: _VS Code is the recommended IDE for this TypeScript track._
