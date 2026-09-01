# Installation Guide

This guide explains how to adapt and install the **Tomex Home Assistant Dashboard** in your own Home Assistant system.

> [!IMPORTANT]
> This project is **not a drop-in configuration**. Every Home Assistant installation has different entity IDs, integrations, devices, helpers, and images. You will need to replace the example/placeholder entities with your own.

---

## 1. Choose what you want to install

There are two ways to use this repository.

### Complete Overview dashboard

Use:

```text
overview-dashboard/dashboard.yaml
```

This contains the complete Overview page, including the animated home/energy visualization and the horizontal status rows.

### Individual sections

Use files from:

```text
sections/
```

For example:

```text
sections/home-visualization.yaml
sections/alarm-cameras.yaml
sections/lights-climate.yaml
sections/overview-horizontal-stacks.yaml
```

The individual section files are intended to be copied into an existing Home Assistant dashboard and adapted to your layout.

---

## 2. Install the frontend requirements

This dashboard uses several custom Home Assistant frontend components.

Install the components you need through **HACS → Frontend** before adding the dashboard YAML.

The dashboard currently uses:

- Mushroom cards
- card-mod
- layout-card / grid-layout
- button-card
- Kiosk Mode
- Swipe Navigation

The dashboard also references the theme:

```text
Caule Black Aqua
```

Install that theme if you want the same appearance, or change/remove the `theme:` entry in the dashboard YAML and use your own theme.

See `docs/REQUIREMENTS.md` for the frontend requirements used by this repository.

---

## 3. Add the backend template sensors

The dashboard depends on template sensors and binary sensors contained in:

```text
backend/
```

The backend files currently include:

```text
backend/base-dashboard-helpers.yaml
backend/dashboard-support-sensors.yaml
backend/dashboard-status-sensors.yaml
backend/energy-flow-binary-sensors.yaml
backend/energy-visualization-sensors.yaml
```

### Important: do not create multiple `template:` keys in configuration.yaml

Each backend file is written with a top-level:

```yaml
template:
```

You have two common installation choices.

### Option A — Home Assistant packages

If your Home Assistant configuration already uses packages, the backend files can be adapted as package files. This keeps the dashboard-related configuration separated from the rest of your Home Assistant configuration.

### Option B — Merge into your existing template configuration

If you already have a `template:` section, merge the `sensor:` and `binary_sensor:` entries from the provided files into that existing template configuration.

Do **not** paste several separate top-level `template:` keys into the same YAML file.

After adding or changing template YAML, check the Home Assistant configuration and reload the appropriate YAML entities or restart Home Assistant as required by your setup.

---

## 4. Create the required Home Assistant Helpers

These helpers are **not included as YAML files** because they were created through the Home Assistant UI.

Go to:

**Settings → Devices & services → Helpers → Create helper**

### Create these Counter helpers

```text
counter.notification
counter.mailbox
counter.trash_counter
```

They are used by the dashboard notification summary.

### Create these Toggle helpers

```text
input_boolean.visitor
input_boolean.lawn
```

- `input_boolean.visitor` is used by the camera/doorbell status card.
- `input_boolean.lawn` is used by the lawn/irrigation status card.

Your own automations, integrations, scripts, buttons, or other logic can control these helpers. The author's personal automations are not required by the dashboard.

See `docs/USER-SETUP.md` for more information.

---

## 5. Replace the public placeholders

Before the dashboard will work correctly, replace the example and placeholder entities with entities from your own Home Assistant installation.

Important placeholders include:

```text
YOUR_HOME_ASSISTANT_USERNAME
/YOUR_DASHBOARD_PATH/...
weather.home
alarm_control_panel.home_alarm
sensor.your_3d_printer_current_stage
sensor.your_3d_printer_remaining_time
media_player.tv_1
media_player.tv_2
...
media_player.tv_8
```

You will also need to review and replace device entities for things such as:

- Lights
- Switches
- Locks
- Garage doors / covers
- Door and motion sensors
- Leak, smoke, and CO sensors
- Climate devices
- Fans
- Vacuum
- Blinds
- Washer / dryer
- Bed occupancy
- Irrigation
- Network sensors
- Solar, grid, battery, and home-load power sensors

See:

```text
docs/BACKEND-ENTITY-MAPPING.md
```

for the main backend entity mappings.

---

## 6. Configure the holiday countdown

The holiday countdown uses a calendar entity.

The example backend currently references:

```text
calendar.holidays_in_united_states
```

If your holiday calendar has a different entity ID, replace that entity in:

```text
backend/base-dashboard-helpers.yaml
backend/dashboard-support-sensors.yaml
```

The resulting dashboard sensors include:

```text
sensor.next_holiday_sensor
sensor.next_holiday_date_sensor
sensor.countdown_2
```

---

## 7. Configure the garage/home visualization

The included `sensor.housecard` watches two garage-cover entities:

```text
cover.garage1
cover.garage2
```

Replace those with your garage entities if necessary.

`sensor.housecard` produces these states:

```text
g1_opening
g2_opening
g1_closing
g2_closing
both_open
g1_open_g2_closed
g2_open_g1_closed
both_closed
default
```

The dashboard uses those states to choose the appropriate image or animation.

### The author's house images and garage GIFs are not included

The original dashboard uses custom images and animated GIFs created specifically for the author's home. Those personal assets are intentionally not distributed in this repository.

Create your own images/animations and store them in Home Assistant's:

```text
/config/www/
```

Files in `/config/www/` are referenced from dashboards using:

```text
/local/filename.ext
```

Then update the image paths in:

```text
sections/home-visualization.yaml
```

and/or:

```text
overview-dashboard/dashboard.yaml
```

You can also remove the image-state elements entirely if you do not want to recreate the animated-house effect.

---

## 8. Review the other `/local/` assets

The dashboard may reference other `/local/` images such as profile images and weather-overlay graphics.

Examples include placeholders such as:

```text
/local/profile_primary.png
/local/profile_default.png
```

You can:

1. Provide your own replacement images in `/config/www/`, or
2. Edit/remove the corresponding dashboard elements.

Do not expect the author's private images to be included with the repository.

---

## 9. Configure the TV counter

`sensor.tvon` counts media players that are considered active.

The public version uses generic placeholders:

```text
media_player.tv_1
media_player.tv_2
media_player.tv_3
media_player.tv_4
media_player.tv_5
media_player.tv_6
media_player.tv_7
media_player.tv_8
```

Edit the list in:

```text
backend/dashboard-support-sensors.yaml
```

and replace those entries with your own TV/media-player entities.

You can add or remove entries from the list to match the number of TVs in your home.

---

## 10. Configure the door summary

The public `sensor.count_doors_open` example uses generic door-contact entities such as:

```text
binary_sensor.front_door
binary_sensor.back_door
binary_sensor.shed
binary_sensor.balcony_door
binary_sensor.garage_door
binary_sensor.backyard_side_door
```

Replace or remove these entries in:

```text
backend/dashboard-support-sensors.yaml
```

so the list matches your home.

The Dashboard Doors Status template must use matching entities as well.

---

## 11. Configure the energy-flow visualization

The energy visualization expects power sensors representing:

```text
sensor.my_home_solar_power
sensor.my_home_grid_power
sensor.my_home_battery_power
sensor.my_home_load_power
sensor.my_home_percentage_charged
```

Replace these with the equivalent sensors from your solar/battery/energy integration.

### Power-direction assumptions

The included flow logic assumes:

- Solar power is positive while producing.
- Grid power greater than `0` means importing from the grid.
- Grid power less than `0` means exporting to the grid.
- Battery power less than `0` means the battery is charging.
- Battery power greater than `0` means the battery is discharging.

If your integration uses different signs, adjust the comparisons in:

```text
backend/energy-flow-binary-sensors.yaml
backend/energy-visualization-sensors.yaml
```

Otherwise the animation direction/status may be incorrect even though the sensors are reporting valid values.

---

## 12. Add the full dashboard to Home Assistant

If you are using Home Assistant's normal UI-managed dashboard, one common method is:

1. Open the target Home Assistant dashboard.
2. Enter dashboard edit mode.
3. Open the dashboard's **Raw configuration editor**.
4. Back up your existing YAML before replacing anything.
5. Copy/adapt the contents of:

   ```text
   overview-dashboard/dashboard.yaml
   ```

6. Replace all remaining entity IDs and placeholders with your own.
7. Save the dashboard.

If you already maintain Lovelace dashboards in YAML files, adapt the provided configuration to your existing YAML-dashboard structure instead.

> [!WARNING]
> Do not overwrite an existing dashboard configuration unless you have saved a copy of it first.

---

## 13. Add only an individual section

If you do not want the complete Overview dashboard:

1. Open the appropriate file in `sections/`.
2. Copy the card configuration you want.
3. Paste it into the `cards:` area of the target Home Assistant view/layout.
4. Replace the example entity IDs with your own.
5. Install only the backend template files required by that section.

For all eight status rows together, use:

```text
sections/overview-horizontal-stacks.yaml
```

---

## 14. Navigation paths

Some cards use navigation paths represented publicly as:

```text
/YOUR_DASHBOARD_PATH/...
```

Replace those with the paths used by your own Home Assistant dashboards/views.

If you do not want those cards to navigate anywhere, change or remove the associated `tap_action`.

---

## 15. Verify the installation

Before troubleshooting the visual layout, use **Developer Tools → States** in Home Assistant and confirm that the custom template entities exist and are returning sensible values.

Examples include:

```text
sensor.dashboard_alarm_status
sensor.dashboard_camera_status
sensor.dashboard_lights_status
sensor.dashboard_climate_status
sensor.dashboard_locks_status
sensor.dashboard_covers_status
sensor.dashboard_doors_status
sensor.dashboard_sensors_status
sensor.dashboard_vacuum_status
sensor.dashboard_blinds_status
sensor.dashboard_media_status
sensor.dashboard_laundry_status
sensor.dashboard_bed_status
sensor.dashboard_irrigation_status
sensor.housecard
sensor.countdown_2
```

For the energy visualization, also check the `binary_sensor.*_to_*` flow sensors.

---

## Troubleshooting

### `Custom element doesn't exist`

A required HACS frontend card/resource is missing or has not loaded. Verify the frontend requirements and refresh Home Assistant after installing them.

### A card shows `Unknown` or `Unavailable`

An entity ID probably does not exist in your installation or has not been replaced with your own entity.

Use **Developer Tools → States** to verify the entity ID.

### The house/garage image is blank

Check that:

- Your files exist in `/config/www/`.
- The dashboard references them as `/local/...`.
- The filenames and capitalization match exactly.
- `sensor.housecard` is producing one of the expected states.

### Energy arrows or flows move in the wrong direction

Check the sign convention of your grid and battery power sensors. Your integration may use the opposite positive/negative direction from the included templates.

### YAML reports a duplicate `template:` key

Do not paste all backend files one after another into `configuration.yaml` unchanged. Merge their template lists under your existing `template:` configuration or use Home Assistant packages.

### The theme is missing

Install the referenced theme or replace/remove:

```yaml
theme: Caule Black Aqua
```

### A navigation card opens the wrong page

Replace `/YOUR_DASHBOARD_PATH/...` with the path from your own Home Assistant dashboard.

---

## Recommended setup order

For the easiest installation, use this order:

1. Install the required HACS frontend components.
2. Add the backend template sensors/binary sensors.
3. Create the five Home Assistant Helpers.
4. Replace backend device/entity placeholders.
5. Verify the new template entities in Developer Tools.
6. Create or remove the custom `/local/` image assets.
7. Add the Overview dashboard YAML or individual sections.
8. Replace dashboard-level placeholders and navigation paths.
9. Save and test each section.

---

## Need to customize it?

This repository is intended to provide the structure and logic behind the dashboard while allowing each user to adapt it to their own Home Assistant installation.

Start with:

```text
docs/USER-SETUP.md
docs/BACKEND-ENTITY-MAPPING.md
docs/REQUIREMENTS.md
```

and then work through the entity IDs used by the section you want to install.
