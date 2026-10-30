# Puzzle Level Production Workbench

A sanitized public demo of a browser-based production tool for designing, generating, validating, and analyzing dense grid puzzle levels.

## What it demonstrates

- Visual grid-level editing with drag-and-drop placement
- JSON import/export
- Automatic level generation with difficulty and cascade targets
- Dependency-graph modeling and graph-first generation
- Solvability validation and reference-solution playback
- SHIFT safety analysis
- Cascade preview and event-chain analysis
- Production-quality scoring and duplicate/similarity detection
- Quality visualization, including release-potential and low-value-action diagnostics
- Mechanic composition using generic units, breakable blockers, dormant locks, push devices, paired locks, key/lock relationships, and teleport pairs

## Public-build sanitization

This repository is a portfolio-safe build. Project-specific names, original level data, internal document references, and theme-specific unit names have been removed or replaced with generic equivalents. The included demo level is generated locally by the tool and is not production content.

## Run locally

No build step is required.

1. Clone or download the repository.
2. Open `index.html` in a modern desktop browser.
3. Use the built-in demo or import your own JSON level data.

## Notes

This is a single-file prototype intended to demonstrate level-design tooling and workflow concepts. It is not packaged as a production game runtime.