# NavFileToolkit

Desktop tool for working with .sct/.sct2 and .ese sector files used in ATC simulation. Parses, visualizes, and lets you edit facility data. Built with Qt6 and C++.

## What it does

Opens sector files and displays everything on an interactive dark-themed map: VORs, NDBs, fixes, airports, runways, GEO coastlines, ARTCC boundaries, SIDs, STARs, and regions. You can click on anything to inspect it, toggle layers on and off, filter by groups, and edit the raw file directly.

The main thing that sets it apart is the sector ownership system. You check which positions are "online," and the app shows you coloured coverage overlays based on the ownership hierarchy defined in the ESE file. You can click any sector on the map to open its hierarchy, drag positions around to change the cascade order, and watch the map update in real time. When multiple sectors overlap at the same point (altitude slices, adjacent sectors), it gives you a picker so you can select exactly which one to edit.

There's also a drawing toolset for adding new GEO lines, ARTCC boundaries, regions, and sectorlines directly on the map with snap-to-navaid support. Everything gets converted to proper SCT/ESE syntax.

## Features

**File handling**
- Reads .sct, .sct2, .ese, .asr files
- Open an entire facility folder and it auto-discovers everything
- Raw file editor with line numbers, switch between loaded files
- Save changes back to the SCT file

**Map**
- Pan with middle mouse, zoom with scroll wheel
- Toggle layers individually (GEO, ARTCC, ARTCC High/Low, SIDs, STARs, etc.)
- Group checkboxes to show/hide specific GEO and ARTCC groups
- Double-click a group name to jump to that spot in the raw file
- Click to inspect any element, shift-click for multi-select

**Sector ownership**
- Check positions as online to see coverage overlays
- Altitude filter (FL min/max) to isolate vertical slices
- Click a sector on the map to open the hierarchy editor
- Drag-and-drop or up/down buttons to reorder the ownership chain
- Map updates live as you make changes
- "Apply to All Similar" to bulk-edit sectors with the same primary owner
- Picks between overlapping sectors when you click a shared area

**Drawing**
- GEO lines, ARTCC boundaries, filled regions, sectorlines
- Pick an existing group or name a new one
- Snaps to VORs, NDBs, fixes, airports, runway ends
- Esc to undo, double-click or Enter to finish, right-click to cancel

**Other tools**
- Colour code manager with BGR picker
- Coordinate converter (DMS/decimal) with distance/bearing calc
- Tag file editor for CANscope .tag files with visual preview
- PDF sector coverage reports with per-position maps and fix markers
- Sortable data tables for all navaid types

## Controls

| Input | What it does |
|-------|-------------|
| Scroll wheel | Zoom |
| Middle mouse drag | Pan |
| Left click | Inspect element / open sector hierarchy |
| Shift + click | Multi-select |
| Ctrl+O | Open SCT file |
| Ctrl+Shift+F | Open facility folder |
| Ctrl+S | Save |
| Ctrl+Shift+S | Save As |
| F5 | Refresh map from raw editor |
| Esc | Undo last draw vertex |
| Enter / double-click | Finish drawing |
| Right-click | Cancel drawing |

## How ownership works

The ESE file defines sectors with an ownership chain (list of position IDs in priority order). When you check positions as "online" in the sidebar, the app walks each sector's chain and assigns it to the first online position it finds. If that position goes offline, the sector falls through to the next one in the chain.

The hierarchy editor lets you reorder this chain per-sector. Green entries are currently online, grey ones are offline. The "Active owner" label shows you who currently wins the sector based on what's checked.

## File formats

**SCT/SCT2** contains navaids, airports, runways, geographic lines, boundaries, procedures, regions, and colour definitions. Coordinates are in DMS format (N044.52.30.000).

**ESE** extends the SCT with controller positions, sectorline definitions (borders between sectors), and sector ownership hierarchies (which position controls which airspace, with fallback chains).

**ASR** files define display settings: which elements are visible, viewport bounds, rotation.

## Version & License

0.5.2

MIT License

Copyright (c) 2026 Keegan McKim / Amk290

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
