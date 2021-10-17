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

todo...

### Accessing the Webserver API
Create a shortcut to the dash. That's a single click to open it and see the states.

### Accessing directly using shortcuts
Add a shortcut (screenshot) that makes a post request.

### Accessing scripts
use template switches.
