#### Viewing results

**Status** tab is the place to monitor current state of the positioning solution. First thing you see is a chart showing rover's satellite levels. Good reception of the satellite signal is essential for RTK technology to be able to produce a good positioning solution. This chart is intended to help with antenna placement. If you are in mode that involves base corrections and the input is setup correctly, you will see base satellite levels as well. The grid above the chart shows current state as the current positioning mode, solution status and coordinates in llh format.

The solution status value (simply labeled **status** in the grid) is the key value you can see here. After you have started the rover, you will be able to get the following solution statuses (probably in this order):

* **"-"**. This means there is not information for the software to process. Either not enough time has passed or the antenna is poorly placed
* **single**. This is usually the state that follows **"-"** in RTK mode. **Single** means that rover has found a solution relying on its own receiver and base corrections are not taken into consideration yet. If rover is started in single mode, this will also be the result
* **float**. The base corrections are now taken into consideration and positioning is relative to base coordinates, but the integer ambiguity is not resolved
* **fixed**. Positioning is relative to the base and the integer ambiguity is properly resolved. This is as good as it gets, **fix** solution status indicates high level of positioning precision

#### Reading LED status

During configuration and non-RTK solution status, Reach will show debug information with the LED in the following form:

* <font color="white" style="background-color:black">White sync light, indicating message start</font>
* Network mode
    * <font color="blue">Wi-Fi Client</font>
    * <font color="green">Wi-Fi Master</font>
* RTK mode
    * <font color="blue">Rover</font>
    * <font color="magenta">Base</font>
* Are we started?
    * <font color="green">Yes</font>
    * <font color="red">No</font>
* Solution status (N/A to base)
    * <font color="red">"-"</font>
    * <font color="cyan">single</font>

After getting either float or fixed status, Reach LED will only show it with:

* Float with <font color="green">green</font>/<font color="yellow">yellow</font> blinks
* Fix with <font color="green">green</font> blinks
