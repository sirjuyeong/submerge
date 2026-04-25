# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Submerge** is a Godot 4.6 game project using GDScript. It uses the Jolt Physics engine for 3D physics and Forward Plus rendering (D3D12 on Windows).

## Running the Project

Requires Godot 4.6 installed and available on `PATH` as `godot`.

```bash
# Open project in the Godot editor
godot --path /path/to/submerge

# Run the project headlessly (e.g., for a specific scene)
godot --path /path/to/submerge --scene player.tscn

# Export a release build (requires export presets configured in editor)
godot --path /path/to/submerge --export-release <preset-name>
```

No test framework or linter is configured yet. Godot's built-in script analysis (Project > Tools > Check Script) is the primary static analysis tool.

## Project Structure

The project is in early development. The expected Godot convention for organizing files as it grows:

```
/scenes/     # .tscn scene files
/scripts/    # .gd GDScript files
/assets/     # textures, audio, models
/ui/         # UI scenes and themes
```

Currently tracked files:
- `project.godot` — project configuration (Godot 4.6, Jolt Physics, Forward Plus)
- `player.tscn` — root player scene (`CharacterBody2D` named `player`)
- `icon.svg` — application icon

The `.godot/` directory (Godot's cache/import cache) and `.export_presets.cfg` are gitignored.

## Key Configuration

- **Physics engine:** Jolt Physics 3D (set in `project.godot`, overrides the default Godot Physics)
- **Renderer:** Forward Plus (desktop-quality rendering pipeline); Windows uses D3D12
- **GDScript:** Godot's dynamically-typed scripting language; scripts attach to scene nodes via the `script` property in `.tscn` files

## GDScript Conventions

Godot uses `snake_case` for variables, functions, and file names. Scene nodes follow `PascalCase` for node type names and `snake_case` for node names in the scene tree. Signals are declared with `signal` and connected in `_ready()` or via the editor.

CharacterBody2D nodes (like `player`) use `move_and_slide()` for physics-based movement, with velocity managed through the built-in `velocity` property.
