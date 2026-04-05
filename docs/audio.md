# 🔊 Audio

Commands for speech, volume control, and audio playback.

---

### Speech

#### `speech/say` — Robot speaks without mouth animation
```bash
rosservice call /qt_robot/speech/say "message: 'The quick brown fox jumps over the lazy dog.'"
```

#### `behavior/talkText` — Robot speaks with animated mouth
```bash
rosservice call /qt_robot/behavior/talkText "message: 'The quick brown fox jumps over the lazy dog.'"
```

### Volume Change
```bash
rosservice call /qt_robot/setting/setVolume "volume: 150"
```

### Play Audio (e.g., mp3)

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
