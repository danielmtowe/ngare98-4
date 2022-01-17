# How to install NVIDIA on Ubuntu 20.04 (enablling GPU)

First we find out what type of graphics card is attached to your system using the lshw command 


sudo lshw -C display


# Install Nvidia Driver
We can install the Nvidia drivers in multiple ways and from different sources.

1. Graphical Installation

2. Install Nvidia drivers from Ubuntu repository

i. ubuntu-drivers command

ii. apt command

3. Install Nvidia drivers from PPA

4. Install Nvidia drivers from Official site

1. Graphical Install
Go to Activities >> Software & Updates >> Additional Drivers.

This tab will display the available driver versions for your graphic card. Choose the suitable driver version you want to install or the recommended one (top of the list) and then click Apply Changes.

Enter the password to authenticate the driver installation. Then, wait for the installation to complete.

Reboot the system post the installation and then validate the driver installation by going again to the Additional Drivers tab.

After the system reboot, use the below command to validate the driver version.

sudo nvidia-smi



First, check if your system has secure boot enabled

sudo mokutil --sb-state

if the output is 
  SecureBoot enabled
  
Generate and import the MOK.


sudo openssl req -new -x509 -newkey rsa:2048 -keyout /var/tmp/MOK.priv -outform DER -out /var/tmp/MOK.der -days 36500 -subj "/CN=ubuntu/" -nodes
sudo mokutil --import /var/tmp/MOK.der


Convert .der file in to .pem format for Nvidia driver installation.

  openssl x509 -in /var/tmp/MOK.der -inform DER -outform PEM -out /var/tmp/MOK.pem
  
Reboot the system and then enroll MOK.

sudo reboot
Enroll Machine-Owner Key
Upon system reboot, you will need to perform MOK management.

Choose Enroll MOK » Continue » Yes » Enter Password (you have set earlier) » Reboot.

After the system reboot, validate the driver version on your Ubuntu system.

sudo nvidia-smi


# testing if GPU is working 
in terminal type 



import tensorflow as tf 
run 
tf.test.is_gpu_available()
or 
print (tf.config.list_physical_devices('GPU'))
or
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))
