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

To start the real fastbot drivers and slam, first ssh into your fastbot.

Then, in your desired workspace's src folder (eg ~/ros2_ws/src), execute:

	git clone https://github.com/FrankWSFO/docker-basics-for-robotics-project.git
	cd docker-basics-for-robotics-project/real
	docker-compose up

To access the ros topics within the fastbot, in a terminal ssh'd into it, execute:

	export ROS_DOMAIN_ID=1
	ros2 topic list

Note: One must always export the ROS_DOMAIN_ID to be 1 to be on the same communication channel when in a new fastbot terminal (or if one would like to automatically get access, add it to the end of your ~/.bashrc)

Then in a terminal on this rosject, to get access to the topics of your fastbot, execute:

	export ROS_DOMAIN_ID=1
	export CYCLONEDDS_URI=file:///var/lib/theconstruct.rrl/cyclonedds.xml
	ros2 topic list

And to visualize the mapping, in this rosject, run:

	rviz2 -d ~/temp_ws/src/ros2-ws-the-construct-web-development-project/fastbot_slam/rviz/cartography.rviz