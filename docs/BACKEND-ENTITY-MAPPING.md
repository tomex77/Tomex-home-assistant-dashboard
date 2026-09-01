# Backend Entity Mapping

This document explains which entities in the public dashboard are created by the included backend YAML files and which entities must be replaced with equivalents from your own Home Assistant installation.

The repository is intentionally sanitized. Personal names, account-specific entities, device serials, IP-based entity IDs, and home-specific identifiers have been replaced with generic placeholders.

---

## Backend files

The `backend/` directory contains the template entities used by the Overview dashboard.

| File | Purpose |
|---|---|
| `backend/base-dashboard-helpers.yaml` | General date, holiday, light/fan/motion counts, and room-overlay helpers |
| `backend/dashboard-support-sensors.yaml` | Holiday countdown, garage/house state, TV count, and open-door summary |
| `backend/dashboard-status-sensors.yaml` | Summary sensors used by the horizontal Overview cards |
| `backend/energy-flow-binary-sensors.yaml` | Determines solar/grid/battery flow direction |
| `backend/energy-visualization-sensors.yaml` | Colors, labels, gradients, glow effects, and animated energy-flow styles |

If you install these backend files, the custom entities listed in the next section are created for you.

---

## Entities created by the included backend

### General helpers

Created by `backend/base-dashboard-helpers.yaml`:

- `sensor.current_day_and_date`
- `sensor.next_holiday_sensor`
- `sensor.count_motion_on`
- `sensor.count_lights_on`
- `sensor.count_fan_on`
- `binary_sensor.window1_overlay`
- `binary_sensor.window2_overlay`

Created by `backend/dashboard-support-sensors.yaml`:

- `sensor.next_holiday_date_sensor`
- `sensor.countdown_2`
- `sensor.housecard`
- `sensor.tvon`
- `sensor.count_doors_open`

### Dashboard summary sensors

Created by `backend/dashboard-status-sensors.yaml`:

- `sensor.dashboard_alarm_status`
- `sensor.dashboard_camera_status`
- `sensor.dashboard_lights_status`
- `sensor.dashboard_climate_status`
- `sensor.dashboard_locks_status`
- `sensor.dashboard_covers_status`
- `sensor.dashboard_doors_status`
- `sensor.dashboard_sensors_status`
- `sensor.dashboard_vacuum_status`
- `sensor.dashboard_blinds_status`
- `sensor.dashboard_media_status`
- `sensor.dashboard_laundry_status`
- `sensor.dashboard_bed_status`
- `sensor.dashboard_irrigation_status`
- `sensor.dashboard_home_notification`

### Energy-flow binary sensors

Created by `backend/energy-flow-binary-sensors.yaml`:

- `binary_sensor.my_home_battery_charging`
- `binary_sensor.solar_to_house`
- `binary_sensor.solar_to_battery`
- `binary_sensor.solar_to_grid`
- `binary_sensor.battery_to_house`
- `binary_sensor.grid_to_house`
- `binary_sensor.grid_to_battery`

### Energy visualization sensors

Created by `backend/energy-visualization-sensors.yaml`:

- `sensor.solar_status_color`
- `sensor.battery_pulse_animation`
- `sensor.load_power_color`
- `sensor.grid_power_color`
- `sensor.solar_flow_style`
- `sensor.solar_house_flow_style`
- `sensor.solar_battery_flow_style`
- `sensor.grid_house_only_flow_style`
- `sensor.solar_grid_export_flow_style`
- `sensor.grid_battery_flow_style`
- `sensor.battery_house_flow_style`
- `sensor.solar_power_label`
- `sensor.grid_power_label`
- `sensor.load_power_label`
- `sensor.garage_light_glow_style`
- `sensor.front_porch_glow_style`
- `sensor.driveway_light_glow_style`
- `sensor.living_room_overlay_opacity`
- `sensor.weather_overlay_combined`

---

# Entities you must map to your own Home Assistant system

## Energy / solar

The dashboard expects the following four live power sensors plus battery percentage.

| Public entity | Replace with |
|---|---|
| `sensor.my_home_solar_power` | Current solar production in kW |
| `sensor.my_home_grid_power` | Current grid import/export power in kW |
| `sensor.my_home_load_power` | Current house/load power in kW |
| `sensor.my_home_battery_power` | Current battery charge/discharge power in kW |
| `sensor.my_home_percentage_charged` | Battery state of charge in percent |

### Important energy sign convention

The included templates expect:

- Solar production: positive
- House load: positive
- Grid import: positive
- Grid export: negative
- Battery discharge: positive
- Battery charging: negative

If your integration uses different signs, modify the templates in:

- `backend/energy-flow-binary-sensors.yaml`
- `backend/energy-visualization-sensors.yaml`

---

## Garage doors / house visualization

| Public entity | Replace with |
|---|---|
| `cover.garage1` | First garage-door cover |
| `cover.garage2` | Second garage-door cover |

`sensor.housecard` converts those cover states into:

- `g1_opening`
- `g2_opening`
- `g1_closing`
- `g2_closing`
- `both_open`
- `g1_open_g2_closed`
- `g2_open_g1_closed`
- `both_closed`
- `default`

The original house and garage GIF/image files are **not included**. Create your own `/local/` images and map these states to them in the dashboard YAML.

---

## Weather and holidays

| Public entity | Replace with |
|---|---|
| `weather.home` | Your Home Assistant weather entity |
| `calendar.holidays_in_united_states` | Your holiday/calendar entity |

If you are outside the United States, use an appropriate calendar integration and update the holiday templates.

The weather visualization also references custom `/local/` weather images such as rain, snow, fog, clouds, and sun. These files are not required for the rest of the dashboard and can be replaced with your own assets.

---

## Alarm

| Public entity | Replace with |
|---|---|
| `alarm_control_panel.home_alarm` | Your alarm control panel |

---

## Media / TVs

| Public entity | Replace with |
|---|---|
| `media_player.spotify` | Your Spotify/media entity |
| `media_player.tv_1` | First TV/media player to count |
| `media_player.tv_2` | Second TV/media player |
| `media_player.tv_3` | Third TV/media player |
| `media_player.tv_4` | Fourth TV/media player |
| `media_player.tv_5` | Fifth TV/media player |
| `media_player.tv_6` | Sixth TV/media player |
| `media_player.tv_7` | Seventh TV/media player |
| `media_player.tv_8` | Eighth TV/media player |

You do not need eight TVs. Remove unused entries from the `players` list in:

`backend/dashboard-support-sensors.yaml`

`sensor.tvon` counts a media player as active when its state is:

- `on`
- `playing`
- `paused`
- `idle`

Adjust that list if your TV integration reports different states.

---

## Door contacts

| Public entity | Replace with |
|---|---|
| `binary_sensor.front_door` | Front-door contact |
| `binary_sensor.back_door` | Back-door contact |
| `binary_sensor.shed` | Shed/extra-door contact |
| `binary_sensor.balcony_door` | Balcony/extra-door contact |
| `binary_sensor.garage_door` | Garage entry/contact sensor |
| `binary_sensor.backyard_side_door` | Backyard/side-door contact |

If you have fewer or more doors, edit both:

- `sensor.count_doors_open` in `backend/dashboard-support-sensors.yaml`
- `sensor.dashboard_doors_status` in `backend/dashboard-status-sensors.yaml`

---

## Locks

| Public entity | Replace with |
|---|---|
| `lock.front_door` | Front-door lock |
| `lock.garage_door` | Garage/secondary lock |
| `lock.touchscreen_deadbolt` | Back-door/third lock |

Edit the template if you have a different number of locks.

---

## Garage covers

These same entities are used by both the Overview Covers card and the animated house:

- `cover.garage1`
- `cover.garage2`

---

## Climate and fans

| Public entity | Replace with |
|---|---|
| `climate.downstairs` | First HVAC zone |
| `climate.bedrooms` | Second HVAC zone |
| `climate.master` | Third HVAC zone |
| `climate.ac` | Additional AC/attic/portable climate entity |
| `fan.bathroom_fan` | Bathroom/exhaust fan |
| `fan.exhaust_fan` | Second exhaust fan |
| `switch.fireplace` | Fireplace switch, if used |
| `sensor.fireplace_switch_0_power` | Fireplace power sensor, if used |

If you do not have a fireplace, remove its lines from `sensor.dashboard_climate_status`.

---

## Camera / visitor status

| Public entity | Replace with |
|---|---|
| `binary_sensor.front_doorbell_reolink_motion` | Doorbell/front camera motion sensor |
| `input_boolean.visitor` | User-created visitor helper |

`input_boolean.visitor` is a Home Assistant UI helper. Create it from:

**Settings → Devices & services → Helpers**

How you turn this helper on and off is up to your own automations.

---

## Motion sensors

`sensor.count_motion_on` contains a list of example motion/presence sensors.

Replace the entities in `backend/base-dashboard-helpers.yaml` with your own motion sensors.

Examples include placeholders such as:

- `binary_sensor.room_1_motion`
- `binary_sensor.room_2_motion`
- `binary_sensor.office_1_presence`
- `binary_sensor.office_2_motion`

You can remove or add sensors as needed.

---

## Room/window overlays

| Public entity | Replace with |
|---|---|
| `light.room_1` | Light controlling overlay 1 |
| `light.room_2` | Light controlling overlay 2 |
| `light.living_room_lights` | Living-room light used for overlay opacity |
| `light.garage` | Garage light |
| `light.front_porch` | Front-porch light |
| `light.driveway` | Driveway light |

These are used only for visual effects and can be modified or removed without affecting the rest of the dashboard.

---

## Leak, smoke, and carbon monoxide sensors

Replace these with your own safety sensors:

- `binary_sensor.water_heater_leak_sensor_moisture`
- `binary_sensor.kitchen_leak_sensor_moisture`
- `binary_sensor.combination_alarm_smoke`
- `binary_sensor.combination_alarm_2_smoke`
- `binary_sensor.combination_alarm_3_smoke`
- `sensor.combination_alarm_carbon_monoxide`
- `sensor.combination_alarm_2_carbon_monoxide`
- `sensor.combination_alarm_3_carbon_monoxide`

If you have a different number of sensors, edit `sensor.dashboard_sensors_status`.

---

## Vacuum

| Public entity | Replace with |
|---|---|
| `vacuum.deebot` | Your vacuum entity |
| `binary_sensor.mop` | Mop-installed/mopping helper or sensor |
| `sensor.deebot_battery` | Vacuum battery percentage sensor |

The dashboard does not require an Ecovacs vacuum specifically. Replace these with the equivalent entities from your vacuum integration.

---

## Blinds

| Public entity | Replace with |
|---|---|
| `cover.window_blinds` | First blind/shade cover |
| `cover.living_2_blinds` | Second blind/shade cover |

The included summary template assumes two covers. Modify it if your setup differs.

---

## Laundry

| Public entity | Replace with |
|---|---|
| `sensor.athom_washer_power` | Washer power-consumption sensor |
| `binary_sensor.dryer` | Dryer-running sensor/helper |
| `switch.ironing_table` | Iron/ironing-table switch |

The washer thresholds in the template are installation-specific. Adjust the wattage thresholds to match your appliance.

---

## Bed occupancy

| Public entity | Replace with |
|---|---|
| `binary_sensor.person_1_in_bed` | First bed-occupancy sensor |
| `binary_sensor.person_2_in_bed` | Second bed-occupancy sensor |

These were sanitized from personally named entities.

---

## Irrigation

| Public entity | Replace with |
|---|---|
| `input_boolean.lawn` | User-created lawn-care helper |
| `switch.rain_bird_sprinkler_side` | First irrigation zone/controller switch |
| `switch.rain_bird_sprinkler_front_main` | Second irrigation zone/controller switch |

`input_boolean.lawn` is a Home Assistant UI-created helper. Users can control it manually or with their own automation.

---

# User-created Home Assistant helpers

The following are **not created by the backend YAML files**. Create them through:

**Settings → Devices & services → Helpers**

### Counters

- `counter.notification`
- `counter.mailbox`
- `counter.trash_counter`

### Toggles

- `input_boolean.visitor`
- `input_boolean.lawn`

The included dashboard reads the states of these helpers. The automations that control them are intentionally left up to each user's installation.

---

# 3D printer entities

The public dashboard uses placeholders such as:

- `sensor.your_3d_printer_current_stage`
- `sensor.your_3d_printer_remaining_time`

Replace these with the equivalent entities from your printer integration.

---

# Navigation placeholder

Replace:

`/YOUR_DASHBOARD_PATH/...`

with the path used by your Home Assistant dashboard, or change/remove those navigation actions.

---

# Profile placeholders

Replace or remove:

- `YOUR_HOME_ASSISTANT_USERNAME`
- `/local/profile_primary.png`
- `/local/profile_default.png`

Profile images are optional.

---

# Custom assets

The original house, garage, and personal visual assets are not distributed with this repository.

Users should create their own files under Home Assistant's `/config/www/` directory and reference them through `/local/`.

See:

`docs/USER-SETUP.md`

for additional setup information.

---

## Quick rule

If an entity is listed under **Entities created by the included backend**, keep it if you are using the supplied backend YAML.

If an entity is listed under **Entities you must map**, replace it with the equivalent entity from your own Home Assistant installation.
