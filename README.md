
# 🕒 Matrix Clock for Esphome with MAX7219

A simple yet nice-looking **Matrix Clock** built using **MAX7219 dot matrix displays** and esp32-c3 supermini.

Nothing groundbreaking here — it’s just a digital clock that:

* Keeps time over NTP (or from home assistant)
* Listens to MQTT for messages
* Scrolls any received text across the display
* Runs with or without Home Assistant

<p align="center">
  <img src="https://github.com/user-attachments/assets/81570a0f-60f7-4607-b54b-495173f3b5ba" alt="Matrix Clock preview" width="500"/>
  <img src="https://github.com/user-attachments/assets/7f054f3b-f26c-47f8-9664-c826921ed674" alt="unnamed-2" width="500"/>
</p>
---

## 📖 Background

I’ve been using [this ESP8266 NTP Clock project](https://github.com/JXGA/ESP8266-NTP-Clock) for years and it works great for showing what is playing on the radio and so on..

This time, I wanted to run it on an **ESP32-C3 SuperMini** and instead of porting the old code, I wrote a simple **ESPHome YAML config** that replicates the same functionality.

---

## 🔧 Hardware Setup

ESP32-C3 SuperMini + MAX7219 dot matrix display:

<img width="1375" height="1126" alt="MAX7219 with ESP32-C3 wiring" src="https://github.com/user-attachments/assets/793786bd-a283-41f0-a64a-3bc666f463f3" />

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

At the top of your YAML script you will find this, change IP to your MQTT broker

if using several clocks, change topic for each

other settings can be left as they are if you followed the diagram:

```yaml
  mqtt_broker: 10.66.66.12
  mqtt_topic: "matrixclock-1"

  pin_mosi: GPIO8
  pin_cs:   GPIO9
  pin_sck:  GPIO10

  num_chips: "4"

  scroll_delay_ms: "20" 
```

(*chips = number of max7219 sections on the board, usually 4, but could be 8*)

### 4. Configuration

compile (install) and you are done! :)

---

## ⚙️ Testing MQTT

To test, go to developer tools, actions, and publish (mqtt.publish) this:

```yaml
action: mqtt.publish
data:
  evaluate_payload: false
  qos: 0
  retain: false
  topic: matrixclock-1/scroll
  payload: "testing scrolling text and the speed TESTING TESTING TESTING "
```
