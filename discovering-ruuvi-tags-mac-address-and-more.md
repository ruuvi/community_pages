# Discovering Ruuvi Tag's MAC address and more

Bluetooth devices have a 48 bit identifier BD\_ADDR displayed as xx:xx:xx:xx:xx:xx.

These address can be either : RANDOM STATIC which have the most two significant bits on and therefore begin with C, D, E or F for example: C4:C1:A5:FB:6D:45 or PUBLIC addresses where the first 3 bytes are a company ID as assigned by IEEE for a fee. All company IDs are less than 3FFFFF which avoids conflict with RANDOM addresses.

For Nordic devices, like nRF52832 a random 64 bit string is writtten to NRF\_FICR->DEVADDR during manufacture. Most Nordic and hence Ruuvi firmware use this to generate a BD\_ADDR.

The Ruuvi firmware replies to scan responses with the string Ruuivxxxx where xxxx are the 2 low order bytes of the BD\_ADDR. From the previous example Ruuvi6D45. Since using only those bytes the odds of 2 devices in any given bluetooth network (expected to be limited in scope) are 1:65,535, these should be significant to identify a particular device in down stream applications.

As the BD\_ADDR is generated in firmware it is posible to customize it to be a PUBLIC address with a company ID portion registered with the IEEE.

***

Apps ruuvi.station for android and ruuvi.station.ios for iPhone will discover tags and allow you to add them.

There is a great application that runs on a Mac at

[https://github.com/balda/ruuvitag-discovery](https://github.com/balda/ruuvitag-discovery)

If you already have ruuviCollector running you can list ALL the MAC address in the database using:

```
influx  -precision rfc3339 -database ruuvi  -host MyRpi 

SELECT last(mac), count(temperature) FROM ruuvi.autogen.ruuvi_measurements GROUP BY mac 
```

Either directly on the raspberry pi or from another "host" where influx is installed.

This may take a little while (2-3 minutes) if you are running the ruuviCollector on a tiny little Pi Zero.

If you have curl installed you can use something like:

```
time curl --silent --show-error --get 'http://pi93graf:8086/query?' --data-urlencode "db=ruuvi" \
--data-urlencode "q=SELECT mac, last(temperature) FROM ruuvi.autogen.ruuvi_measurements GROUP BY mac"
```

But the output is hard (for humans) to unscramble.
