# Ruuvi Tag movement and orientation

Ruuvi Tag includes a [LIS2DH12 accelerometer](https://www.st.com/en/mems-and-sensors/lis2dh12.html) made by STMicroelectronics. It can measure +-16 G accelerations up to 5,000 times a second.

The Ruuvi firmware provides 2 different interpretations:

**Movement:** When the tag is moved in a combined X/Y/Z direction exceeding 64mG the "movementCounter" is incremented and reported in [Format 05 (RAWv2)](https://github.com/ruuvi/ruuvi-sensor-protocols/blob/master/dataformat\_05.md) packets. This has a range of 0 to 254. A value of 0 would only indicate no movement if the tag has not moved since reset. The 64mG reflects a rather subtle movement. This is very useful if the tag is usually in a static position and is occasionally bumped. The frequency of packet transmission is low ( as of [version2.5.9](https://lab.ruuvi.com/dfu/) 1.285 seconds in fast modes and 6.425 seconds in slow mode). The "movementCounter" may wrap and return unpredictable values if the tag is mounted on a vibrating surface.

**Orientation:** A (usually) static tag's orientation can be determined by examining the Acceleration-X, Y and Z values in [Format 03 (RAWv1)](https://github.com/ruuvi/ruuvi-sensor-protocols/blob/master/dataformat\_03.md) and [Format 05 (RAWv2)](https://github.com/ruuvi/ruuvi-sensor-protocols/blob/master/dataformat\_05.md) packets. Acceleration-Z will reflect the orientation i.e. flat like on a table which reports a value near 1.000. As the tag is inclined the value decreases until, when the tag is on edge, a small value ( like .004 or -.004) is reported.

If the tag is positioned not exactly flat (like on edge) X and Y can be used to understand a rotational position. There is no way to know the position of the sensor when the circuit board is inside the enclosure. The circuit board must be aligned and prevented from rotating within the enclosure and each tag must be calibrated.

Various use cases include [Monitor varmit trap](https://f.ruuvi.com/t/monitor-varmit-trap/4213), [Remote location flood reporting](https://f.ruuvi.com/t/remote-location-flood-reporting/4266), [Garage Door monitor](https://f.ruuvi.com/t/garage-door-monitor/3800) , [Door monitor](http://mybeacons.info/doorMonitor.html), [wind vane](http://mybeacons.info/windvane.html) and [Sump pump failure alert](https://f.ruuvi.com/t/sump-pump-failure-alert/4127/2).
