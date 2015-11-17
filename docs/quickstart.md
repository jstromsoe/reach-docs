### Intro

In this quick tutorial we will show you how to two set up two Reach devices as a base and a rover with corrections sent over Wi-Fi.

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

### Working with ReachView app

#### Updating ReachView

To do this, make sure Reach is connected to a Wi-Fi network with Internet access. Go to the Logs page and press the **Update** button. ReachView will go inactive for about a minute. To reconnect, close the current tab and try to open ReachView in a new one. It is preferred to use Reach's IP address instead of **reach.local** to connect after an update.

***Repeat all previous steps for both Reach devices.***

#### Interface walkthrough

Open a web browser on your smartphone, tablet or laptop and type IP address of Reach in the address bar. ReachView consists of three main tabs: Status, Config, Logs. Status will show current satellite levels, solution status and coordintes. Config tab is used to set RTK parameters like positioning mode, set correction input interface and more. Logs tab keeps links to raw data logs, stored on the device and keeps the self-update button. By default, Reach starts as a rover and is stopped.

#### Setting up base station

Connect to Reach you want to use as a base. Navigate to Config tab and choose **Base** in the upper selector. Wait for the app to fetch current base settings. The settings include: base coordinates, input stream, output stream and RTCM3 messages to be used.

By default, base output stream will be available on a TCP port 9000.

Hit the **Start** button.

#### Setting up rover

Connect to the second Reach. Navigate to **Config** tab and choose **Rover** mode in the upper selector. Wait for the app to fetch current rover settings. Choose **reach_kinematic_default.conf** from the configuration file list.

Now, you need to change base station connection settings. Make sure that "Input source for base corrections" is set to **TCP client** and enter base Reach's IP address to the address window. Default port is 9000.

Hit the **Save** button. Click "Yes" to load current settings. The rover mode will start.

#### Viewing results

Go to **Status** tab of the app on the rover device. You can see a bar chart with satellite levels, current coordinates in llh format, positioning mode and solution status. In this quick tutorial, positioning mode is set to "Kinematic" which is the main RTK mode.

If everything has been set up correctly, you will see changes in the solution status box. You will see the statuses in the following order:

* **"-"**. This means there is not information for the software to process. Either not enough time has passed or the antenna is poorly placed
* **single**. This is usually the state that follows **"-"** in RTK mode. **Single** means that rover has found a solution relying on it's own receiver and base corrections are not taken into consideration yet. If rover is started in single mode, this will also be the result
* **float**. The base corrections are now taken into consideration and positioning is relative to base coordinates, but the integer ambiguity is not resolved
* **fixed**. Positioning is relative to the base and the integer ambiguity is properly resolved. This is as good as it gets, **fix** solution status indicates high level of positioning precision

If you got around to the **fixed** status everything is perfect. Satellite levels and therefore antenna placement severely affect RTK performance. Remember that you need at least 4 satellites with SNR levels over 45(marked green on the chart) to get RTK improved solution. 
