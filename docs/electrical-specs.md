### Maximum ratings

|Name                                       | Value                |
|-------------------------------------------|----------------------|
| Inout voltage on USB and DF13 connectors  | 4.75 - 5.5 V         |
| Logic levels on all pins                  | 3.3 V                |
| Max input voltage on all pins             | 5.5 V                |
| Antenna DC bias                           | 3.3 V                |
| Antenna output current                    | 100 mA               |
| Max current consumption @5V               | 500 mA               |
| Normal current consumption @5V            | 200 ma               |
| Current limit on USB OTG                  | 1000 mA              |
| Temperature range                         | 0 +40 C (-40 +85 C)^ |

Officially Intel Edison is rated 0C to 40C, but Intel also claims they are performing temperature tests with good results, but just are not yet ready to officially rate Edison as extended temperature range device. Users report successful tests down to -40 C.

### Connectors pinout
![reach-connectors](img/electrical-specs/reach-connectors.png)

* GPIO46, GPIO77, PWM, SCL, SDA, TX, RX are connected to Intel Edison via buffers and are 3.3 V logic level, 5 V tolerant.
* TX and RX belong to UART1 on Intel Edison
* SCL and SDA belong to I2C1 on Intel Edison, I2C1 also could be used to communicate with internal magnetometer in MPU9250.
* PWM belongs to PWM3 GPIO183 on Intel Edison
* Time Mark input is connected directly to U-blox chip for low latency, it includes an over-voltage clamp, pull up and current limiting resistor.

### USB OTG

![otg-connection](img/electrical-specs/otg-connection.png)

Reach can both receive power from USB, acting as a device and source power to the port acting as a host. To use Reach in OTG mode you will need to connect 5V power source to DF13 connector pins (5 V, GND) and use OTG USB cable.
