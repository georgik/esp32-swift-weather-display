# ESP32 Swift Weather Display Example

![Test Status](https://github.com/georgik/esp32-swift-weather-display/actions/workflows/test.yml/badge.svg)

Supported targets: ESP32-C3, ESP32-C6

Read more about Swift for ESP32 at [Espressif Developer Portal](https://developer.espressif.com/tags/swift/).

## On-line Demo Simulation

[![ESP32-C6 Swift Weather Display](docs/img/esp32-c3-swift-weather-display.webp)](https://wokwi.com/experimental/viewer?diagram=https%3A%2F%2Fraw.githubusercontent.com%2Fgeorgik%2Fesp32-swift-weather-display%2Fmain%2Fboards%2Fesp32_c6_devkit%2Fdiagram.json&firmware=https%3A%2F%2Fgithub.com%2Fgeorgik%2Fesp32-swift-weather-display%2Freleases%2Fdownload%2Fv1.0.0%2Fesp32-swift-weather-display-esp32_c6_devkit.bin)

[ESP32-C6 Swift Weather Display with Wokwi.com](https://wokwi.com/experimental/viewer?diagram=https%3A%2F%2Fraw.githubusercontent.com%2Fgeorgik%2Fesp32-swift-weather-display%2Fmain%2Fboards%2Fesp32_c6_devkit%2Fdiagram.json&firmware=https%3A%2F%2Fgithub.com%2Fgeorgik%2Fesp32-swift-weather-display%2Freleases%2Fdownload%2Fv1.0.0%2Fesp32-swift-weather-display-esp32_c6_devkit.bin)

## Requirements

- Swift 6.1 - https://www.swift.org/install
- ESP-IDF 5.4 - https://github.com/espressif/esp-idf

## Build

### Preparation

Copy `nvs-template.csv` to `nvs.csv` and set proper values.

```shell
cp nvs-template.csv nvs.csv
```

### Configure build environment

```shell
source esp-idf/export.sh
export TOOLCHAINS=$(plutil -extract CFBundleIdentifier raw /Library/Developer/Toolchains/swift-DEVELOPMENT-SNAPSHOT-2024-10-30-a.xctoolchain/Info.plist)
```

### Build for ESP32-C3-LcdKit

```shell
idf.py @boards/esp32_c3_lcdkit.cfg flash monitor
```

### Build for ESP32-P4-Function-EV-Board

```shell
idf.py @boards/esp32_p4_function_ev_board.cfg flash monitor
```

Note: Wi-Fi communication is handled by ESP32-C6 chip on the board.
The communication between ESP32-P4 and ESP32-C6 is based on [esp_wifi_remote component](https://components.espressif.com/components/espressif/esp_wifi_remote).


### Build for ESP32-C6-DevKit or Custom Devkit

The configuration of this board is based on [ESP-BSP Generic](https://developer.espressif.com/blog/using-esp-bsp-with-devkits/) which allows configuration using menuconfig.

SPI Display configuration:

```ini
CONFIG_BSP_DISPLAY_ENABLED=y
CONFIG_BSP_DISPLAY_SCLK_GPIO=6
CONFIG_BSP_DISPLAY_MOSI_GPIO=7
CONFIG_BSP_DISPLAY_MISO_GPIO=-1
CONFIG_BSP_DISPLAY_CS_GPIO=20
CONFIG_BSP_DISPLAY_DC_GPIO=21
CONFIG_BSP_DISPLAY_RST_GPIO=3
CONFIG_BSP_DISPLAY_DRIVER_ILI9341=y
```

You can change the configuration by running:

```shell
idf.py @boards/esp32_c6_devkit.cfg menuconfig
```

Flash and monitor

```shell
idf.py @boards/esp32_c6_devkit.cfg flash monitor
```

### Run simulation in VS Code

- Build the project, to get binaries for simulation.
- Install [Wokwi for VS Code](https://docs.wokwi.com/vscode/getting-started/).
- Open file `boards/esp32_.../diagram.json`.
- Click Play button to start simulation.
- Click Pause button to freeze simulation and display states of GPIOs.

## Credits

- Font FreeSans.ttf: https://github.com/opensourcedesign/fonts/blob/master/gnu-freefont_freesans/FreeSans.ttf
