Internet connection??




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

### Play Audio
```bash
rostopic pub /qt_robot/audio/play std_msgs/String "data: 'QT/Komiku_Glouglou'"
```


