# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FlowCode is an educational web app that teaches students how flowcharts map to Python code. It consists of two self-contained HTML files with no build system, bundler, or package manager.

## Architecture

- **`flowcode.html`** — The main interactive builder. A three-panel layout:
  - **Shape palette** (left): drag-and-drop flowchart shapes (Start/Stop, Process, Decision, Input, Output)
  - **SVG canvas** (center): renders flowchart nodes and arrows; supports pan/zoom, node selection, drag reordering
  - **Code panel** (right): uses CodeMirror 5 for a live Python editor that stays in sync with the flowchart (bidirectional: flowchart→code and code→flowchart modes)
- **`index.html`** — Step-by-step tutorial mode. A lesson picker loads predefined walkthroughs (sequence, selection, iteration) that progressively build a flowchart and its corresponding Python code with explanatory text.

Both files are fully self-contained single-file apps — all CSS is inlined in `<style>` tags, all JS is inlined in `<script>` tags. External dependencies (CodeMirror, Google Fonts) are loaded via CDN.

## Key Design Patterns

- **SVG rendering**: Flowchart nodes are rendered as SVG elements (`rect`, `polygon`, `ellipse`) inside an `<svg>` element. Arrows use SVG `<path>` with marker-end arrowheads.
- **Node model**: Nodes are stored in a JS array of objects with `{id, type, x, y, text, varName?, condType?}`. The canvas re-renders from this array on every change.
- **Lesson data** (index.html): Each lesson is a JS object with an array of `steps`, where each step defines `shapes`, `code` lines, and `explain` HTML. Steps are rendered progressively.
- **Layout constants**: Node dimensions and spacing are defined as constants (`NODE_W`, `NODE_H`, `DIAMOND_W`, `GAP_Y`, `CENTER_X`, etc.) at the top of each file's script section.
- **Color scheme**: CSS custom properties in `:root` define the full color palette. Shape types have dedicated color mappings in `SHAPE_COLORS`/`COL` objects.

## Development

No build step. Open either HTML file directly in a browser. To develop, edit the HTML files and refresh.
