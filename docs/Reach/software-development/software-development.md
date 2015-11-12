#### Using Reach as a standalone Linux computer

While the intended workflow for Reach is using the ReachView app, no one restricts you from using it as a standalone Linux device. It can not be connected to a display, so you can only work with it through a network connection using **ssh**.

##### Connecting to Reach via ssh

###### Resolving IP address

* If you are on Reach's self-hosted network, it's IP is always **192.168.42.1**
* If there is only one Reach unit on the network, it should be accessible by **reach.local** address

If these are not the case, you will need to scan your local network. In most of these apps, Reach units will show up as **Murata Manufacturing Co.** device.

* You can use the **Fing app** to scan your local network from your phone
* You can use **nmap** to scan your local network on Linux/Mac OS X. Nmap is cli tool available through most package managers like [homebrew](http://brew.sh) on Mac and **apt-get** on Debian based Linux distributions. Example of using nmap to perform host discovery would be `sudo nmap -sn 192.168.1.0/24`
* On Windows, you can use **Zenmap**, which is a GUI for **nmap** or use any other third-party network scanners.

###### Linux/Mac OS X

Open up a terminal and type `ssh reach@192.168.1.3`, where **192.168.1.3** is the IP address of your Reach unit. If there is only one Reach unit on the network, it should be accessible by `ssh reach@reach.local`. If you are on the Reach-hosted network, it's IP address will always be **192.168.42.1**. The **password** is also **reach**.

###### Windows

To connect, you will need to use **putty** or another third-party ssh implementation. After you have determined the IP address, type it in along with username **reach**. The **password** is also **reach**.

#### Home directory contents

Default **reach** user's home directory contains following directories:

* **ReachView** contains the code for the ReachView app
* **RTKLIB** contains the software responsible for navigation data processing
* **Ubloxtest** and **MPUtest** are small programs used for self-tests
* **GPIO_Py** is a small python sysfs GPIO wrapper
* **logs** directory is the default path for storing RTKLIB output and raw data logs
* A hidden **.reach** directory that a save file **rtk_state**

<font color="red">It is very important not to change anything in these directories, as the software relies on the current structure.</font>

#### Working with RTKLIB without ReachView

If you wish, you can disable ReachView by disabling the start-up service called **reach-setup**. To do this, run `sudo systemctl disable reach-setup.service`. However, this will also disable the WiFi setup.

The main workflow for working with RTKLIB is the same as with any other Linux platform

###### Setting up Rover

To use Rover mode, you need to run **rtkrcv** binary located inside `/home/reach/RTKLIB/app/rtkrcv/gcc/`

**Rtkrcv** relies on configuration files usually stored in `/home/reach/RTKLIB/app/rtkrcv/`.
You can find a couple of Reach-ready **rtkrcv** configuration files for reference inside `/home/reach/ReachView/rtklib_configs`.

To load a configuration file, you can either `load` it after running the binary, or add a **-o** option followed by the file path, relative or absolute. For example: `/home/reach/RTKLIB/app/rtkrcv/gcc/rtkrcv -o /home/reach/RTKLIB/app/rtkrcv/reach_single_default.conf`. After this, several commands like `start`, `stop`, `restart` and `shutdown`(to quit) are available.

###### Setting up Base










