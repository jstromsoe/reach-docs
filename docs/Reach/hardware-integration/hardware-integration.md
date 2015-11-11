### Hardware INTEGRATION

#### Radio

It is possible to connect radio modules to Reach in order to obtain corrections or send calculated coordinates.

Most radios nowadays use UART or USB as a connection.

##### Connecting UART radio

<font color="red">DO NOT CONNECT RADIO TO REACH WITH DIRECT DF13 CABLE, IT CAN CAUSE DAMAGE TO THE DEVICES</font>

Logic level on UART in Reach is 3.3V. Please only use radios  with 3.3V logic level.
To connect UART radio to Reach use upper DF13 port (the one near the USB).

| Reach pins | Radio pins |
|:----------:|:----------:|
|     +5V    |     +5V    |
|     TX     |     RX     |
|     RX     |     TX     |
|     GND    |     GND    |

Connection diagram for 3DR Radio v2:

![image](reach-3dr-radio.png)

UART radio is accessible on Reach as a serial device with the name **ttyMFD2**

##### Connecting USB radio

To connect USB radio to Reach use USB-OTG cable provided with the package.
Plug radio into USB-F port and plug Micro-USB end of the cable in Reach.
When using USB port in OTG mode Reach has to be powered over one of the DF13 ports.

USB radio is accessible on Reach as a serial device with the name **ttyUSB0**

#### Pixhawk autopilot

**[Integration of Reach RTK module with Pixhawk is a work in progress]**

#### Camera

**[Integration of Reach RTK module with cameras is a work in progress]**
