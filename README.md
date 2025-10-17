# OpenSCAD MCP Server

A comprehensive Model Context Protocol (MCP) server that provides deep OpenSCAD knowledge and safe file management for 3D modeling workflows.

## Purpose

This server acts as an expert OpenSCAD reference and project assistant, providing AI assistants with authoritative OpenSCAD documentation and safe file operations to accelerate 3D design workflows.

## Features

### Comprehensive OpenSCAD Knowledge
- **`get_scad_syntax()`** - Complete language syntax, rules, and flow control
- **`get_scad_reference(category)`** - Detailed reference by category:
  - `syntax` - Language characteristics and structure
  - `primitives` - 2D and 3D primitive shapes
  - `operations` - CSG operations and transformations
  - `variables` - Special variables and debugging modifiers
  - `bestpractices` - Design patterns and optimization
- **`scad_quick_help(topic)`** - Quick function reference for common operations

## Installation

### Prerequisites
- Docker installed and running.

### Step 1: Save the Files
Create a new directory for the project and save the following files in it:
- `Dockerfile`
- `requirements.txt`
- `openscad_server.py`
- `readme.md`
- `LLM_GUIDE.md`

### Step 2: Build Docker Image
```bash
docker build -t openscad-mcp-server .
```

### Step 3: Create Custom Catalog for Claude Desktop

1.  Create the catalogs directory if it doesn't exist:
    ```bash
    mkdir -p ~/.docker/mcp/catalogs
    ```

2.  Create or edit `custom.yaml`:
    ```bash
    nano ~/.docker/mcp/catalogs/custom.yaml
    ```

3.  Add this entry to `custom.yaml`:
    ```yaml
    version: 2
    name: custom
    displayName: Custom MCP Servers
    registry:
      openscad:
        description: "Comprehensive OpenSCAD knowledge base and file management for 3D modeling"
        title: "OpenSCAD Assistant"
        type: server
        dateAdded: "2025-01-15T00:00:00Z"
        image: openscad-mcp-server:latest
        ref: ""
        readme: ""
        toolsUrl: ""
        source: ""
        upstream: ""
        icon: ""
        tools:
          - name: get_scad_syntax
          - name: get_scad_reference
          - name: scad_quick_help
        secrets: []
        metadata:
          category: productivity
          tags:
            - openscad
            - 3d-modeling
            - cad
            - 3d-printing
          license: MIT
          owner: local
    ```

### Step 4: Update Registry for Claude Desktop

1.  Edit the registry file:
    ```bash
    nano ~/.docker/mcp/registry.yaml
    ```

2.  Add this entry under the existing `registry:` key:
    ```yaml
    registry:
      # ... existing servers ...
      openscad:
        ref: ""
    ```

### Step 5: Configure Claude Desktop

1.  Find your Claude Desktop config file:
    - **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
    - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
    - **Linux:** `~/.config/Claude/claude_desktop_config.json`

2.  Edit the file and add your custom catalog to the `args` array:
    ```json
    {
      "mcpServers": {
        "mcp-toolkit-gateway": {
          "command": "docker",
          "args": [
            "run",
            "-i",
            "--rm",
            "-v", "/var/run/docker.sock:/var/run/docker.sock",
            "-v", "C:/Users/your_username/.docker/mcp:/mcp",
            "docker/mcp-gateway",
            "--catalog=/mcp/catalogs/docker-mcp.yaml",
            "--catalog=/mcp/catalogs/custom.yaml",
            "--config=/mcp/config.yaml",
            "--registry=/mcp/registry.yaml",
            "--tools-config=/mcp/tools.yaml",
            "--transport=stdio"
          ]
        }
      }
    }
    ```
    **Important:** Replace `/Users/your_username` with your actual home directory path.

### Step 6: Restart Claude Desktop
1.  Quit Claude Desktop completely.
2.  Start Claude Desktop again.
3.  Your OpenSCAD tools should now be available.

### Step 7: Test Your Server
```bash
docker mcp server list
```

## Example Queries

Once installed, you can ask Claude:

- "Show me the OpenSCAD syntax rules"
- "What functions are available for transformations?"
- "Create a new SCAD file for a parametric box"
- "Read my existing project.scad and suggest improvements"
- "How do I use the hull() operation?"

This server transforms AI assistants into expert OpenSCAD consultants with instant access to comprehensive 3D modeling knowledge.
