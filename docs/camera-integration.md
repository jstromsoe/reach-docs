### Camera integration

As of version **v0.4.0**, ReachView supports time marks in raw data logs. After converting a log to RINEX, you will see a number of captured time marks, among other RINEX messages.

The time marks are saved to the RINEX observation file as **external events**.

#### Post-processing software

To get the coordinates for these events you will need to perform post-processing on RINEX logs. By default, RTKLIB does not support external events, so we provide a patched version of **RTKPOST**. Our version **requires SBAS turned off during processing**.

* [RTKPOST](https://files.emlid.com/RTKLIB/rtkpost.exe)
* [RTKPLOT](https://files.emlid.com/RTKLIB/rtkplot.exe)

If the logs contains RINEX external events, this version of RTKPOST will add a new solution file, with "**_events**" appended to the name with a list of events and their coordinates, calculated from two nearest points.

#### Camera hardware integration

[COMING SOON]
