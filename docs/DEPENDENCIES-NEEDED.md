# Dependency Code Still Needed

The Lovelace YAML references the following entities that appear to be created by helpers, templates, counters, or custom backend logic. We need to locate their definitions in your Home Assistant configuration before the GitHub repository is complete.

## Revised top / visual section

- `binary_sensor.battery_to_house`
- `binary_sensor.grid_to_battery`
- `binary_sensor.grid_to_house`
- `binary_sensor.my_home_battery_charging`
- `binary_sensor.solar_to_battery`
- `binary_sensor.solar_to_grid`
- `binary_sensor.solar_to_house`
- `binary_sensor.window1_overlay`
- `binary_sensor.window2_overlay`
- `counter.mailbox`
- `counter.notification`
- `counter.trash_counter`
- `sensor.battery_house_flow_style`
- `sensor.battery_pulse_animation`
- `sensor.countdown_2`
- `sensor.current_day_and_date`
- `sensor.dashboard_home_notification`
- `sensor.driveway_light_glow_style`
- `sensor.flow_2`
- `sensor.front_porch_glow_style`
- `sensor.garage_light_glow_style`
- `sensor.grid_battery_flow_style`
- `sensor.grid_house_only_flow_style`
- `sensor.grid_power_color`
- `sensor.grid_power_label`
- `sensor.housecard`
- `sensor.living_room_overlay_opacity`
- `sensor.load_power_color`
- `sensor.load_power_label`
- `sensor.next_holiday_sensor`
- `sensor.solar_battery_flow_style`
- `sensor.solar_flow_style`
- `sensor.solar_grid_export_flow_style`
- `sensor.solar_house_flow_style`
- `sensor.solar_power_label`
- `sensor.solar_status_color`
- `sensor.weather_overlay_combined`

## Horizontal-stack overview cards

- `sensor.dashboard_alarm_status`
- `sensor.dashboard_bed_status`
- `sensor.dashboard_blinds_status`
- `sensor.dashboard_camera_status`
- `sensor.dashboard_climate_status`
- `sensor.dashboard_covers_status`
- `sensor.dashboard_doors_status`
- `sensor.dashboard_irrigation_status`
- `sensor.dashboard_laundry_status`
- `sensor.dashboard_lights_status`
- `sensor.dashboard_locks_status`
- `sensor.dashboard_media_status`
- `sensor.dashboard_sensors_status`
- `sensor.dashboard_vacuum_status`

## Device/integration entities

These normally should **not** be copied from your backend config; users map them to their own devices/integrations:

- `alarm_control_panel.home_alarm`
- `cover.living_2_blinds`
- `cover.window_blinds`
- `light.driveway`
- `light.front_porch`
- `light.garage`
- `light.living_room_lights`
- `sensor.my_home_percentage_charged`
- `sensor.speedtest_download`
- `sensor.your_3d_printer_current_stage`
- `sensor.your_3d_printer_remaining_time`
- `sun.sun`
- `switch.wake_on_lan`
- `weather.home`
