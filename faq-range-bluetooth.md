# FAQ: range: Bluetooth

The range of bluetooth and specifically the nRF52832 are very dependent on the radio materials blocking (like walls) between the transmitter and the receiver.

Another consideration is the interference caused by other devices including other bluetooth devices and other ruuvis!

* maximum expected range in meters
* Outdoors with a clear line of sight has been reported as high as 1,000M
* Indoors, with standard home construction more like 20.
* In an office building it may be only 10.

Since the regulations restrict the maximum power output, the best way to increase range is to use a more sensitive receiver.

If ruuvi is acting as a beacon this means that the range is dependent on the phone or bluetooth receiver (like on a Raspberry Pi).

A possible means of extending the range is by adding a custom antenna.

The radio output power is set in the nordic Semiconductor n58532 TXPOWER register in the range from +4 to -40 dBm. see 23.14.10 of nRF52832 Product Specification v1.3

This is a sample of the RSSI over a 15 second period as measured by raspberry pi using hcidump with NO movement:

71, 72, 54, 56, 71, 71, 54, 71, 70, 73, 71, 70, 70, 72, 74, 55, 55, 69, 72, 73, 73, 74, 69, 69, 72, 57, 74, 70, 72, 71, 74,

Min=54, average=68.3, max 74,

Here's a summary of 5,000 RSSI values taken by a raspberry pi at a 2 meter range with no movement.

![RSSI at 2 meters](http://mybeacons.info/RSSIat2meters.png)

nRF52832 does not support BT Long Range.

See [This](https://blog.nordicsemi.com/getconnected/bluetooth-5-in-smartphones) Nordic article from June 2018.

[Bluetooth Accessory Design Guidelines for Apple Products](https://developer.apple.com/hardwaredrivers/BluetoothDesignGuidelines.pdf) Section 23.\
[Apple Technical Q\&A QA1931](https://developer.apple.com/library/archive/qa/qa1931/\_index.html)

Your actual mileage, i.e. range may vary.
