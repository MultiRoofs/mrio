# Changelog

## 0.4.0 — 2026-10-09

### Added
- Welcome screen in the web app: what the tool does, a note that files are processed locally (not uploaded), and MultiRoofs/Interreg acknowledgement
- Large-file warning in the web app (over 20,000 objects) pointing users to the TUI/desktop version
- "Set CRS" dialog now shows the file's current EPSG code
- Attribute overview now explains the example value and the count/percentage shown
- Link to [cjval](https://github.com/cityjson/cjval) for the meaning of validation results

### Changed
- Renamed and reordered the operations in both the web app and the TUI for clarity; "Validate schema" is now "Validate file"
- Header in the web app shows `Uploaded file: <name>`
- Renamed the "CRS: set EPSG" button to "Set CRS"
- Save dialog uses `Tab` (instead of `f`) to toggle the output format
- Save default filename keeps the correct extension (`.city.json` / `.city.jsonl`) instead of repeating the input extension

### Fixed
- Web dialogs no longer re-run their operation on Cancel/Esc after a previous confirm (stale dialog `returnValue`)
- Web dialogs can no longer be dismissed by clicking outside them; use the buttons
- Renaming an attribute to an existing name is rejected instead of silently overwriting its values
- Attribute names are validated (letters, digits and `+ - _ . :` only)
- CSV import is now linear instead of O(rows × objects), fixing hangs/crashes on large files
- Imported CSV structure is validated (ID column, headers, duplicate or invalid attribute names)
- Validation dialog no longer shows a confusing "Warnings" title state
- Fixed a stray orange bar on the web page caused by the hidden large-file warning element

## 0.3.0 — 2026-07-23

### Added
- **Volume** operation — computes and adds per-object building volume attribute

### Changed
- Renamed project from `mrio2` to `mrio`
- Add a link to latest version of the MultiRoofs Extension



## 0.2.0 — 2026-06-04
### Added
- Workspace restructure: monorepo split into `mrio-core`, `mrio-cli`, `mrio-web` crates
- Web app (WASM) with drag-and-drop, operations panel, validation, and download
- **Roof total area** operation — computes and adds per-object roof area attribute
- **Set CRS EPSG** operation — changes the CRS EPSG code of the document
- **Validate schema** operation — validates against CityJSON schema via `cjval`
- **Validate with extensions** — fetches extension schemas and validates against them
- Extension schema loading during validation (native via ureq, WASM via browser fetch)
- GitHub CI deploy workflow for hosting the web app
- Version display on web app
- Warning dialog when saving overwrites an existing file

### Changed
- Operations restructured to return `OpReport` with summary, affected count, and error flag
- Roofer → MultiRoofs now also adds roof-total-area attribute
- Web app styling improvements with oat.ink UI framework
- TUI input dialog supports numeric entry for roof area operator parameters

### Fixed
- Cursor position preserved when writing in TUI save dialog
- Removed duplicate "Validate schema" entry from operations list


## 0.1.0 — 2026-05-04

Initial release.

### Added
- Read both CityJSON (`.city.json`) and CityJSONSeq (`.city.jsonl`) — auto-detected by extension
- Write both formats with conversion between them (collapse/expand with vertex remapping)
- TUI with two panels: operations list and scrollable file overview
- Tab-based focus switching between panels (border highlight)
- Operations:
  - **Attribute: delete** — remove an attribute from all CityObjects
  - **Attribute: rename** — rename an attribute across all CityObjects
  - **Attributes: add from CSV** — bulk-add attributes from a CSV file (auto-detects `;` / `,` delimiter)
  - **Roofer → MultiRoofs** — merge BuildingParts into parents, clean up geometry, rename `b3_volume`, add multiroofs extension
- File statistics panel: object counts by type, attribute inventory with sample values, CRS, extensions
- CLI flags: `--output`, `--output-format` (cityjson / cityjsonseq / auto)
- Dialog system for operation parameters, save path input, and quit confirmation
