### Intro

In this quick tutorial we will show you how to two set up two Reach devices as a base and a rover with correction link over Wi-Fi.

> If you encounter any issues performing these steps, we will be happy to help at our [**community forums**](http://community.emlid.com/).

This tutorial only covers on use case. To get more information, follow these links:

* [Mechanical specs](mechanical-specs.md)
* [Electrical specs](electrical-specs.md)
* [Hardware integration](hardware-integration.md)
* [ReachView app](reachview-basics.md)

### Powering up

* Take **Micro-USB <--> USB cable** that is coming with the package.

* Plug **Micro-USB end** of the cable into **Micro-USB port** on Reach and plug another end into 5V power source such as USB power bank, USB wall adapter or USB port of a computer.

> <font color="red"> **IMPORTANT** </font>

> **Do not** plug two power supplies at the same time as it may damage the device.

More on power supply you can read [here](power-supply.md).

### Connecting and placing GPS antenna

* Plug antenna cable into MCX socket on Reach. 

* Place antenna on a ground plane. It could be a cut piece of metal > 100mm in diameter, roof of a car or metal roof of a building. 

> **IMPORTANT**

>There **should be no** obstacles near the antenna that could block the sky view higher than 30 degrees above horizon.

> **Do not** test the device indoors or near buildings, do not cover the skyview for the antennas with laptops, cars or yourself. RTK requires good satellite visibility and reception.

A guide how to properly place the antennas is available in [Antenna Placement](antenna-placement.md) section.

### Connecting to Reach

When Reach is powered for the first time it will create a Wi-Fi hotspot.

* Open a list of Wi-Fi networks on your smartphone, tablet or laptop.

* Connect to a network named **reach:xx:xx** (ex. reach:66:ac).

* Type network password: **emlidreach**.

> If this password is not accepted, probably your Reach has been flashed with a bugged firmware, please [reflash](firmware-reflashing.md) with the latest image.

### Setting up Wi-Fi

After connecting to the network hosted by reach, open a web browser on your smartphone, tablet or laptop.    

* Type either **http://reach.local** or **http://192.168.42.1** in the address bar and you will see ReachView Updater.

![reach_view_updater_main.png](img/quickstart/reach_view_updater_main.png) 

* Press plus button and enter your Wi-Fi network name, security type and password. Press Save button

![reach_view_updater_wifi.png](img/quickstart/reach_view_updater_wifi.png) 

* Press on your added network and click Connect. 

![reach_view_updater_wifi_connect.png](img/quickstart/reach_view_updater_wifi_connect.png)    

* After that Reach device will reboot and connect to your Wi-Fi network.

> **IMPORTANT**

> If your device do not connect to Wi-Fi network, check your name and password once again.    
> You can find Reach on **http://reach.local** or **http://192.168.42.1** as usual in hotspot mode.

### Accessing Reach device in a network

After connecting Reach device to an existing Wi-Fi network, you will need to identify it IP.    

For this you can use:    

* "**Fing**" app for [iOS](https://goo.gl/Ho0qB) or [Android](https://goo.gl/7Wuwu).

* ["**Nmap**"](https://nmap.org/) on Linux/OS X.

* ["**Zenmap**"](https://nmap.org/zenmap/) on Windows. 

![fing.png](img/quickstart/fing.png)

* Reach will show up as "**Murata Manufacturing**" device in these apps.

* Put Reach IP in address bar and go.

> If your device supports Bonjour discovery, you can access Reach with **http://reach.local**.
> However, **with two** devices on the network **only one** will respond to such address.

Read more on resolving IP addresses in the [ReachView section](reachview-basics.md).    

* After that you will see ReachView Updater again which will test your device and check for updates.

> In ReachView we have automatic notification about updates.    
> You can also check :5000 port fo them in the future.

![reach_view_updater_finish.png](img/quickstart/reach_view_updater_finish.png)

* Press **Reboot and go to the app!** button if everything is OK.

* Refresh page when you will see green led on your device, which means that it is ready to go.

* Here's our ReachView app is loading!

![reach_view_loading.png](img/quickstart/reach_view_loading.png)


### Working with ReachView app


#### Interface walkthrough

![reach_view_status_menu.png](img/quickstart/reach_view_status_menu.png)

ReachView menu consists of 9 tabs, but we only need three of them to start work:    

* **Status** tab which shows current satellite levels, RTK parameters, coordinates and map.

* **Base mode** tab is used to set base mode, coordinates and RTCM3 messages.

* **Correction input** tab is used to set base correction for the rover.

#### Setting up base station

* Connect to Reach you want to use as a base.

* Navigate to **Base mode** tab and turn on Correction output box toggle.

* Wait until base will average it's position in Base ccordinates box.

![reach_view_base_mode_menu.png](img/quickstart/reach_view_base_mode_menu.png)

By default, base output stream will be available on a **TCP port 9000**.


#### Setting up rover

* Connect to the second Reach. 

* Navigate to **Correction input** tab. 

![reach_view_correction_input_tab.png](img/quickstart/reach_view_correction_input_tab.png)

* Choose TCP correction mode.

* Choose **Client** in **Role** field.

* Add base IP in **Address** field.

* Add base correction port in **Port** field. Default one is **9000**.

* Choose correction input **Format**. Default one is **RTCM3**. 

![reach_view_correction_input_tcp.png](img/quickstart/reach_view_correction_input_tcp.png)

* Save settings by pushing **Save** button.


#### Viewing results

* Go to **Status** tab of the app on the rover device.

![reach_view_status_menu_correction.png](img/quickstart/reach_view_status_menu_correction.png)

You can see a bar chart with satellite levels, RTK parameters, positioning mode and solution status, current coordinates of rover and base in LLH format, velocity and map. In this quick tutorial, positioning mode is set to "Kinematic" which is the main RTK mode.

* If everything has been set up correctly, **Solution status** will be **Float** and **you should see grey bars near satellite levels bars**. 

> **Float** means that base corrections are now taken into consideration and positioning is relative to base coordinates, but the integer ambiguity is not resolved.    

> If you see **"-"** or **Single** in **Solution status** box on this step, that means that some settings are incorrect.    
> **"-"** means there is no information for the software to process. Either not enough time has passed or the antenna is not placed correctly.    
> **Single** means that rover has found a solution relying on it's own receiver and base corrections are not taken into consideration yet. If rover is started in single mode, this will also be the result.

* Wait until **Solution status** will be **Fix**. It should happen when AR validation ratio in RTK parameters box will be more than 3.    

> **Fix** means that positioning is relative to the base and the integer ambiguity is properly resolved.    

> There's no default time for getting **Fix** because it depends on various factors.    
> Remember that satellite levels and therefore antenna placement severely affect RTK performance.       
> You need at least 5 satellites with SNR levels over 45 (marked green on the chart) to get RTK improved solution.

![reach_view_status_menu_fix.png](img/quickstart/reach_view_status_menu_fix.png)

* Now you can see green points on the map below.

* You're ready to go!

### More reading

Congratulations on finishing the quickstart tutorial! Continue to learn about setting up different correction links in the [ReachView section](reachview-basics.md).
