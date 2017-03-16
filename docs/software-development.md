### Using Reach as a standalone Linux computer

While the intended workflow for Reach is using the ReachView app, no one restricts you from using it as a standalone Linux device. It can not be connected to a display, so you can only work with it through a network connection using **ssh**.

#### Connecting to Reach via ssh

##### Resolving IP address

* If you are on Reach's self-hosted network, it's IP is always **192.168.42.1**
* If there is only one Reach unit on the network, it should be accessible by **reach.local** address

If these are not the case, you will need to scan your local network. In most of these apps, Reach units will show up as **Murata Manufacturing Co.** device.

* You can use the **Fing app** to scan your local network from your phone
* You can use **nmap** to scan your local network on Linux/Mac OS X. Nmap is cli tool available through most package managers like [homebrew](http://brew.sh) on Mac and **apt-get** on Debian based Linux distributions. Example of using nmap to perform host discovery would be `sudo nmap -sn 192.168.1.0/24`
* On Windows, you can use **Zenmap**, which is a GUI for **nmap** or use any other third-party network scanners.

##### Using Ethernet over USB

With Reach you can use a virtual Ethernet network over a USB connection. Intel Edison officially supports this type of connection on Windows and Linux hosts.

###### Windows

You might need to wait for Windows to install the driver after plugging Reach in.

* In Windows 7 and below, go to the Control Panel. Under Network and Internet, click View network status and tasks. Click Change Adapter Settings in the sidebar
* In Windows 8, right-click the Windows Start menu button and select Network Connections

Choose the network adapter with RNDIS label. Go to properties, configure IPv4 IP address. Set manual IP address **192.168.2.2** with **255.255.255.0** mask. Apply changes.

Reach should now be available on **192.168.2.15** address.

###### Linux

Run `ifconfig` to check if you have a **usb0** interface available. It will not appear until Reach has at least partly booted.

If you do, run `sudo ifconfig usb0 192.168.2.2`.

Reach should now be available on **192.168.2.15**.

###### Mac OS X

This is not officially supported, but there is a [workaround](https://communities.intel.com/message/286267) that works on some versions of OS X.

##### SSH connection

###### Login and password:

* **login**:    `reach`
* **password**: `reach`

Note that for the latest beta images this has changed and the new login credentials are:

* **login**:    `root`
* **password**: `emlidreach`

###### Linux/Mac OS X

Open up a terminal and type `ssh reach@192.168.1.3`, where **192.168.1.3** is the IP address of your Reach unit. If there is only one Reach unit on the network, it should be accessible by `ssh reach@reach.local`. If you are on the Reach-hosted network, it's IP address will always be **192.168.42.1**. You will be prompted for password.

###### Windows

To connect, you will need to use **putty** or another third-party ssh implementation. After you have determined the IP address, type it in along with the username.

### Home directory contents

Default **reach** user's home directory contains following directories:

* **ReachView** contains the code for the ReachView app
* **RTKLIB** contains the software responsible for navigation data processing
* **Ubloxtest** and **MPUtest** are small programs used for self-tests
* **GPIO_Py** is a small python sysfs GPIO wrapper
* **logs** directory is the default path for storing RTKLIB output and raw data logs
* A hidden **.reach** directory that a save file **rtk_state**

> It is very important not to change anything in these directories, as the software relies on the created directory structure.

### Software structure

Software powering Reach can be divided in three different parts:

1. RTKLIB. Takes care of all navigation-related issues
2. ReachView back-end. A set of scripts aimed at automating work with RTKLIB and extracting useful information
3. ReachView front-end. Provides an interface to visualize this information and tweak RTKLIB settings

#### RTKLIB

[RTKLIB](http://www.rtklib.com) is written by Tomoji Takasu and distributed under BSD 2-clause license.

RTKLIB consists of multiple programs with different goals. For example, **rtkrcv** is used for immediate GPS data processing, including Real Time Kinematics. **Str2str** is used for the base mode to direct and split receiver stream. **Convbin** can convert navigation data from and to different formats.

RTKLIB was chosen as the data processing engine for Reach because it is widely used, open source, reliable and highly portable.

#### ReachView back-end

As stated above, the back-end is focused on automating work with RTKLIB. This includes switching modes(Rover/Base) and running corresponding binaries, extracting status info from the binaries, editing configuration files and mirroring all this to the front-end.

The back-end is written in Python. It uses [**pexpect**](http://pexpect.readthedocs.org/en/stable/) library to automate working with RTKLIB and [**Flask-SocketIO**](https://flask-socketio.readthedocs.org/en/latest/) framework for communicating with the front-end.

#### ReachView front-end

The front-end is the primary user interface for both ReachView and Reach. The intended use includes changing RTKLIB settings on Reach device, monitoring satellite levels for better antenna placement, monitoring solution status. It also allows to download logs, in case they were stored on the device.

The front-end is built using [**jQuery**](https://jquery.com), [**Socket.IO**](http://socket.io) and [**jQuery Mobile**](https://jquerymobile.com) as a UI element framework.

### Working with RTKLIB without ReachView

If you wish, you can disable ReachView by disabling the start-up service called **reach-setup**. To do this, run `sudo systemctl disable reach-setup.service`. However, this will also disable the Wi-Fi setup.

The main workflow for working with RTKLIB is the same as with any other Linux platform.

Most of the information is laid out in [RTKLIB docs](http://www.rtklib.com/rtklib_document.htm).

##### Setting up Rover

To use Rover mode, you need to run **rtkrcv** binary located inside `/home/reach/RTKLIB/app/rtkrcv/gcc/`.

**Rtkrcv** relies on configuration files usually stored in `/home/reach/RTKLIB/app/rtkrcv/`.
You can find a couple of Reach-ready **rtkrcv** configuration files for reference inside `/home/reach/ReachView/rtklib_configs`.

To load a configuration file, you can either `load` it after running the binary, or add a **-o** option followed by the file path, relative or absolute. For example: `/home/reach/RTKLIB/app/rtkrcv/gcc/rtkrcv -o /home/reach/RTKLIB/app/rtkrcv/reach_single_default.conf`. After this, several commands like `start`, `stop`, `restart` and `shutdown`(to quit) are available.

##### Setting up Base

Base is mode is represented by **str2str** binary inside `/home/reach/RTKLIB/app/str2str/gcc/`.

**Str2str** does not use configuration files and is configured by command line options. Important options include:

* **-in** specifies the input stream
* **-out** specifies the output stream
* **-p** specifies base coordinates(this is crucial to achieve good results) in llh format
* **-c** specifies receiver command file. Used to enable and disable certain receiver messages and their frequencies. You can use of the files provided in `/home/reach/ReachView/rtklib_configs`.

An example of running **str2str** on Reach:

`/home/reach/RTKLIB/app/str2str/gcc/str2str -in serial://ttyMFD1:230400:8:n:1:off#ubx -out tcpsvr://:9000#rtcm3 -msg 1002,1006,1013,1019 -p 60 30 50 -c /home/reach/RTKLIB/app/rtkrcv/reach_raw.cmd`

This starts a stream, capturing a UART stream in u-blox format from onboard GPS receiver and listening for connections on TCP port 9000. The output stream is in **RTCM3** format(RTKLIB only supports this output format). Messages used for output are 1002, 1006, 1013, 1019. Base latitude is 60, longitude 30, height 50. **reach_raw.cmd** file turns off default NMEA messages and turns on UBX-RAWX, UBX-SFRBX, UBX-TIM-TM2 messages and sets the frequency to 10 Hz.

Note that by default, after a power cycle, u-blox sends data on a 9600 baud rate. ReachView changes this to 230400. So, if you turned off **reach-setup** service that launches ReachView on boot, u-blox will be configured to use 9600 baud rate.
