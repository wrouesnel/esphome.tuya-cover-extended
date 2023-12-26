# ESPHome tuya-cover-extended

This is an extended version of the built-in `cover` component on the `tuya` platform in
ESPHome.

The primary change is it allows inverting the position report via `invert_position_report` for a
Tuya platform cover. An example for the blind I developed this for is below:

```
cover:
  - platform: tuya-ex
    name: Motor
    control_datapoint: 1
    position_datapoint: 2
    position_report_datapoint: 3
    restore_mode: NO_RESTORE
    min_value: 0
    max_value: 100
    device_class: blind
    invert_position_report: true
```

This is for a Zemismart `ZMTQ25-TYW`. This blind reports it's position as 0 to 100 once calibrated,
but inverts that report if you invert the motor direction. The problem is this makes the report
consistently "percentage open" and ESPHome cover components and Home Assistant both deal consistently
with "% closed".

By setting `invert_position_report` to true, the % values are inverted when they're used which ensures
consistent behavior.