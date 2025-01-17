# Design To Production - Device Proxy installation
## Pre Installation
### Updating an Existing Installation

Stop, disable and delete the depricated deviceProxy.service
<pre>
sudo systemctl stop deviceProxy.service
sudo systemctl disable deviceProxy.service
sudo rm /etc/systemd/system/deviceProxy.service
</pre>

## Installation

To install the D2P device proxy repo on your PC you need to get the following file from the apt-dev repo
<pre>
sudo wget https://design2production.github.io/apt-dev/install-dp-device-proxy.sh
</pre>

If you get an error about wget not being able to verify the github.io certificates, ensure the certificates are installed and being used for wget
<pre>
sudo apt install ca-certificates
printf "\nca_directory=/etc/ssl/certs" | sudo tee -a /etc/wgetrc
</pre>

Next execute the installation script

Shopper Indoor testing
<pre>
sudo sh ./install-dp-device-proxy.sh testing Staging DPEMS-V1_DBV2 new smg-pc-mac-address
</pre>

Shopper Outdoor testing
<pre>
sudo sh ./install-dp-device-proxy.sh testing Staging DPEMS-V2 new smg-pc-mac-address
</pre>

Shopper Indoor producton
<pre>
sudo sh ./install-dp-device-proxy.sh stable Production DPEMS-V1_DBV2 new smg-pc-mac-address
</pre>

Shopper Outdoor production
<pre>
sudo sh ./install-dp-device-proxy.sh stable Production DPEMS-V2 new smg-pc-mac-address
</pre>

Allowed parameters.

<pre>
sudo sh ./install-dp-device-proxy.sh stable|testing Production|Staging DPEMS-V1|DPEMS-V1_DBV2|DPEMS-V1_DBV3|DPEMS-V1_FANEXT|DPEMS-V2 new|oldInstallationFolder deviceId
</pre>

The arguments being passed in are:

Release:
- stable
- testing

Remote Server:
- Production
- Staging

Hardware Configuration: 
- DPEMS-V1
- DPEMS-V1_DBV2
- DPEMS-V1_DBV3
- DPEMS-V1_FANEXT
- DPEMS-V2

Installation Type:
- new
- ***old Installation Folder***

Device Id:
- unique device Id, usually the name of the pc or mac address

Use the arguments based on the device you are installing the proxy on.

***Shopper Indoor Units are DPEMS-V1_DBV2***

***Shopper Outdoor Units are DPEMS-V2***

For new feature development as well as pre-production testing

***testing*** and ***Staging*** should be used along with the hardware configuration for the device.

For new machine installation and updating existing machines

***stable*** and ***Production*** should be used along with the hardware configuration for the device.

Once the installation script is completed, you can check that the new proxy is running by executing

<pre>
sudo systemctl status dp-device-proxy
</pre>

And you should see something like
<pre>
● dp-device-proxy.service - DeviceProxy
   Loaded: loaded (/etc/systemd/system/dp-device-proxy.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2022-08-15 16:30:58 AEST; 19h ago
 Main PID: 3487 (DeviceProxy)
    Tasks: 23 (limit: 4569)
   CGroup: /system.slice/dp-device-proxy.service
           └─3487 /usr/lib/dp-device-proxy/DeviceProxy

</pre>

Along with some additional recent logs.

## Updates
Use the standard apt update system to the latest version
<pre>
sudo apt update
sudo apt install dp-device-proxy
</pre>

And to a specific version
<pre>
sudo apt update
sudo apt install dp-device-proxy=1.7.5-5
</pre>

## Post Installation
Delete the Old Installation.
<pre>
sudo rm -r <i><b>ExistingInstallationFolder</b></i>
</pre>

