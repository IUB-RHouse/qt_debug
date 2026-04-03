> ⚠️ **Always ensure you are using QTrobot V1**
> 📖 Official Docs: [LuxAI Intro to Code (V1)](https://docs.luxai.com/docs/v1/intro_code)

---

## 🌐 Internet / WiFi Setup

### Step 1 — Access QTRP via SSH

From the Ubuntu desktop of QTPC, open a terminal and connect to QTRP:
```bash
ssh developer@192.168.100.1
# or
ssh developer@QTRP
```

> 🔑 Password: `qtrobot`

---

### Step 2 — Configure `wpa_supplicant` for `wlan0`

Edit the WiFi config file to update your network credentials:
```bash
cd /etc/wpa_supplicant
sudo nano wpa_supplicant-wlan0.conf
```

Set the `ssid` and `psk` for your router:
```bash
country=LU
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="<your router SSID>"
    psk="<your router passphrase>"
}
```

> ⚠️ **Warning — read carefully before saving:**
> - `ssid` and `psk` values must be wrapped in **double quotation marks**
> - There must be a `<TAB>` before `ssid` and `psk`
> - Do **not** create or modify any other `wpa_supplicant` or `systemd` network files — this may break your QTrobot network setup
> - Ensure you are editing `wpa_supplicant-wlan0.conf`, **not** `wpa_supplicant.conf`

#### Connecting to IU Network

If connecting to IU internet, use this configuration instead:
```bash
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=LU

# Home/office network (commented out)
#network={
#    ssid="JillsResidents"
#    psk="GuestWiFi"
#}

network={
    ssid="IU PublicNet"
    key_mgmt=NONE
}
```

---

### Step 3 — Restart `wpa_supplicant` and Verify Connectivity

From the QTRP SSH terminal, restart the service:
```bash
sudo systemctl restart wpa_supplicant@wlan0.service
```

Then verify internet access:
```bash
ping www.google.com
```

✅ If successful, QTrobot is connected to your network and has internet access.

---

## 🔊 Audio

### Speech
```bash
rosservice call /qt_robot/speech/say "message: 'The quick brown fox jumps over the lazy dog.'"
```
```bash
rosservice call /qt_robot/behavior/talkText "message: 'The quick brown fox jumps over the lazy dog.'"
```

### Volume Change
```bash
rosservice call /qt_robot/setting/setVolume "volume: 150"
```

### 🔈 Play Audio

> 📖 Reference: [LuxAI Speakers Module Docs](https://docs.luxai.com/docs/v1/modules/speakers)

#### Using Publisher
```bash
rostopic pub /qt_robot/audio/play std_msgs/String "data: 'QT/Komiku_Glouglou'"
```

#### Using Service Call
```bash
rosservice call /qt_robot/audio/play "filename: 'QT/Komiku_Glouglou'
filepath: ''"
```

> 💡 **Tip:** Use the publisher to trigger audio and keep moving, use the service call if you need to confirm playback completed before proceeding.
---

## 🤲 Gestures

> 📖 Reference: [LuxAI Create Your Own Gesture](https://docs.luxai.com/docs/v1/tutorials/python/python_ros_record)

### Both Arms Test
```bash
rosservice call /qt_robot/gesture/play "name: 'QT/happy'
speed: 1.0"
```
```bash
rosservice call /qt_robot/gesture/play "name: 'QT/clapping'
speed: 1.0"
```

### Right Arm Test
```bash
rosservice call /qt_robot/gesture/play "name: 'QT/bye'
speed: 1.0"
```

---

## 😊 Emotions

> 📖 Reference: [LuxAI Display Module Docs](https://docs.luxai.com/docs/v1/modules/display)

### Using Publisher
```bash
rostopic pub /qt_robot/emotion/show std_msgs/String "data: 'QT/happy'"
```

### Using Service Call
```bash
rosservice call /qt_robot/emotion/show "name: 'QT/happy'"
```

> 💡 **Tip:** Use the publisher to set an emotion and keep moving, use the service call if you need to confirm the emotion displayed before proceeding.
