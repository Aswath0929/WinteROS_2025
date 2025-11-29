# Configuring Environment

## Step 1
Source the setup files
```bash
source /opt/ros/jazzy/setup.bash
```
If you don't want to do this in every terminal session then run:
```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
```

## Step 2
Sourcing ROS2 setup files will set environment variables necessary for operating ROS2. Make sure your environment is properly set up usinng the following command:
```bash
printenv | grep -i ROS
```
Check that the variables like `ROS_DISTRO` and `ROS_VERSION` are set.
```bash
ROS_VERSION=2
ROS_PYTHON_VERSION=3
ROS_DISTRO=jazzy
```
If these variables are not set correctly, return to the ROS2 package installation and try again.

## Step 3
Set the `domain ID`. For more information go [here](https://docs.ros.org/en/jazzy/Concepts/Intermediate/About-Domain-ID.html).
Set the domain ID between **0 and 101**.

```bash
echo "export ROS_DOMAIN_ID=<your_domain_id>" >> ~/.bashrc
```

# Using `turtlesim`, `ros2`, and `rqt`
Turtlesim is a lightweight simulator for learning ROS 2. It illustrates what ROS 2 does at the most basic level to give you an idea of what you will do with a real robot or a robot simulation later on.

rqt is a graphical user interface (GUI) tool for ROS 2. Everything done in rqt can be done on the command line, but rqt provides a more user-friendly way to manipulate ROS 2 elements.

## Task 1
Installing turtlesim
```bash
sudo apt update
sudo apt install ros-jazzy-turtlesim
```

To check if the package is installed, run the following command:
```bash
ros2 pkg executables turtlesim
```
It should output:
```bash
turtlesim draw_square
turtlesim mimic
turtlesim turtle_teleop_key
turtlesim turtlesim_node
```

## Task 2
Running turtlesim
```bash
ros2 run turtlesim turtlesim_node
```

It will open a window:
![Turtlesim Window](../Images/week0_turtlesim.png)

Open a new terminal and run:
```bash
ros2 run turtlesim turtle_teleop_key
```

You will be able to move your turtle now through the terminal!!

## Task 3
Open a new terminal to install `rqt` and its plugins:
```bash
sudo apt update
sudo apt install '~nros-jazzy-rqt*'
```

To run `rqt` just run:
```bash
rqt
```

When running `rqt` for the first time, the window will be blank. Just select **Plugins > Services > Service Caller** from the menu bar on top.

> Note: It may take some time for rqt to locate all the plugins. If you click on Plugins but don’t see Services or any other options, you should close rqt and enter the command `rqt --force-discover` in your terminal.

![rqt window](../Images/week0_rqt_default.png)

Use the refresh button to the left of the **Service** dropdown list to ensure all the services of your turtlesim node are visible.

### Try the spawn service
Click on the **Service** dropdown and and select the `/spawn` service.

![rqt spawn service](../Images/week0_rqt_spawn1.png)

Give the new turtle a unique name, like `turtle2`, by double-clicking between the empty single quotes in the Expression column. You can see that this expression corresponds to the value of name and is of type string.

Next enter some valid coordinates at which to spawn the new turtle, like `x = 1.0` and `y = 1.0`.

> Note: If you try to spawn a new turtle with the same name as an existing turtle, like the default turtle1, you will get an error message in the terminal running turtlesim_node
> `[ERROR] [turtlesim]: A turtle named [turtle1] already exists`

If you're successful, you should see a new turtle spawn in your existing window!!!

### Remapping controls
You need a second teleop node in order to control `turtle2`. However, if you try to run the same command as before, you will notice that this one also controls `turtle1`. The way to change this behavior is by remapping the `cmd_vel` topic.

In a new terminal, run:
```bash
ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel
```
Now you can move `turtle2` in this terminal!!

---

This is it for the initial part of this ROS2 bootcamp. Stay tuned for next week!!
