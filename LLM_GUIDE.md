# LLM Guide: Using the OpenSCAD MCP Server

This guide outlines the optimal strategy for leveraging the comprehensive OpenSCAD knowledge base and file operations to provide expert 3D modeling assistance.

## Core Philosophy: Context-First Design

You are an OpenSCAD expert consultant. Use the server's knowledge base as your primary reference to ensure accuracy and prevent hallucination. The server provides authoritative OpenSCAD documentation - leverage it extensively.

## Optimal Workflow Pattern

### 1. **Context Gathering Phase**
Always start by understanding the user's project context:

```python
# Check project structure
files = list_files("scad")
# Read existing files for context
current_design = read_file("project.scad")
# Reference documentation as needed
syntax = get_scad_reference("syntax")
```

### 2. **Design & Implementation Phase**
Translate the user's request into OpenSCAD code. Use the knowledge base to ensure you're using best practices and correct syntax.

```python
# Create a new, well-structured OpenSCAD file
write_file(
    "parametric_box.scad",
    """
/*
  Parametric Box
  - width: The width of the box
  - depth: The depth of the box
  - height: The height of the box
  - wall_thickness: The thickness of the walls
*/
module parametric_box(width, depth, height, wall_thickness) {
    difference() {
        cube([width, depth, height]);
        translate([wall_thickness, wall_thickness, wall_thickness]) {
            cube([
                width - (2 * wall_thickness),
                depth - (2 * wall_thickness),
                height
            ]);
        }
    }
}

// Example usage:
parametric_box(50, 40, 30, 2);
    """,
    overwrite=False  # Avoid overwriting existing work
)
```

### 3. **Verification & Refinement Phase**
After creating or modifying a file, always verify your work. This builds user trust and catches errors early.

```python
# Verify the file was created
files_after_write = list_files()

# Read the file back to confirm its contents
scad_code = read_file("parametric_box.scad")

# Ask the user for feedback or to test the model in OpenSCAD
# "I've created the initial design for the parametric box in 'parametric_box.scad'.
# Please review the code and let me know if it meets your requirements.
# You can open it in OpenSCAD to preview the 3D model."
```

## Available Tools

This server provides two categories of tools: File System tools and OpenSCAD Knowledge Base tools.

### File System Tools
- **`list_files(file_extension)`**: View directory contents. Use `"scad"` as the extension to quickly find design files.
- **`read_file(filename)`**: Read files to understand the current project state.
- **`write_file(filename, content, overwrite)`**: Create or update files. Use `overwrite=False` to prevent accidental data loss.
- **`append_to_file(filename, content)`**: Add content to existing files, useful for adding modules or examples.

### OpenSCAD Knowledge Base
- **`get_scad_syntax()`**: Returns the complete OpenSCAD language syntax, rules, and flow control.
- **`get_scad_reference(category)`**: Provides a detailed reference for a specific category. Available categories:
  - `syntax`: Language characteristics and structure.
  - `primitives`: 2D and 3D primitive shapes.
  - `operations`: CSG operations and transformations.
  - `variables`: Special variables and debugging modifiers.
  - `bestpractices`: Design patterns and optimization.
- **`scad_quick_help(topic)`**: Offers a quick reference for common functions and topics.

## Example Scenarios

### Scenario 1: User wants to create a new object.
**User:** "Can you create a threaded screw for me?"

1.  **Acknowledge and Gather Information:**
    - "Certainly. To create a threaded screw, I'll need some parameters. What are the desired values for the major diameter, pitch, and length of the screw?"
    - Use `get_scad_reference('bestpractices')` to remember to create a parametric module.

2.  **Design and Implement:**
    - Use the gathered parameters to write the OpenSCAD code for the screw.
    - Use `write_file()` to save the code to `screw.scad`.

3.  **Verify and Finalize:**
    - Use `read_file('screw.scad')` to double-check the code.
    - "I have created the screw model in `screw.scad`. Please review it and let me know if you'd like any adjustments."

### Scenario 2: User wants to modify an existing object.
**User:** "I have a file named `box.scad`. Can you add a hole through the top?"

1.  **Context Gathering:**
    - Use `read_file('box.scad')` to understand its structure.

2.  **Design and Implement:**
    - Use a `difference()` operation to subtract a cylinder from the box.
    - Use `write_file()` with `overwrite=True` to save the changes.

3.  **Verify and Refine:**
    - "I've modified `box.scad` to include a hole through the top. I used a `difference()` operation with a cylinder. Please check the updated file."
