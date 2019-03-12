# Absolute core (ABS) - build from source guide


## install build deps

	apt-get install nano wget mc dbus ufw fail2ban htop git pwgen automake -y
	apt-get install software-properties-common build-essential -y
	apt-get install libtool autotools-dev autoconf pkg-config libssl-dev -y
	apt-get install libevent-dev libboost-all-dev libminiupnpc-dev libzmq3-dev -y
	# on newer versions of ubuntu (17.x and newer) you need to install libssl1.0 -y
	apt-get install libssl1.0-dev -y

	# for QT GUI
	apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev -y
	apt-get install qttools5-dev-tools libprotobuf-dev protobuf-compiler libqrencode-dev -y

	# add bitcoin repo
	add-apt-repository ppa:bitcoin/bitcoin  
	apt-get update  
	apt-get install libdb4.8-dev libdb4.8++-dev



## create 2GB swap space

	#!/bin/sh
	dd if=/dev/zero of=/mnt/swap bs=1M count=2000
	mkswap /mnt/swap
	chmod 0600 /mnt/swap
	swapon /mnt/swap
	echo '/mnt/swap swap swap defaults 0 0' | sudo tee -a /etc/fstab
	sudo sysctl vm.swappiness=10
	echo "vm.swappiness = 10" >> /etc/sysctl.conf



## build script without QT GUI

	cd
	git clone https://github.com/absolute-community/Absolute-Combine.git AbsoluteTEMP
	cd AbsoluteTEMP
	chmod +x ./autogen.sh
	./autogen.sh
	./configure --without-gui
	chmod +x share/genbuild.sh
	chmod +x src/leveldb/build_detect_platform
	make
