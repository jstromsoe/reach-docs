### When to reflash the firmware

On this page you will find the information on how to reflash Reach firmware.
Please note that you don't need to do this unless you want to bring Reach to its initial state or new firmware image version is released.
Most new features are released via ReachView app updates that can be updated simply by pressing an "Update" button in its interface.
More information on how to update ReachView app is available in [ReachView App docs section](reachview-app.md).

##### Emlid Reach RTK firmware download

We provide a special, enhanced Intel Edison image with following changes:

* Pre-installed software, including RTKLIB, ReachView, socat and more
* Wi-Fi setup service(Creates an access point, if no known WiFi networks are found)
* Created user "reach" with set up passwords, permissions, etc.

While Reach units are flashed before shipping, we plan to update the image in the future. You can get the latest version here:

[**Reach Image v1.2**](http://files.emlid.com/data/public/43c706)

There are two ways to flash the image. Intel's GUI Phone Flash Tool Lite and a CLI script.

### Flashing process

#### GUI guide

###### Getting Intel Phone Flash Tool Lite

You can get the tool [here](https://software.intel.com/en-us/iot/hardware/edison/downloads). It is available for Windows, Mac and Linux.

###### Flashing Reach

Before flashing:

0. If you are running Windows, install [Intel Edison drivers](http://downloadmirror.intel.com/24909/eng/IntelEdisonDriverSetup1.2.1.exe)
1. Unzip the image
2. Open the Phone Flash Tool Lite
3. Choose correct path to the unzipped image(You will need to point it to a **.json** file inside)
4. Choose correct USB drivers. RNDIS for Windows, CDC for Mac and Linux

![preflash](img/firmware-reflashing/preflash.png)

After this:

1. Unplug Reach if it is plugged to this computer
2. Hit the blue **Start to flash** button
3. Plug Reach in
4. Monitor progress
5. Proceed to "After flashing"

![flash](img/firmware-reflashing/flash.png)

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
* Blinking <font color="yellow">Yellow</font> while looking for known networks
* <font color="green">Green</font> after creating a hotspot
