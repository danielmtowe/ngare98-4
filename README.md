# How to install NVIDIA on Ubuntu 20.04 (enablling GPU)

First we find out what type of graphics card is attached to your system using the lshw command 


- sudo lshw -C display


## Install Nvidia Driver
We can install the Nvidia drivers in multiple ways and from different sources.

1. Graphical Installation
2. Install Nvidia drivers from Ubuntu repository
  - ubuntu-drivers command
  - apt command

3. Install Nvidia drivers from PPA
4. Install Nvidia drivers from Official site

In this work we uses the first approach 

1. Graphical Install
Go to Activities >> Software & Updates >> Additional Drivers.

This tab will display the available driver versions for your graphic card. Choose the suitable driver version you want to install or the recommended one (top of the list) and then click Apply Changes.

Enter the password to authenticate the driver installation. Then, wait for the installation to complete.

Reboot the system

After the system reboot, use the below command to validate the driver version.

  - sudo nvidia-smi



First, check if your system has secure boot enabled

sudo mokutil --sb-state

if the output is " SecureBoot enabled "
  
Generate and import the MOK.


  - sudo openssl req -new -x509 -newkey rsa:2048 -keyout /var/tmp/MOK.priv -outform DER -out /var/tmp/MOK.der -days 36500 -subj "/CN=ubuntu/" -nodes
  - sudo mokutil --import /var/tmp/MOK.der


Convert .der file in to .pem format for Nvidia driver installation.

   - openssl x509 -in /var/tmp/MOK.der -inform DER -outform PEM -out /var/tmp/MOK.pem
  
Reboot the system and then enroll MOK.

  - sudo reboot
Enroll Machine-Owner Key
Upon system reboot, you will need to perform MOK management.

Choose Enroll MOK » Continue » Yes » Enter Password (you have set earlier) » Reboot.

After the system reboot, validate the driver version on your Ubuntu system.

sudo nvidia-smi


## Testing if GPU is working 
In terminal type the following command 

  - python 
  - import tensorflow as tf
  
then run 

  - tf.test.is_gpu_available()
  
or 

 - print (tf.config.list_physical_devices('GPU'))
 
or

 - print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))



# How to install mobius in Ubuntu 20.04 


Node JS installation

sudo apt-get install -y nodejs

sudo apt install npm


check the vision installed 

node -v
(v 10.19.0)


npm install 


### mysql installation

### MQTT server Installation

Mobius enables IoT devices to communicate with MQTT server through MQTT protocol. To use this function, an MQTT broker needs to be installed. 

It is installed through the command 
  - sudo apt-get install mosquitto
  - sudo apt-get install mosquitto-clients

To check the installed version of mosquito use the "mosquitto -v" command


After installed Mosquitto broker, you can test whether the Mosquitto broker works properly or not as follows:
Step -1: Subscription test
  - Open the Terminal Command and input command as below
    -- mosquitto_sub -h localhost -t /mytopic/1
Step -2: Notification test
  - Open the Terminal Command and input command as below
    -- mosquitto_pub -h localhost -t /mytopic/1 -m "Hello MQTT test"



### Node JS Installation

  - sudo apt-get install nodejs

you can checkk the version of nodejs installed thought the "node -v" command


### Mobius Installation

download the zipped packag from the Mobius GitHub (https://github.com/IoTKETI/Mobius )

After downloading, unzip the package and you will see the included folders and files as Figure

To install the required  additional node.js modules, open a Linux terminal window and go to the directory where the  unzipped package and run npm install command

After running the npm install command, all additional required node.js modules will be generated and stored in node_modules folder


configure the Mobius server in terms of communication port and CSE name e

### Running Mobius Server
A configuration file conf.json is included in the unzipped folder of Mobius package

sudo apt update

sudo apt install mysql-server

sudo mysql

select user, authentication_string, plugin from mysql.user;

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'mobius123';

FLUSH PRIVILEGES;

EXIT

now yo can not login directly 

sudo mysql
