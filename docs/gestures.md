# 🤲 Gestures

Commands for playing and recording arm gestures.

---

### Playing Gestures

| Gesture | Joint Tested | Arms |
|---|---|---|
| `QT/happy` | Shoulder rotation | Both |
| `QT/clapping` | Elbow flexion | Both |
| `QT/bye` | Shoulder rotation | Right only |
```bash
rosservice call /qt_robot/gesture/play "name: 'QT/happy'
speed: 1.0"
```
```bash
rosservice call /qt_robot/gesture/play "name: 'QT/clapping'
speed: 1.0"
```
```bash
rosservice call /qt_robot/gesture/play "name: 'QT/bye'
speed: 1.0"
```

---


### Recording Your Own Gesture

> 📖 Reference: [LuxAI Create Your Own Gesture](https://docs.luxai.com/docs/v1/tutorials/python/python_ros_record)

#### Step 1 — Create the Python Package
```bash
cd ~/catkin_ws/src
catkin_create_pkg tutorial_qt_record rospy roscpp -D "Record new gestures"
cd tutorial_qt_record/src
touch tutorial_qt_record_node.py
chmod +x tutorial_qt_record_node.py
```

#### Step 2 — Add the Code

Open `tutorial_qt_record_node.py` and add the following:
```python
#!/usr/bin/env python3
import sys
import rospy
from qt_robot_interface.srv import *
from qt_gesture_controller.srv import *
from qt_motors_controller.srv import *
if __name__ == '__main__':
    rospy.init_node('my_tutorial_node')
    rospy.loginfo("my_tutorial_node started!")
    speechSay = rospy.ServiceProxy('/qt_robot/speech/say', speech_say)
    gestureRecord = rospy.ServiceProxy('/qt_robot/gesture/record', gesture_record)
    gestureSave = rospy.ServiceProxy('/qt_robot/gesture/save', gesture_save)
    setControlMode = rospy.ServiceProxy('/qt_robot/motors/setControlMode', set_control_mode)
    gesturePlay = rospy.ServiceProxy('/qt_robot/gesture/play', gesture_play)
    try:
        if len(sys.argv) < 2:
            rospy.logerr("Please provide a gesture name. Usage: python3 script.py <gesture_name>")
            sys.exit(1)
        name = sys.argv[1]
        parts = ["left_arm","right_arm","head"]
        input('Press enter to START recording ...\n')
        speechSay('Recording now.')
        res = gestureRecord(parts, True, 0, 0)
        if not res.status:
            rospy.logfatal("Could not start recording gesture '%s' using '%s'." % (name, parts))
        speechSay('When you want to STOP recording, just press enter again')
        input('Press enter to STOP recording ...\n')
        res = gestureSave(name, "")
        if not res.status:
            rospy.logfatal("Could not save gesture '%s'." % name)
        else:
            rospy.loginfo("Gesture '%s' was recorded." % name)
            speechSay("Your gesture %s was recorded." % name)
        res = setControlMode(parts, 1)
        if not res.status:
            rospy.logfatal("Could not set control mode of '%s'." % parts)
        else:
            speechSay("Let's see what did you record.")
            gesturePlay(name, 0)
    except KeyboardInterrupt:
        pass
    rospy.loginfo("finished!")
```

#### Step 3 — Run the Script

From the QTPC terminal, navigate to the script location and run it:

```bash
cd ~/catkin_ws/src/tutorial_qt_record/src
python3 tutorial_qt_record_node.py my_gesture
```

> 💡 **Tip:** Replace `my_gesture` with whatever you want to name your gesture. This will be the name of the saved XML file.
```

> 💡 **Tip:** Replace `my_gesture` with whatever you want to name your gesture. This will be the name of the saved XML file.

#### Step 4 — Verify and Move the Gesture File

After recording, check that the gesture was saved:
```bash
ssh developer@192.168.100.1
cd /home/qtrobot/robot/data/gestures
ls
```

Open a **new terminal** and test the gesture:
```bash
rosservice call /qt_robot/gesture/play "name: 'my_gesture'
speed: 1.0"
```

Once verified, move the file from the gestures folder to the `QT` subfolder:
```bash
# Copy to home directory first
sudo scp my_gesture.xml developer@192.168.100.1:/home/developer/

# Move to the QT folder
sudo mv /home/developer/my_gesture.xml /home/qtrobot/robot/data/gestures/QT/

# Delete the original
sudo rm /home/qtrobot/robot/data/gestures/my_gesture.xml
```

#### Step 5 — Clean Up / Remove a Gesture

From the QTRD terminal, remove the gesture file:
```bash
sudo rm /home/qtrobot/robot/data/gestures/QT/my_gesture.xml
```

> ⚠️ **Warning:** `rm` is permanent — double check the filename before running.




