# Backend configuration

These files are sanitized extracts from the Home Assistant configuration that powers the dashboard. They are **not** the author's full Home Assistant configuration.

## Files

- `base-dashboard-helpers.yaml` — date/holiday/count helpers and generic room/window overlay binary sensors.
- `dashboard-support-sensors.yaml` — holiday countdown, house image-state selector, active-TV counter, and open-door summary.
- `energy-flow-binary-sensors.yaml` — solar/grid/battery flow-direction binary sensors.
- `energy-visualization-sensors.yaml` — colors, flow CSS strings, labels, weather overlay and light glow helpers.
- `dashboard-status-sensors.yaml` — summary sensors used by the horizontal-stack Overview cards.

## Important installation note

Each backend file contains a top-level `template:` key. Do not paste multiple `template:` keys into the same `configuration.yaml`.

Either merge the lists under your existing `template:` configuration or use Home Assistant packages.

## Things intentionally not included

Some dependencies are specific to each user's home and must be created or replaced locally:

- The notification/mail/trash counters and visitor/lawn toggles are ordinary Home Assistant UI-created helpers.
- Custom house and garage-door images/GIFs are user-supplied and are not distributed.
- Physical device/integration entity IDs must be mapped to the installer's own entities.

Read `../docs/USER-SETUP.md` before installing the dashboard.
