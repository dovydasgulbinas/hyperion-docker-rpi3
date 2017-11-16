INFO:

	{{ DATA THAT IS CUSTOM GOES HERE }}.

Getting most recent docker hash:
	
	docker ps -q 

Getting docker hash simple way:

	docker ps -a


0. Plugin your usb device and determine its port.

	https://stackoverflow.com/questions/24225647/docker-any-way-to-give-access-to-host-usb-or-serial-device#24231872


1. create basic container with docker

	docker pull resin/rpi-raspbian
	docker run -t -i --name=test-hyperion-rpi  --device={{ /dev/ttyUSB0 }} resin/rpi-raspbian bash -c 'ping 127.0.0.1'


1 1/2. detach from docker and start it again

	ctrl + d
	docker start test-hyperion-rpi


2.  attach to that container

	docker exec -it test-hyperion-rpi bash


3. do dependency installation

	apt-get update
	apt-get upgrade
	apt-get install -y wget curl usbutils


4. install actual hyperion script
	
	cd ~
	wget https://raw.githubusercontent.com/megamorphf/hyperion-docker-rpi3/master/install_hyperion_rpi.sh
	chmod +x install_hyperion_rpi.sh
	sh ./install_hyperion_rpi.sh


5. go to install direcory and test hyperion

	cd /usr/share/hyperion/bin
	hyperion-remote
