# Raspberry Pi Ready To Run SD image

There is a SD card image available for the Raspberry Pi 3, 3+ and 4 (not pi Zero)\*\*.

It sets up the raspberry Pi with Raspian Buster as an WiFI access point named RuuviCollector

The RuuviCollector java package reads packets from multiple Ruuvi Tags and inserts them into an Influx database.

Grafana is included to view the data from a web page.

Details about the genesis are available at [RPI Gateway](https://blog.ruuvi.com/rpi-gateway-6e4a5b676510)

An SD card image can be downloaded from [ruuviberry\_latest.zip](http://storage.ruuvi.com/ruuviberry\_latest.zip) which was ruuvicollector\_2020-01-30.minimal.img compressed as 1,804MB.

It can be flashed onto an 8GB or larger SD card using a utility like [balenaEtcher](https://www.balena.io/etcher/)

You may want to use `ssh` (or the MSwindows ssh client `putty`) to login to `10.0.0.1` as`pi:ruuviberry`and use `sudo raspi-config` to set the time zone.

Addition configuration of RuuviColector like changing the `measurementUpdateLimit` can be done by editing `/home/pi/RuuviCollector/ruuvi-collector.properties`. Refer to `/home/pi/RuuviCollector/ruuvi-collector.properties.example` for details.

You can change the retention policy - which is 7 days - for the influx database with a command like

`echo ALTER RETENTION POLICY default ON ruuvi DURATION 38d |influx`

\*\*An unofficial versinn for Pi ZeroW is available at [http://MyBeacons.info/RuuviCollectorSD.html](http://mybeacons.info/RuuviCollectorSD.html)
