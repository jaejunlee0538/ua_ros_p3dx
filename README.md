## How to run
### 1. control with ros_control

```shell
Open a new terminal window.
$ roslaunch p3dx_gazebo gazebo.launch

Open a new terminal window.
$ roslaunch p3dx_control control.launch

Open a new terminal window.
$ roslaunch p3dx_description rviz.launch
```

**P3DX in Gazebo**

![p3dx_in_gazebo]

**P3DX in Rviz**

![p3dx_in_rviz]

```xml
<transmission name="${parent}_${suffix}_wheel_trans">
<type>pr2_mechanism_model/SimpleTransmission</type>
<joint name="base_${suffix}_wheel_joint">
	<hardwareInterface>EffortJointInterface</hardwareInterface>
</joint>
<actuator name="base_${suffix}_wheel_motor">
  <hardwareInterface>EffortJointInterface</hardwareInterface>
  <mechanicalReduction>${reflect * 624/35 * 80/19}</mechanicalReduction>
</actuator>
</transmission>
```

Now two actuators are located at left/right wheel joints respectively and ros_control has controls of them.  
To give commands to them, you have to publish the following topics.

```
/p3dx/joint1_position_controller/command
/p3dx/joint2_position_controller/command
```

Each topic represent desired positions of each wheel joints.

To make it easy to publish the topics, you can use rqt_gui.

```shell
$ rosrun rqt_gui rqt_gui
```

By loading appropriate plugins, you can publish topics in easy and intuitive way.

**rqt gui for ros control**

![rqt_gui_for_ros_control]

### 2. control with `/p3dx/vel_cmd` msg

**When the position_controller is up, `/p3dx/vel_cmd` has no effect**

```shell
Open a new terminal window.
$ roslaunch p3dx_gazebo gazebo.launch

Open a new terminal window.
$ rosrun rqt_gui rqt_gui

Open a new terminal window.
$ roslaunch p3dx_description rviz.launch
```

Turn on rqt_gui and loading relevant plugins.

```shell
$ rosrun rqt_gui rqt_gui
```

**rqt gui for DiffDrivePlugin**

![rqt_gui_for_DiffDrivePlugin]

If more information about DiffDrivePlugin, visit [here](https://github.com/jaejunlee0538/gazebo_personal_tutorial/blob/master/move_pioneer2dx/README.md)

[p3dx_in_gazebo]:https://raw.github.com/jaejunlee0538/ua_ros_p3dx/master/readme/pictures/p3dx_in_gazebo.png
[p3dx_in_rviz]:https://raw.github.com/jaejunlee0538/ua_ros_p3dx/master/readme/pictures/p3dx_in_rviz.png
[rqt_gui_for_DiffDrivePlugin]:https://raw.github.com/jaejunlee0538/ua_ros_p3dx/master/readme/pictures/rqt_gui_for_DiffDrivePlugin.png
[rqt_gui_for_ros_control]:https://raw.github.com/jaejunlee0538/ua_ros_p3dx/master/readme/pictures/rqt_gui_for_ros_control.png

##what is libgazebo_ros_p3d.so?
You can find source code from [gzebo_ros_pkgs](https://github.com/ros-simulation/gazebo_ros_pkgs) repository.

Go to `gazebo_plugins/include/gazebo_plugins/gazebo_ros_p3d.h`.

```
/*
BriefNote:
Compute relative position of [bodyName] frame with respect to [frameName] frame.
And publish it as [topicName] with [updateRate].
It seems that it does not have physical control of the model.
*/
```
