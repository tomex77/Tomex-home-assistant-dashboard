# User-created setup requirements

Some parts of this dashboard are intentionally **not included as downloadable Home Assistant configuration** because they are specific to each user's home.

## Helpers you must create

Create these helpers in Home Assistant from:

**Settings → Devices & services → Helpers → Create helper**

### Counters

Create three **Counter** helpers and use these entity IDs (or update the dashboard/templates to match your own IDs):

- `counter.notification`
- `counter.mailbox`
- `counter.trash_counter`

These counters are used by `sensor.dashboard_home_notification` to display dashboard notification status.

The repository does not require any particular automation for these counters. You can increment/reset them using your own automations, scripts, buttons, integrations, or other logic.

### Toggles

Create two **Toggle** helpers:

- `input_boolean.visitor`
- `input_boolean.lawn`

`input_boolean.visitor` is used by the camera/doorbell status card.

`input_boolean.lawn` is used by the irrigation/lawn status card.

How these toggles are turned on or off is intentionally left to the user. You can control them with your own automations or manually.

## House and garage images / GIFs

The home visualization in this repository was designed around custom images of the author's own home. Those personal image files are **not distributed** with the repository.

If you want to recreate the effect, create your own house images and garage-door animations and place them in your Home Assistant `/config/www/` directory. Files stored there are referenced in dashboards as `/local/...`.

The included `sensor.housecard` produces these states:

- `g1_opening`
- `g2_opening`
- `g1_closing`
- `g2_closing`
- `both_open`
- `g1_open_g2_closed`
- `g2_open_g1_closed`
- `both_closed`
- `default`

Use those states to select your own matching images/GIFs in `sections/home-visualization.yaml` or in the full overview dashboard.

You do **not** need to copy the author's home images. The intent is for each user to substitute imagery representing their own home.

## Other entity IDs

Device and integration entities such as lights, garage doors, weather, TVs, locks, solar/battery sensors, vacuum entities, and climate entities are examples. Replace the public placeholder IDs with the entities from your own Home Assistant installation.

See `BACKEND-ENTITY-MAPPING.md` for the main mappings.
