# 🤲 Gestures

Commands for playing and recording arm gestures.

---

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

### Recording Your Own Gesture

> 📖 Reference: [LuxAI Create Your Own Gesture](https://docs.luxai.com/docs/v1/tutorials/python/python_ros_record)
>
> ```bash
rosservice call /qt_robot/gesture/play "name: 'my_gestures'
speed: 1.0"
```
