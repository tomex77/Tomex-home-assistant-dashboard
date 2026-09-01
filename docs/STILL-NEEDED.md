# Remaining setup requirements

The reusable dashboard template dependency chain is resolved for the shared Overview dashboard.

There are no additional private Home Assistant configuration files required from the original installation for the Overview dashboard package.

## User-created helpers

The following helpers must be created by the person installing the dashboard:

- `counter.notification`
- `counter.mailbox`
- `counter.trash_counter`
- `input_boolean.visitor`
- `input_boolean.lawn`

These are normal Home Assistant helpers created from **Settings → Devices & services → Helpers**. They are not copied from the original system's `.storage` files.

Their automation/control logic is optional and installation-specific. Users can control them manually or with their own automations.

See `USER-SETUP.md` for details.

## User-supplied visual assets

The custom home/garage images and animated GIFs are intentionally **not distributed** because they depict the original author's home.

Anyone using the home visualization should create their own images/GIFs and update the `/local/...` paths in the dashboard YAML.

See `USER-SETUP.md` for the expected `sensor.housecard` states and setup guidance.

## Integration/device entities to map

These normally come from integrations/devices rather than reusable YAML:

- `calendar.holidays_in_united_states`
- `cover.garage1`
- `cover.garage2`
- `sensor.my_home_solar_power`
- `sensor.my_home_grid_power`
- `sensor.my_home_load_power`
- `sensor.my_home_battery_power`
- `sensor.my_home_percentage_charged`
- `weather.home`
- `sensor.speedtest_download`
- `switch.wake_on_lan`
- `sensor.your_3d_printer_current_stage`
- `sensor.your_3d_printer_remaining_time`

Users should replace these with equivalent entities from their own Home Assistant installation.
