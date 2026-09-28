# esp32-web-server

An ESP32 Arduino sketch that serves a small web page for switching the three channels of an RGB LED (red, green and blue) on and off from a browser.

## Features

* Web page with a state line (`GPIO <n> - State on/off`) and a Turn ON / Turn OFF button for each color.
* Simple URL endpoints, so a link or `curl` can switch a channel.
* Runs on port 80 using the `WiFi` library that ships with the ESP32 core; no extra libraries needed.
* Online simulation on [Wokwi](https://wokwi.com/projects/380548733838320641).

## Wiring

| Color | GPIO |
|-------|------|
| Blue | 23 |
| Green | 22 |
| Red | 19 |

Each pin drives its channel HIGH for on and LOW for off (a common-cathode RGB LED, each channel through a current-limiting resistor). All channels start off.

## Configuration

Set your Wi-Fi credentials in [`esp32-web-ui-rgb-led/esp32-web-ui-rgb-led.ino`](esp32-web-ui-rgb-led/esp32-web-ui-rgb-led.ino):

```cpp
const char* ssid = "";
const char* password = "";
```

## Usage

1. Open the sketch in the [Arduino IDE](https://www.arduino.cc/en/software) with ESP32 board support installed.
2. Fill in `ssid` and `password`, select your board and port, then upload.
3. Open the serial monitor at **115200** baud. After Wi-Fi connects, the sketch prints the board's IP address.
4. Open `http://<ip>/` in a browser and use the buttons.

### URL endpoints

Each request returns the full HTML page.

| URL | Action |
|-----|--------|
| `/23/on`, `/23/off` | Blue on / off |
| `/22/on`, `/22/off` | Green on / off |
| `/19/on`, `/19/off` | Red on / off |

```bash
curl http://<ip>/19/on
```

## Limitations

* No authentication: anyone on the network can switch the LED.
* LED state is kept in memory and resets to off on reboot.
* The sketch waits for Wi-Fi forever at startup.

## Credits

Based on the ESP32 Web Server example by Rui Santos from [Random Nerd Tutorials](https://randomnerdtutorials.com); the original header is kept in the sketch.

## License

This repository has no license file.
