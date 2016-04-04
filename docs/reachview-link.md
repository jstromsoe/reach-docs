
###### Data streams

There is a number of data streams to be configured: base input, solution and logs.

* Base input stream is the way to get base corrections
* Logs, or raw data streams, contain receiver's output and can be later used for post-processing
* Solution is location information extracted from processed raw data

All these streams have a number of paths to directed to. Some paths are common, some paths are specific to the stream type.

Common stream paths include:

* Serial connection. For Reach's UART port use "**ttyMFD2**" device and a baud rate of the connected accessory. For USB devices, use "**ttyUSB0**" and a random baud rate (it will be ignored)
* TCP server. Listen to TCP connections on a specified **port**
* TCP client. Connect to TCP server listening on a certain **IP address** and **port**
* File. Specify a **path to a file** on Reach. This is particularly useful for logs. By default, when you choose log output path to be a file, you get a default path to a file which contains current date and time mask. Writing logs to this default file path will make them available in the **Logs** tab later (refresh page after stopping rover)

Paths, specific to input stream:

* NTRIP client. Connect to a NTRIP caster. You will need an **address** and a **port**, some casters also require a **login** and a **password**
* http. Enter a **URL**
* ftp. Enter a **URL**

Paths, specific to output streams:
