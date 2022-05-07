# Masternode Setup Guide

### 1. Requirements
* 5 BNTU  
* VPS server
	* [Vultr](https://www.vultr.com/?ref=7684542)
	* [Digital Ocean](https://m.do.co/c/917baa6de4c8)
* SSH client ([Bitvise](https://www.bitvise.com/) for windows)
* Text Editor (e.g. Notepad)
___
### 2. Local wallet setup part 1 of 2  
Download latest wallet: [GitHub](https://github.com/CRYPT0BUNTU/buntu/releases)  

Open the wallet

 *Note: If you're setting up using an Ubuntu desktop wallet and you do not see the File, Settings, or Help wallet menu options then you must uninstall apppmenu-qt5 from your system (Terminal> sudo apt-get remove appmenu-qt5)*

Go to the `Receive` tab

Click `New Address` and enter a Masternode Address name (e.g. MN01) and click `OK` *(do not check `Stealth Address`)*  

Select the Masternode Address and click `Copy Address`. Paste the address in a text editor  

Click `New Address` again and enter a label for your Reward Address (e.g. Rewards1) and click `OK` *(do not check `Stealth Address`)*  

Select the Reward Address and click `Copy Address`. Paste the address in a text editor

Go to the `Send` tab

*Use "Coin Control" to select your collateral. If Coin Control is not visible, enable by navigating to menu >Options>Display*

Paste the address on the `Pay To` box and enter 5 in the `Amount` box  

*Note : You must be sent exactly 5 BNTU in a single transaction*  

Click `Send` *(do not check `Darksend`)*

Go to `Help` > `Debug window`  

Open `Console`and type `masternode genkey`

Copy the key and paste the masternode genkey (also referred later as a "PrivKey" or "Masternode Private Key") into your text editor  

Wait for 10 confirmations (Go to the next step while waiting)
___
### 3. Setup VPS   
Login to your VPS ([Vultr](https://www.vultr.com/?ref=7684542) or [Digital Ocean](https://m.do.co/c/917baa6de4c8)) using your SSH client
Deploy a new instance *(1GB RAM  VPS Recommended)*

Login to your instance using your SSH Client

#### 3-1. Installation  

Paste the applicable command below into your terminal to run the automated masternode installation script.
*these scripts automatically install the daemon and a bootstrap; therefore, they will take some time to run. Please be patient.*

Ubuntu 16.04 VPS:

Install dos2unix:
```
sudo apt-get install dos2unix -y

```
Run the setup commands:

```
wget -q https://github.com/CRYPT0BUNTU/buntu/releases/download/1.0/masternode1604.sh
chmod +x masternode1604.sh
dos2unix masternode1604.sh
bash masternode1604.sh

```  

Ubuntu 18.04 VPS:

Install dos2unix:
```
sudo apt-get install dos2unix -y

```
Run the setup commands:

```
wget -q https://github.com/CRYPT0BUNTU/buntu/releases/download/1.0/masternode1804.sh
chmod +x masternode1804.sh
dos2unix masternode1804.sh
bash masternode1804.sh

```  
Paste your masternode genkey when prompted


Ubuntu 20.04 VPS:

Masternodes built with Ubuntu 20.04 must be compiled manually. 

Follow the compilation instructions in the [Ubuntu 20.04 Build Guide](https://github.com/CRYPT0BUNTU/Buntu/blob/master/Ubuntu_20_04_Build.md)

Paste your masternode genkey in configuration file as detailed in the step, "Edit the config file"


#### VPS Masternode Troubleshooting

*Get the status code to identify issues:'./buntu masternode status'* 

The "status" of your masternode will be one of the following:

1 = Your masternode has not been processed by the network yet. Please wait.

2 = Your masternode is active and synced to the network.

3 = Your masternode is inactive.

4 = Your masternode has stopped.

5 = Your masternode seed transaction hasn't reached the minimum of 16 confirmations.

6 = Your masternode port is closed.

7 = Your masternode port is open.

8 = Your masternode is syncing to the network.

9 = Your masternode is remotely enabled and active.
___
### 4. Setup local wallet part 2 of 2  

After 10 confirmations type `masternode outputs` in the `Debug window` in your wallet

Copy the TxHash and output index number and paste it into your text editor

*the "Output Index" number is after the collateral tx and is either a "1" or "0"*
___
### 5. Create the Masternode  
Go to the `Masternodes` tab

Click the `Create...` button

Fill in the form using the instructions provided by the wallet. Use the information recorded in your text editor from previous steps.

Note: Be sure to add :32821 to the end of the VPS ip in the "Address" field!

Click `OK`  

Click `Update`  

Select your masternode
Click `Start`  

*Note: If you receive an error such as "Could not allocate VIN", unlock your wallet and click `Start` again.*
*If the error reoccurs then you may need to reinstall your VPS, remove the masternode (see below) from your masternode.conf file, and begin the setup from the beginning*

The above steps will create a 'masternode.conf' file in your %appdata% folder (windows).
Masternodes can be removed by editing or deleting file. Your collateral will reappear after you restart your wallet.

You may need to wait a few hours or even a day to receive rewards depending on the number of masternodes on the network.
___
### 6. Checking masternode status  
Click `Update` periodically to ensure your masternodes are running

After 30 minutes, your masternode `Active(secs)` will be reflected in the Buntu subtab

### Thank you for running a Buntu Masternode!
___
