### Camera integration

As of version **v0.4.0**, ReachView supports time marks in raw data logs. After converting a log to RINEX, you will see a number of captured time marks, among other RINEX messages.

The time marks are saved to the RINEX observation file as **external events**.

#### Post-processing software

To get the coordinates for these events you will need to perform post-processing on RINEX logs. By default, RTKLIB does not support external events, so we provide patched versions of **RTKCONV** and **RTKPOST**.

* [RTKCONV](https://files.emlid.com/RTKLIB/rtkconv_emlid_b26.exe)
* [RTKPOST](https://files.emlid.com/RTKLIB/rtkpost_emlid_b26.exe)
* [RTKPLOT](https://github.com/tomojitakasu/RTKLIB_bin/raw/rtklib_2.4.3/bin/rtkplot.exe)

If the logs contains RINEX external events, this version of RTKPOST will add a new solution file, with "**_events**" appended to the name with a list of events and their coordinates, calculated from two nearest points.

#### Camera hardware integration

[COMING SOON]
