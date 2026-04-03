# 😊 Emotions

> 📖 Reference: [LuxAI Display Module](https://docs.luxai.com/docs/v1/modules/display)

Commands for displaying emotions on QTrobot's screen.

---

### Using Publisher
```bash
rostopic pub /qt_robot/emotion/show std_msgs/String "data: 'QT/happy'"
```

### Using Service Call
```bash
rosservice call /qt_robot/emotion/show "name: 'QT/happy'"
```

> 💡 **Tip:** Use the publisher to set an emotion and keep moving, use the service call if you need to confirm the emotion displayed before proceeding.
