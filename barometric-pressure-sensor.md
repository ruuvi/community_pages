# Barometric pressure sensor

The Infineon [DPS310](https://www.infineon.com/cms/en/product/sensor/pressure-sensors/pressure-sensors-for-iot/dps310/) or the  Bosch BME280 provide barometric pressure in hPa. The usage of this sensor includes indoor navigation (change of floor detection elevator detection), vertical velocity indication (rise/sink speed).



>

The Ruuvi Tag advertisement reports this with Rawv2 (format 05)in hundredths of hPa in the range to 500.00hPa to 1,100.00hPa. Variations of .01hPa may not be indicative of any change. As of version 2.5.9 the firmware uses the normal mode with a default oversampling of 1 (see drivers/init/init.c) and an IIR filter of (see application\_config.h) 16.

The sensor responds not only to changes that occur due to changes in the local weather but also the height of the sensor.

Here example of values taken on 12/20/20 in Northern New Jersey, USA Beginning at 12:26 ET on floor 1,003.07 .5 meters 1,003.03 floor 1,003.06 .5 meters 1,003.002 1 meter 1,002.96 floor 1,003.12 1 meter 1,003.27 2 meters 1,002.85 floor 1,002.80

From these values taken over 1/2 hour two things are apparent.

1. The pressure at any given height is constant over the short term (a few minutes) but varies of a longer period.
2. Not only a change in height but also then distance from datum can be determined.
