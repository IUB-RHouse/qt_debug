# 🔊 Audio

Commands for speech, volume control, and audio playback.

---

### Speech

| Command | Behavior |
|---|---|
| `speech/say` | Speaks without mouth animation |
| `behavior/talkText` | Speaks with animated mouth |
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

### Play Audio

> 📖 Reference: [LuxAI Speakers Module Docs](https://docs.luxai.com/docs/v1/modules/speakers)

| Method | When to Use |
|---|---|
| Publisher | Trigger audio and keep moving |
| Service Call | Wait for playback to complete |
```bash
rostopic pub /qt_robot/audio/play std_msgs/String "data: 'QT/Komiku_Glouglou'"
```
```bash
rosservice call /qt_robot/audio/play "filename: 'QT/Komiku_Glouglou'
filepath: ''"
```
