### Setting up Reach networking

#### Powering up for the first time

When Reach is powered for the first time it will create a Wi-Fi hotspot. Open a list of Wi-Fi networks on your smartphone, tablet or laptop and connect to a network named **reach-part_of_mac_address**. Keep in mind that it takes some time for network to show up on your device after it's been created. Network password is "emlidreach".

For example:

![reach_network.png](img/reachview-app/reach_network.png)

#### Connecting Reach to your Wi-Fi network

After connecting to the network hosted by Reach, open a web browser on your smartphone, tablet or laptop and type either **http://reach.local:5000** or **http://192.168.42.1:5000** in the address bar. Choose your Wi-Fi network (e.g. a hotspot on your smartphone) and enter a password. Hit **Submit** and wait for a minute. Reach will disable its own hotspot and try to connect to your Wi-Fi network.

![reach_wifi_setup.png](img/reachview-app/reach_wifi_setup.png)

***Repeat all previous steps for both Reach devices.***

#### Resolving IP address

After connecting Reach to an existing network, you will need to find its IP address.

Good to remember:

* If you are on Reach's self-hosted network, its IP is always **192.168.42.1**
* If there is only one Reach unit on the network, it should be accessible by **reach.local** address

If these are not the case, you will need to scan your local network. In most of these apps, Reach units will show up as **Murata Manufacturing Co.** device.

* You can use the **Fing app** to scan your local network from your phone
* You can use **nmap** to scan your local network on Linux/Mac OS X. Nmap is cli tool available through most package managers like [homebrew](http://brew.sh) on Mac and **apt-get** on Debian based Linux distributions. Example of using nmap to perform host discovery would be `sudo nmap -sn 192.168.1.0/24`
* On Windows, you can use **Zenmap**, which is a GUI for **nmap** or use any other third-party network scanners.

For example - a screenshot of fing running on an iPhone:

![fing.png](img/reachview-app/fing.png)

### Working with ReachView app

#### Connecting to ReachView

Once you have the address, enter it into a browser. The app should work on most reasonably modern browsers, including those in phones and tablets.

The first thing you should see is a status tab:

![status_tab.png](img/reachview-app/status_tab.png)

***The interface might be updated and look slightly different***

As you can see, the default state for Reach is **stopped Rover**.

#### Interface walkthrough

ReachView consists of three main tabs: **Status**, **Config**, **Logs**. Status will show current satellite levels, solution status and coordinates. Config tab is used to set RTKLIB parameters like positioning mode, set correction input interface and more. Logs tab keeps links to raw data logs stored on the device and some other miscellaneous useful features.

***It is very important that you perform self-update during your first Reach use.***

#### Updating ReachView

To do this, make sure Reach is connected to a Wi-Fi network with Internet access. Go to the Logs page and press the **Update** button. ReachView will go inactive for about a minute. To reconnect, close the current tab and try to open ReachView in a new one. It is preferred to use Reach's IP address instead of **reach.local** to connect after an update.

![update.png](img/reachview-app/update.png)

<font color="red">***From this point, it is considered that you performed the update.***</font>