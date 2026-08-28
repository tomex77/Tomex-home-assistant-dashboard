# Backend configuration

These files are sanitized extracts from the Home Assistant configuration that powers the dashboard.
They are **not** the user's full Home Assistant configuration.

## Files

- `base-dashboard-helpers.yaml` — date/holiday/count helpers and the two generic room/window overlay binary sensors.
- `energy-flow-binary-sensors.yaml` — solar/grid/battery flow-direction binary sensors.
- `energy-visualization-sensors.yaml` — colors, flow CSS strings, labels, weather overlay and light glow helpers.
- `dashboard-status-sensors.yaml` — the summary sensors used by the horizontal-stack overview cards.

## Important installation note

Each file contains a top-level `template:` key. Do not paste multiple `template:` keys into the same `configuration.yaml`.
Either merge the lists under your existing `template:` configuration or use Home Assistant packages.

All device entities are examples/mappings. Read `../docs/STILL-NEEDED.md` before trying to install the dashboard.
