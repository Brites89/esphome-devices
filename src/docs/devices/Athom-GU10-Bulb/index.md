---
title: Athom GU10 Bulb
date-published: 2021-10-05
type: light
standard: us
board: esp8266
---

Manufacturer: [Athom.tech](https://www.athom.tech/blank-1/gu10-rgbcw)

## Flashing Procedure

Natively runs Tasmota, upload ESPHome binary to flash wirelessly.

## Bulb Specifications

Color: RGB+Warm+Cold White
Color Temperature: 3000-6000K
Brightness: 300 lumens
Voltage: 110V~240V
Power: 4.5W
Base:  GU10

## Product Images

![Athom GU10 Bulb](/Athom-GU10-Bulb.png "Athom GU10 Bulb")

## GPIO Pinout

| Pin    | Function             |
| ------ | -------------------- |
| GPIO13 | CT Output            |
| GPIO5  | CT Brightness Output |
| GPIO4  | Red Output           |
| GPIO12 | Green Output         |
| GPIO14 | Blue Output          |

## Basic Configuration

```yaml
substitutions:
  device_name: "athom-rgbww-light"
  friendly_name: "Athom RGBWW Light"
  project_name: "athom.rgbww-light"
  project_version: "1.0"

esphome:
  name: "${device_name}"
  name_add_mac_suffix: true
  project:
    name: "${project_name}"
    version: "${project_version}"

esp8266:
  board: esp8285

api:

ota:

logger:

web_server:
  port: 80

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  ap:

captive_portal:

binary_sensor:
  - platform: status
    name: "${friendly_name} Status"

sensor:
  - platform: uptime
    name: "${friendly_name} Uptime Sensor"

switch:
  - platform: restart
    id: restart_switch
    name: "${friendly_name} Restart"

output:
  - platform: esp8266_pwm
    id: red_output
    pin: GPIO4
  - platform: esp8266_pwm
    id: green_output
    pin: GPIO12
  - platform: esp8266_pwm
    id: blue_output
    pin: GPIO14
  - platform: esp8266_pwm
    id: warm_white_output
    pin: GPIO13
  - platform: esp8266_pwm
    id: white_output
    pin: GPIO5


light:
  - platform: rgbww
    name: "${friendly_name}"
    red: red_output
    green: green_output
    blue: blue_output
    warm_white: warm_white_output
    cold_white: white_output
    cold_white_color_temperature: 6000 K
    warm_white_color_temperature: 3000 K
    color_interlock: true

text_sensor:
  - platform: wifi_info
    ip_address:
      name: "${friendly_name} IP Address"
      disabled_by_default: true
```
