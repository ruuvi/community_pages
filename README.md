# FAQ: Beacon ID

Ruuvi tags are based on the Nordic Semiconductor nRF52832 System On a Chip which includes bluetooth radio.

The chip has several identifiers.

*   The MAC address: Unlike Network Interface Cards which have a manufacturers prefix and a unique device address, bluetooth MACs are simply a random 6 byte number. For example several samples of nRF52832 have addresses of C7:10:3C:68:24:C2, C4:C1:A5:FB:6D:46, F2:C0:C6:43:AD:03. The MAC address is taken from the chip's NRF\_FICR->DEVICEADDR\[0..1], a 64bit (sic) value in reverse order. The high order 2 bits are forced on so if the DEVICEADDR contains C2 24 68 3C 10 87 the advertised MAC will be C7:10:3C:68:24:C2.

    When the tag is in boot mode (after holding the B button, pressing Reset and releasing B as indicated by a solid RED LED and broadcasting as "RuuviBoot" ) the MAC address is broadcast as one higher then when running the applications. For example while in boot mode C7:10:3C:68:24:**C3** and in the application C7:10:3C:68:24:**C2**.

    The MAC address is broadcast in the bluetooth header. This is NOT available to Apple application Interfaces.

    In the raw/highres format 05: MAC is replicated in the data portion of packet. See [MyBeacons.info/packetFormats](http://mybeacons.info/packetFormats.html#highres).

    The MAC address can be read via NFC scan on official Ruuvi firmware.
* BLE name: The second and first bytes of DEVICEADDR\[0], aka the fifth and sixth bytes of the MAC (in lower case) are used, for example 'Ruuvi 24C2'.
* DEVICEID\[0..1]
* DEVICEADDR\[0..1] , DEVICEADDRTYPE ( public:0, random:1)
* NFC Tag Header: NFC.TAGHEADER0..1. (see 13.1.38)
*   userID

    None are printed on the ruuvi enclosure so determining the ID can be done by monitoring the nearby beacons( with Nordic nRFconnect for example), checking the signal strength (RSSI) and switching modes with the "B" button.
* Deprecated BEACON ID : in URL format 04 (#B): The first byte of DEVICEID is included as the last character of the the URL since Sept 2017 and displayed as a integer by ruu.vi. See [MyBeacons.info/packetFormats.html](http://mybeacons.info/packetFormats.html#four) For Example DEVICEID of 1A D8 3B D2 F1 A1 2C 54 reports BEACON ID 71. (The 1A
