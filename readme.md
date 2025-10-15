# OpenSCAD MCP Server

A comprehensive Model Context Protocol (MCP) server that provides deep OpenSCAD knowledge and safe file management for 3D modeling workflows.

## Purpose

This server acts as an expert OpenSCAD reference and project assistant, providing AI assistants with authoritative OpenSCAD documentation and safe file operations to accelerate 3D design workflows.

## Features

### File System Tools
- **`list_files(file_extension)`** - View directory contents with OpenSCAD file highlighting
- **`read_file(filename)`** - Read files to understand current project state
- **`write_file(filename, content, overwrite)`** - Create or update files with safety checks
- **`append_to_file(filename, content)`** - Add content to existing files

### Comprehensive OpenSCAD Knowledge
- **`get_scad_syntax()`** - Complete language syntax, rules, and flow control
- **`get_scad_reference(category)`** - Detailed reference by category:
  - `syntax` - Language characteristics and structure
  - `primitives` - 2D and 3D primitive shapes
  - `operations` - CSG operations and transformations
  - `variables` - Special variables and debugging modifiers
  - `bestpractices` - Design patterns and optimization
- **`scad_quick_help(topic)`** - Quick function reference for common operations

## Knowledge Coverage

Based on comprehensive OpenSCAD documentation, this server provides:

### Language Fundamentals
- Variable assignment and scoping rules
- Module and function definitions
- Flow control (if/else, for loops, list comprehensions)
- Import directives (include vs use)

### Geometry Primitives
- 3D: cube, sphere, cylinder, polyhedron
- 2D: circle, square, polygon, text
- Extrusions: linear_extrude, rotate_extrude

### Operations & Transformations
- CSG: union, difference, intersection
- Geometric: translate, rotate, scale, mirror, resize
- Advanced: hull, minkowski, offset

### Special Features
- Resolution control: $fn, $fa, $fs
- Debugging modifiers: #, %, !, *
- Animation variables: $t
- Utility functions: echo, assert, children

## Strategic Usage

The server enables AI assistants to follow this optimal workflow:

1. **Orient** - Use `list_files()` to understand project structure
2. **Analyze** - Use `read_file()` to examine existing SCAD files
3. **Reference** - Access comprehensive documentation via `get_scad_reference()`
4. **Implement** - Generate OpenSCAD code using authoritative knowledge
5. **Modify** - Safely update files with proper validation

## Security

- Runs as non-root user in Docker container
- File operations include overwrite protection
- Input validation on all parameters
- No external network dependencies
- Comprehensive error handling

## Quick Start

```bash
# Build the image
docker build -t openscad-mcp-server .

# The server will be available through Claude Desktop MCP integration
```

Example Queries

· "Show me OpenSCAD syntax rules"
· "What transformation functions are available?"
· "How do I create a parameterized module?"
· "Explain the difference between union and difference"
· "What are the special variables for resolution control?"

This server transforms AI assistants into expert OpenSCAD consultants with instant access to comprehensive 3D modeling knowledge.
