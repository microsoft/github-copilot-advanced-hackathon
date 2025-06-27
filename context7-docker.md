
## Using Docker to run Context7

If you prefer to run the MCP server in a Docker container:

1. **Build the Docker Image:**

   First, create a `Dockerfile` in the project root (or anywhere you prefer):

   <details>
   <summary>Click to see Dockerfile content</summary>

   ```Dockerfile
   FROM node:18-alpine

   WORKDIR /app

   # Install the latest version globally
   RUN npm install -g @upstash/context7-mcp

   # Expose default port
   EXPOSE 3000

   # Default command to run the server
   CMD ["context7-mcp", "--transport", "http", "--port", "3000"]
   ```

   </details>

   Then, build the image using a tag (e.g., `context7-mcp`). **Make sure Docker Desktop (or the Docker daemon, or Podman) is running.** Run the following command in the same directory where you saved the `Dockerfile`:

   ```bash
   docker build -t context7-mcp .
   ```

   <details>
   <summary> For Podman users</summary>

   All of these commands should work just fine with Podman. Just replace `docker` with `podman`, and the rest of the instructions should be the same!
   </details>

1. Run the Context7 Container locally and expose the port:

    `docker run -d -p 127.0.0.1:3000:3000 --name context7 --restart=unless-stopped context7-mcp`

    This will run the container in the background, and expose port 3000 to your localhost only. Thus preventing outside traffic from accessing the container. The container should stay running in the background unless you stop it. This allows you to reuse the MCP server across multiple projects. If you need, change the first :3000 to an open port you want to use locally for the server. Make sure you make note of it for the next step.

1. **Configure Your MCP Client:**

   Update the `mcp.json` file in the `.vscode` folder of the repo

   _Example changes:_

   ```json
   {
     "mcpServers": {
       "Сontext7": {
         "type": "http",
         "url": "http://localhost:3000"
       }
     }
   }
   ```
