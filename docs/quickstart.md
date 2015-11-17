### Powering up

Take Micro-USB<-->USB cable that is coming with the package. Plug Micro-USB end of the cable into Micro-USB port on Reach and plug another end into 5V power source such as USB power bank, USB wall adapter or USB port of a computer.

### Connecting and placing antenna

Plug antenna cable into MCX socket on Reach. Place antenna on a ground plane. It could be a cut piece of metal > 100mm in diameter, roof of a car or metal roof of a building. There should be no obstacles near the antenna that could block the sky view higher than 30 degrees above horizon.

### Connecting to Reach

When Reach is powered for the first time it will create a Wi-Fi hotspot. Open a list of Wi-Fi networks on your smartphone, tablet or laptop and connect to a network named "reach-something".

### Accessing Reach device in a network

If you have a smartphone \ tablet \ laptop with Bonjour service running on it such as iPhone, Mac you can access Reach by using address "reach.local".
If your OS is Android use an app called Fing to find IP addresses of Reach devices in the network. Note that Reach units will probably show up as "Murata manufacturing" devices in the app.

### Setting up Wi-Fi

After connecting to the network hosted by reach, open a web browser on your smartphone, tablet or laptop and type either **http://reach.local:5000** or **http://192.168.42.1:5000** in the address bar. Choose your Wi-Fi network (e.g. a hotspot on your smartphone) "mywifinetwork" and enter a password. Hit submit and wait for a minute. Reach will disable its own hotspot and try to connect to your Wi-Fi network.

***Repeat all previous steps for both Reach devices.***

### Working with ReachView app

#### Interface walkthrough

Open a web browser on your smartphone, tablet or laptop and type IP address of Reach in the address bar. ReachView consists of three main tabs: Status, Config, Logs. Status will show current satellite levels, solution status and coordintes. Config tab is used to set RTK parameters like positioning mode, set correction input interface and more. Logs tab keeps links to raw data logs, stored on the device and keeps the self-update button. By default, Reach starts as a rover and is stopped.

** It is highly recommended that you perform self-update during your first Reach use. **

To do this, make sure Reach is connected to a Wi-Fi network with Internet access. Go to the Logs page and press the **Update** button. ReachView will go inactive for about a minute. To reconnect, close the current tab and try to open ReachView in a new one. It is preferred to use Reach's IP address instead of **reach.local** to connect after an update.

#### Setting up base station

Navigate to Config tab and choose **Base** mode in the upper selector. Wait for the app to fetch current base settings. The settings include: base coordinates, input stream, output stream and RTCM3 messages to be used. **Input stream** settings must not be changed.

Most common settings for **output stream** are:

* TCP server with a specified port
* Serial connection
    * To direct the output stream to UART, use **ttyMFD2** device and desired baudrate
    * To direct to use a USB serial device, use **ttyUSB0**

Note that RTCM3 format is the only one available for base output. **RTCM3 message selector** is used to determine what kind of messages can be sent by the base. More about these messages can be found [here](http://www.geopp.de/rtcm-3-x-message-types/).

*It is very important to set precise **base coordinates** for RTK solution on rover to be valid.*

When you are done with the settings, hit the **SAVE & LOAD** button. Start the stream with the start button.

*TODO:* Wait for Single solution to appear, set up a coordinate, set up a port.

#### Setting up rover

Navigate to **Config** tab and choose **Rover** mode in the upper selector. Wait for the app to fetch current rover settings. Unlike the base mode, rover has a lot more settings and works with configuration files. You may choose the configuration file from the dropdown menu. Reach comes with several pre-defined default configs, such as **reach\_single\_default.conf** and **reach\_kinematic\_default.conf**.

The most important settings for the rover include:

* Positioning mode
    * Single. The result relies only on the on-board GPS unit. Base corrections will not be used in positioning
    * Kinematic. Base corrections will be used to improve positioning. The rover is assumed to be moving. This is the main RTK mode
* Input source for base corrections. Specify the path to base corrections stream. Most common options include:
    * TCP client with an IP and port
    * Serial connection. Use **ttyUSB0** for USB devices and **ttyMFD2** and baudrate for UART devices
    * NTRIP client
* Output solution paths. You can output solution data in several formats, like llh, xyz, nmea or enu. You can use the same UART port(**ttyMFD2**) for both base correction input and solution data output
* Log paths. By default, logs are written to a file stored locally. It is later available for download from the **Logs** tab


Under **Advanced settings** you can see much more parameters for fine-tuning RTK performance.

When you are done with the settings, hit the **SAVE & LOAD** button. This will start the calculations and writing the raw data log. Proceed to the **Status** tab to check your setup.

*TODO*
Set up a correction stream.

#### Viewing results

**Status** tab is the place to monitor current state of the positioning solution. First thing you see is a chart showing rover's satellite levels. Good reception of the satellite signal is essential for RTK technology to be able to produce a good positioning solution. This chart is intended to help with antenna placement. If you are in mode that involves base corrections and the input is setup correctly, you will see base satellite levels as well. The grid above the chart shows current state as the current positioning mode, solution status and coordinates in llh format.

The solution status value(simply labeled **status** in the grid) is the key value you can see here. After you have started the rover, you will be able to get the following solution statuses(probably in this order):

* **"-"**. This means there is not information for the software to process. Either not enough time has passed or the antenna is poorly placed
* **single**. This is usually the state that follows **"-"** in RTK mode. **Single** means that rover has found a solution relying on it's own receiver and base corrections are not taken into consideration yet. If rover is started in single mode, this will also be the result
* **float**. The base corrections are now taken into consideration and positioning is relative to base coordinates, but the integer ambiguity is not resolved
* **fixed**. Positioning is relative to the base and the integer ambiguity is properly resolved. This is as good as it gets, **fix** solution status indicates high level of positioning precision

*TODO*
Wait for Float status, then for Fix. LED statuses

#### Output: logs and solution

Reach supports outputting two types of data: **raw data logs** and processed **solution**.

**Raw data logs** contain all the messages sent by base and rover receivers. These logs can be used later for post-processing. On the contrary, **solution** is a stream of already processed and enhanced coordinates. Available solution formats include llh, xyz, nmea and enu.

By default, all **raw data logs** are saved as files on the device and are available for download on ReachView's **Logs** tabs.

*TODO*
Logs can be used for post-processing.
