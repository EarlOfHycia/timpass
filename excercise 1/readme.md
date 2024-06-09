# Assignment 3 (ETHZ Exercise 1)

Download the smb_common zip file from ethz website and put the unzipped file in the local repo ~/git

Make a common workspace with a special sub workspace for smb_ws for out task and a mandatory src folder, using the command...

*mkdir -p ~/ws/smb_ws/src*

Make a symbolic link or symlink in the src folder of the unzipped smb_common folder in local git repo..
(for easier management of the packages without things getting messy),
using the command (make sure you are in the src directory)...

*ln -s ~/git/smb_common*

In the smb_ws run the command...

*catkin build*

Run the built smb_gazebo package using the command...

*roslaunch smb_gazebo smb_gazebo.launch*

Open another terminal to analyse the running nodes and topics

To get the list of running nodes use the command...

*rosnode list*

<img width="1352" alt="rosnode list" src="https://github.com/EarlOfHycia/timpass/assets/162675481/2b4b5f5c-f7c2-4059-874c-80756ae57e6b">


Similarly to get the list of all topics, use the command...

*rostopic list*

We know that to give command using the *rostopic pub* command we need the name of the topic to which /gazebo node subscribes
to via the /cmd_vel topic, we find the list of such topics by using the command...

*rostopic list | grep cmd_vel*
