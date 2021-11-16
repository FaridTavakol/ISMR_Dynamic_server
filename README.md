## Clone the repository to your home folder
git clone --recurse-submodules https://github.com/FaridTavakol/ISMR_Dynamic_server.git
## Build RBDL Library
### Go to your cloned folder 
cd ~/ISMR_Dynamics_server
### Run the setup script
cd rbdl-orb/

sudo sh setup.sh
## Copy the test_controller and ambf_control_system folders to the source directory of your catkin workspace
cd ~/ISMR_Dynamic_server

cp -r test_controller ~/catkin_ws/src

cp -r ambf_control_systems ~/catkin_ws/src
## Go to your catkin workspace and build the new packages
cd ~/catkin_ws

catkin_make
### Source setup.bash
source ~/catkin_ws/devel/setup.bash
### Run ROS master
roscore
### In another terminal run the RBDL Server Node
rosrun  rbdl_server   rbdl_server_node
### In another terminal run the Controller Node
rosrun test_controller_pkg control_node
### Run the custom robot file
cd ~/ambf/bin/  "yourOS"  /

./ambf_simulator -a   "location of the custom robot model.yaml"
### Finally, run the gravity compensation node by providing the file with the location of your robot config file ("robot.yaml")
rosrun  test_controller_pkg my_robot_gravity  "Address to your robot.yaml file"
