# zmk-dongle-display
# Dongle Display

This module repository provides a ZMK shield that replaces the built-in status screen with a custom screen designed for 128x64-pixel OLED displays.

## Usage

To use this module, first add it to your `config/west.yml` by adding a new entry to `remotes` and `projects`:

```yaml west.yml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: williambonfim
      url-base: https://github.com/williambonfim
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: zmk-dongle-display
      remote: williambonfim
      revision: main
  self:
    path: config
```

Next, replace the built-in status screen by adding `dongle_display` to your `build.yaml`:

```yaml build.yaml
---
include:
  - board: nice_nano_v2
    shield: corne_central_dongle dongle_display
```

This shield assumes that the dongle is already set up and functioning with the built-in status screen.
For setup examples, refer to the shields in my [`zmk-config`](https://github.com/englmaxi/zmk-config/tree/master/boards/shields).
- If you are using the larger 1.3" OLED, replace `solomon,ssd1306fb` with `sinowealth,sh1106` and set `segment-offset = <2>`.
- If you are using a nice!nano, replace `xiao_i2c` with `pro_micro_i2c`.

## Widgets
- active hid indicators (CLCK, NLCK, SLCK)
- active modifiers
- bongo cat
- highest layer name
- output status
- peripheral battery levels
- wpm speed

## Configuration

To also display the battery level of the dongle/central device, use the following configuration property:

```ini
CONFIG_ZMK_DONGLE_DISPLAY_DONGLE_BATTERY=y
```

If you want to use MacOS modifier symbols instead of the Windows modifier symbols, use the following configuration property:

```ini
CONFIG_ZMK_DONGLE_DISPLAY_MAC_MODIFIERS=y
```