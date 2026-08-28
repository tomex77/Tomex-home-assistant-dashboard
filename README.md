# Home Assistant Dashboard

Sanitized, share-ready Home Assistant dashboard configuration.

## Start here

- `full-dashboard/dashboard.yaml` — complete dashboard, including the visual overview and all horizontal-stack overview rows.
- `sections/overview-horizontal-stacks.yaml` — all eight overview horizontal-stack rows together.
- `sections/` — individual shareable portions.
- `docs/DEPENDENCIES-NEEDED.md` — backend/helper/template definitions still needed to make the shared dashboard reproducible.
- `docs/ASSETS.md` — `/local/` image files referenced by the dashboard.
- `docs/REQUIREMENTS.md` — detected custom frontend cards/features.

## Important placeholders

Before using this dashboard, users should map placeholders such as:

- `YOUR_HOME_ASSISTANT_USERNAME`
- `/YOUR_DASHBOARD_PATH/...`
- `weather.home`
- `alarm_control_panel.home_alarm`
- `sensor.your_3d_printer_current_stage`
- `sensor.your_3d_printer_remaining_time`
- `/local/profile_primary.png`
- `/local/profile_default.png`

The backend/template/helper configuration is being separated from the Lovelace dashboard so individual sections can be shared with their required dependencies.
