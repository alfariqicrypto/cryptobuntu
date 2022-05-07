# Linux Build Instructions
Buntu requires
* openssl-1.0.2n
* berkeley 4.8 db
* boost 1.57.0
* miniupnpc

To install, first follow the instructions to install dependencies 18.04 then follow the compilation instructions.

  ## Dependencies (Ubuntu 20.04)

    sudo apt-get update && apt-get upgrade  
    sudo apt-get dist-upgrade
    sudo apt-get install git screen net-tools
    sudo apt-get install libzmq3-dev libminiupnpc-dev libevent-dev -y  
    sudo apt-get install build-essential libtool autotools-dev automake pkg-config -y  
    sudo apt-get install libevent-dev bsdmainutils software-properties-common -y   
    sudo apt-get update  
    sudo apt-get install libgmp3-dev
    sudo apt-get install libdb5.3++ unzip libzmq5 -y

    ##### Install openssl-1.0.2n on Ubuntu 20.04:
		cd ~
		sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
		echo "deb http://security.ubuntu.com/ubuntu bionic-security main" | sudo tee -a /etc/apt/sources.list
		sudo apt-get update && apt-cache policy libssl1.0-dev
		sudo apt-get install libssl1.0-dev
		wget http://www.openssl.org/source/openssl-1.0.2n.tar.gz
		tar -xvzf openssl-1.0.2n.tar.gz
		cd openssl-1.0.2n
		./config --prefix=/usr/
		make
		sudo make install
	  
	##### Install berkeley 4.8 db on Ubuntu 20.04:
		cd ~
		wget http://download.oracle.com/berkeley-db/db-4.8.30.tar.gz
		tar -xvzf db-4.8.30.tar.gz
		cd db-4.8.30
		sed -i 's/__atomic_compare_exchange/__atomic_compare_exchange_db/g' dbinc/atomic.h
		cd build_unix/
		../dist/configure --prefix=/usr/local --enable-cxx
		make
		sudo make install
		export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/lib"
		
	##### Install boost 1.57 on Ubuntu 20.04 (get some coffee, this will take a while):
		cd ~
		wget http://sourceforge.net/projects/boost/files/boost/1.57.0/boost_1_57_0.tar.gz
		tar -xvzf boost_1_57_0.tar.gz
		cd boost_1_57_0
		./bootstrap.sh
		./b2
		sudo ./b2 install
		sudo ldconfig
	      
#### Swapfile
	swapoff -a
    fallocate -l 4G /swapfile  
    chown root:root /swapfile  
    chmod 0600 /swapfile  
    sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"  
    mkswap /swapfile  
    swapon /swapfile    
    echo '/swapfile none swap sw 0 0' >> /etc/fstab

#####  Restart the system
    sudo reboot

#####  Download Source code
	cd ~
    sudo git clone https://github.com/CRYPT0BUNTU/Buntu.git

### Compiling  
    cd Buntu/src
    sudo make -f makefile.unix

	./buntud

##### Edit the config file  
    nano ~/.buntu/buntu.conf  

	Copy and paste the following:
	
	rpcuser=username(Configure your own)  
	rpcpassword=password(Configure your own)  
	rpcallowip=127.0.0.1  
	daemon=1  
	server=1  
	listen=1  
	logtimestamps=1  
	maxconnections=256  

	For masternodes, also add:

	masternode=1  
	masternodeprivkey=your private key
	masternodeaddr=your VPS IP:32822

#### Usage  
Start daemon

	./buntud  

Stop daemon

	./buntud stop  

Display information  

	./buntud help
	./buntud getinfo  
	./buntud getmininginfo  
	./buntud getblockcount  
	./buntud masternode status  
	./buntud masternode list  
___