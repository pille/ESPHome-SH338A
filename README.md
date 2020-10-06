# ESPHome-SH338A
ESPHome configuration to generate firmware for EFUN Smart Plug (SH338A)


## About
this project provides a ([YAML](https://yaml.org)) configuration to generate and build a custom firmware for the **EFUN Smart Plug** (**SH338A**) in order to free it from its vendors' cloud integration, while retaining its most impotant features. you bought it, so it should run your code, respecting your privacy.

it uses the [ESPHome](https://esphome.io) framework to generate C code for the [ESP8266-S3](https://fccid.io/2AKBPESP8266-S3/User-Manual/User-Manual-3594791) microcontroller that drives the socket.
it is then compiled using [PlatformIO](https://platformio.org).


## Scope

this project is tied and limited to the cheap EFUN Smart Plug (SH338A), which currently costs about 5€ per unit in a pack of four.

although it most likely runs on other hardware using a ESP8266 based microcontroller, it's not supported, as they use different GPIOs. feel free to fork this configuration and adapt the GPIOs.
a general rule of thumb: if the device is [supported by tasmota](https://tasmota.github.io/docs/devices/Other-Devices/#plugssockets), it will work.

* no security by default as supposed to run in isolated network


### Hardware
* power socket
  * 230V AC 50Hz 16A ≙ max. 3680W
  * controlled by relay (`GPIO15`)
* button (`GPIO13`)
* green LED (`GPIO2`) around the button
* [ESP8285](https://www.espressif.com/sites/default/files/documentation/0a-esp8285_datasheet_en.pdf) ≙ [ESP8266-S3](https://fccid.io/2AKBPESP8266-S3/User-Manual/User-Manual-3594791) with 1MB flash integrated

### Features
* "dumb" standalone (a.k.a physical access):
  * power on/off
  * countdown timer
* "smart" connected (a.k.a. remote access):
  * connect to your WIFI
  * fallback Access-Point (in case configured WIFIs can't be joined)
  * integrated webserver
    * power on/off
    * firmware upgrade
    * debug interface
  * integrates with [Home-Assistant](https://hass.io) via [Home-Assistant ESPHome Integration](https://www.home-assistant.io/integrations/esphome)
  * OTA firmware upgrade
  * ESPhome debug interface 

see [Modes of Operation](#Modes-of-Operation) to figure out how to use them.


## Usage
before building the firmware, ensure all of the following dependencies are met:

### Dependencies
* you are able to upload a new firmware
  * use [tuya-convert](https://github.com/ct-Open-Source/tuya-convert) to upload your firmware onto a original device for the first time
  * you can directly upload a new firmware via the webinterface, when you already have a custom firmware installed ([TASMOTA](https://tasmota.github.io/docs), [ESPurna](https://github.com/xoseperez/espurna), [ESPEasy](https://www.letscontrolit.com/wiki/index.php?title=ESPEasy), ...)
* [python](https://www.python.org)
* [ESPHome](https://esphome.io): `pip install esphome`

### Setup
* clone this project: `git clone https://github.com/pille/ESPHome-SH338A`
* change into project: `cd ESPHome-SH338A`
* create `secrets.yaml` by copying and editing WIFI credentials from `secrets.yaml.sample`

### Building the Firmware
* `esphome SH338A.yaml compile`
  * resulting firmware image is `.pioenvs/sh338a/firmware.bin`

#### multiple devices
since you probably own multiple devices that should have different names in your home automation system, you can build all their individual firmwares by defining an appendix (`1` in this example):

* `esphome -s append_name 1 SH338A.yaml compile`
  * resulting firmware image is: `.pioenvs/sh338a1/firmware.bin`

### Flashing the Firmware

#### Webinterface
#### tuya-convert
#### OTA


### Modes of Operation


## Contributing

## Similar Projects

## License
AGPL-v3