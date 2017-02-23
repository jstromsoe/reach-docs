### When to reflash the firmware

On this page you will find the information on how to reflash Reach firmware.
Please note that you don't need to do this unless you want to bring Reach to its initial state or new firmware image version is released.
Most new features are released via ReachView app updates that can be updated simply by pressing an "Update" button in its interface.
More information on how to update ReachView app is available in [ReachView App docs section](reachview-basics.md).

##### Emlid Reach RTK firmware download

We provide a special, enhanced Intel Edison image with following changes:

* Pre-installed software, including RTKLIB, ReachView, socat and more
* Wi-Fi setup service(Creates an access point, if no known WiFi networks are found)
* Created user "reach" with set up passwords, permissions, etc.

While Reach units are flashed before shipping, we plan to update the image in the future. You can get the latest version here:

[**Reach Image v1.2**](https://files.emlid.com/images/ReachImage_v1.2.zip)

[**Reach Image v2.3(beta)**](https://files.emlid.com/images/ReachImage_v2.3.zip)

There are two ways to flash the image. Intel's Edison Board Configuration Tool and a CLI script.

### Flashing process

#### GUI guide

##### Getting Intel Edison Board Configuration Tool

You can get the tool [here](https://software.intel.com/en-us/iot/hardware/edison/downloads). It is available for Windows, Mac and Linux.

##### Flashing Reach

- Plug Reach to this computer 
- Unzip the image 
- Run Intel Edison Board Configuration Tool. Hit **Next**

![Welcome](img/firmware-reflashing/welcome.png)

- Read License Agreement, accept the terms of the License and hit **Next** twice

![License](img/firmware-reflashing/license.png)

- Install drivers (**Only for Windows**) 

![setupopt](img/firmware-reflashing/setupopt.png)

- After installation hit **Flash Firmware**

![setupopt_drv](img/firmware-reflashing/setup_with_drivers.png)

- Choose second item: **Use existing image, located at:**  
- Choose correct path to the unzipped image (You will need to point it to a **.json** file for Windows and **.hddimg** for Linux)  
- Hit **Next** twice

![preflash](img/firmware-reflashing/choose_img.png)

- Proceed to "After flashing"

#### Terminal guide

###### Windows

Before flashing:

* Install [Intel Edison drivers](http://downloadmirror.intel.com/24909/eng/IntelEdisonDriverSetup1.2.1.exe)
* Unzip downloaded image
* Unplug Reach if it's plugged in

To flash:

1. `cd` into the image directory
2. Run `flashall.bat`
3. Plug Reach in
4. Monitor progress in the terminal window
5. Proceed to "After flashing"

###### Mac OS X

Before flashing:

* Unzip downloaded image
* Install **[homebrew](http://brew.sh)**
* Install dependencies with `brew install dfu-util coreutils gnu-getopt`
* Unplug Reach if it's plugged in

To flash:

1. `cd` into the image directory
2. Run `sudo ./flashall.sh`
3. Plug Reach in
4. Monitor progress in the terminal window
5. Proceed to "After flashing"

###### Linux

Before flashing:

* Unzip downloaded image
* Unplug Reach if it's plugged in

To flash:

1. `cd` into the image directory
2. Run `sudo ./flashall.sh`
3. Plug Reach in
4. Monitor progress in the terminal window
5. Proceed to "After flashing"

### After flashing

After the initial process is done, Reach will reboot. **Do not unplug it until it reboots and goes through the initial setup process completely**.

Since image version **1.2**, the LED signals during startup are as follows:

* <font color="magenta">Magenta</font> during device boot
* Off, then White for a second to show script start
* Blinking <font color="yellow" style="background-color: grey;">Yellow</font> while looking for known networks
* <font color="green">Green</font> after creating a hotspot
