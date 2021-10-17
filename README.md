# IN PROGRESS 

# Accessing ESPHome with IOS Shortcuts

### Background
Having created several ESPHome devices for smart home automation around my house, I began looking for quicker ways to access them. Although the tight integration of ESPHome and HomeAssistant allowed me to feature these devices in whole home browser based smart dashboards, I wanted a simpler way to trigger events than opening an app. I'd toyed with Home Assistant's Emulated Hue (which lets you expose a device to voice assistants such as Alexa) but for some installs (garage doors, for example) the convenience was outstripped by the security risk. As my phone is always on me, the goal was to find a single click solution.

### Approach
The ESPHome system includes two API components:

* An excellent [native API](https://esphome.io/components/api.html) for HomeAssistant
* A [REST API](https://esphome.io/web-api/index.html) exposed as part of ESPHome's [Web Server Component](https://esphome.io/components/web_server.html).

We are interested in the second of these, as it allows easy integration from any http capable device or program.

### Exposing the Webserver API
The following lines in your YAML configuration will enable the webserver.

```yaml
# Example configuration entry
web_server:
  port: 80
```

> :warning: The ESPHome Documentation notes that enabling the webserver component cause issues by  **taking up a lot of device memory**. Although I've been running the web server for many years on ESP8266 devices (sonoff, Wemos D1 minis, etc) without issue, your mileage may vary.

### Accessing the Webserver

When flashed with a sketch that includes the `web_server` lines above, your ESPHome device will expose a web page at the node's IP and via mDNS as ` <name>.local/`.
 
My garage-door sketch starts

```yaml
esphome:
  name: garage-doors
  platform: ESP8266
  board: esp01_1m
```
So my webpage is accessible on my wifi via mDNS as:

```http://garage-doors.local/```

The web page returned is very lightweight, tabular, and includes a row for each sensor, cover, switch, light, etc. For my garage-door sketch, the page looks like this:


Name                 | State | Actions
-------------------- | ------| ----------
East Opening Relay	 | OFF   | <button>Toggle</button>
East Closing Relay	 | OFF   | <button>Toggle</button>
West Opening Relay	 | OFF   | <button>Toggle</button>
West Closing Relay	 | OFF   | <button>Toggle</button>
Open and Close East	 | OFF   | <button>Toggle</button>
Open and Close West	 | OFF   | <button>Toggle</button>
Garage Doors Reboot	 | OFF   | <button>Toggle</button>

The names and options against each row will vary based upon the name and types you specify in your configuration.yaml

### Accessing the Webserver API
Typically, I've created a shortcut to the dash and shared that to my home page. That's a single click to open it and see the states.

### Accessing directly using shortcuts
Add a shortcut (screenshot) that makes a post request.

### Accessing scripts
You can use `on_press:` to trigger a sequence of events upon trigger, but sometimes you won't have a direct 1:1 connection between a script and a GPIO device.

Currently, ESPHome does not seem to expose scripts through the API, so to trigger a series of events
use template switches.
