### Simulation

To start docker, in the rosject terminal, run:

	sudo apt-get update
	sudo apt-get install -y docker.io docker-compose
	sudo service docker start
	sudo usermod -aG docker $USER
	newgrp docker

Note, to access docker in a new terminal, there's no need to reinstall, so just run:

    sudo service docker start
	sudo usermod -aG docker $USER
	newgrp docker

Then, to start the fastbot simulation, slam, and website, in the rosject terminal, run: 

	cd ~/ros2_ws/src/fastbot_ros2_docker/simulation
	docker-compose up

Bear in mind, it will take a little over a minute to spool up. Eventually, in the graphical window display, you should see the simulation environment and the fastbot. 

To access the website, in the rosject terminal, run

	webpage_address

Copy the provided link, and enter it into a web browser

Then, in the rosject terminal, run

	rosbridge_address

Copy the provided link, and paste it into the rosbridge_address box on the webpage. Then hit connect.

Now, you should be able to see a joystick to control the robot, a map that can be generated as the robot moves, a 3d viewer, and a live camera.

  

### Real

Note: This assumes your fastbot's Raspberry PI is set up according to the assembly guidelines provided by The Construct and has docker installed. It also assumes the machine you're using to ssh into your PI is connected to the PI over a LAN to allow for ros2 topic discovery, and has ros2 and rviz2 installed. Thus, you should already be able to run a ros node on your PI and be able to see the topics and visualize them in Rviz on your external computer that sshes into your PI.

To start the real fastbot drivers and slam, first ssh into your fastbot.

Then, in your desired workspace's src folder (eg ~/ros2_ws/src), execute:

	git clone https://github.com/FrankWSFO/docker-basics-for-robotics-project.git
	cd docker-basics-for-robotics-project/real
	docker-compose up

To access the ros topics within the fastbot, in a terminal ssh'd into it, execute:

	export ROS_DOMAIN_ID=0
    export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
    source /opt/ros/humble/setup.bash
	ros2 topic list

And in a terminal on your external computer, to get access to the topics of your fastbot, execute:

	export ROS_DOMAIN_ID=0
	export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
    source /opt/ros/<ros-distro>/setup.bash
	ros2 topic list

Finally, to visualize the mapping, in your desired folder (eg ~/ros2_ws/src), run:

    git clone https://github.com/FrankWSFO/docker-basics-for-robotics-project.git
	rviz2 -d ./docker-basics-for-robotics-project/rviz/cartography.rviz