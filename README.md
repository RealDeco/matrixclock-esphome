
# 🕒 Matrix Clock with MAX7219

A simple yet nice-looking **Matrix Clock** built using **MAX7219 dot matrix displays** and esp32-c3 supermini.

Nothing groundbreaking here — it’s just a digital clock that:

* Keeps time over NTP (or from home assistant)
* Listens to MQTT for messages
* Scrolls any received text across the display


<img width="1024" height="1024" alt="Matrix Clock preview" src="https://github.com/user-attachments/assets/81570a0f-60f7-4607-b54b-495173f3b5ba" />

---

## 📖 Background

I’ve been using [this ESP8266 NTP Clock project](https://github.com/JXGA/ESP8266-NTP-Clock) for years and it works great for showing what is playing on the radio and so on..

This time, I wanted to run it on an **ESP32-C3 SuperMini** and instead of porting the old code, I wrote a simple **ESPHome YAML config** that replicates the same functionality.

---

## 🔧 Hardware Setup

ESP32-C3 SuperMini + MAX7219 dot matrix display:

<img width="1375" height="1126" alt="MAX7219 with ESP32-C3 wiring" src="https://github.com/user-attachments/assets/c8bac4e1-fcc6-4bc9-9245-5c1c649b411e" />

parts:

MAX7210: https://www.aliexpress.com/item/1005008005112441.html (comes with cable)

ESP32-C3 Supermini: https://www.aliexpress.com/item/1005005967641936.html

---

## ⚙️ Installation

### 1. Fonts

Make sure you have these fonts in your ESPHome `fonts` directory:

```
fonts/Eight-Bit-Dragon.ttf
fonts/5x8.bdf
```

### 2. Secrets

In ESPHome, set the following **secrets** (top-right corner in the ESPHome dashboard):

```yaml
mqtt_username: "your-mqtt-username"
mqtt_password: "your-mqtt-password"
```

### 3. Configuration

At the top of your YAML script, define your MQTT broker and topic:

```yaml
mqtt_broker: 10.66.66.12
mqtt_topic: "matrixclock-1"
```

*(You can leave the topic as-is unless you plan to run multiple clocks.)*

compile! (install) :)
---

