# Linux Build Instructions
Buntu requires
* openssl-1.0.2n
* berkeley 4.8 db
* boost 1.57
* miniupnpc

To install, first follow the instructions to install dependencies 18.04 then follow the compilation instructions.

  ## Dependencies (Ubuntu 18.04)

    sudo apt-get update && apt-get upgrade  
    sudo apt-get dist-upgrade
    sudo apt-get install git screen net-tools
    sudo apt-get install libzmq3-dev libminiupnpc-dev libevent-dev -y  
    sudo apt-get install build-essential libtool autotools-dev automake pkg-config -y  
    sudo apt-get install libevent-dev bsdmainutils software-properties-common -y  
    sudo apt-get install libboost-all-dev -y  
    sudo add-apt-repository ppa:bitcoin/bitcoin  
    sudo apt-get update  
    sudo apt-get install libdb4.8-dev libdb4.8++-dev  -y  
    sudo apt-get install libgmp3-dev
    sudo apt-get install libdb5.3++ unzip libzmq5 -y

    ##### Special instructions for openssl-1.0.2n on Ubuntu 18.04:
      wget http://www.openssl.org/source/openssl-1.0.2n.tar.gz
      tar -xvzf openssl-1.0.2n.tar.gz
      cd openssl-1.0.2n
      ./config --prefix=/usr/
      make
      sudo make install
      
#### Swapfile
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
    sudo git clone https://github.com/CRYPT0BUNTU/Buntu.git

### Compiling  
    cd Buntu/src
    sudo make -f makefile.unix  

##### Edit the config file  
    nano ~/.buntu/buntu.conf  

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
masternodeaddr=your VPS IP:32821

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
