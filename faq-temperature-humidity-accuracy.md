# FAQ: Temperature, humidity accuracy

There are frequently questions regarding the accuracy of the data reported by the Ruuvi tags.

While accuracy (as well as precision) are a consideration, each application has requirements that need to be considered. For example when weather monitoring, a difference in a few percent humidity or a few degrees temperature are frequently insignificant and even for trends can be ignored. Differences in different tags may not be important.

Devices including Bosch BME280, Sensirion SHTC31 and [TMP117](https://blog.ruuvi.com/ruuvi-firmware-adding-a-new-sensor-6e973b2e8a9b) (temperature only) may be incorporated.

* The Sensirion SHTC31 [datasheet](https://www.sensirion.com/fileadmin/user\_upload/customers/sensirion/Dokumente/2\_Humidity\_Sensors/Datasheets/Sensirion\_Humidity\_Sensors\_SHTC1\_Datasheet.pdf) shows typical tolerance of ±2%RH Across the entire range.
* The Bosch BME280 [datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf) provides details. Some are here:
* **Humidity**: "Absolute accuracy tolerance" is ±3%RH at 25°C(77°F) within the 20..80%RH range. According to a Bosch engineer this accuracy can be expected up to 90%RH but is only ±6%RH above 90%RH. This means that if the device is reporting 100%RH the actual humidity may be only 94%. "**Non-linear** contributions to the sensor data are corrected during the calculation of the relative humidity by the compensation formulas" which are used by the Ruuvi tag firmware. The Ruuvi Station IOS mobil application also provides establishing a subsequent per tag correction factor which assumes a constant discrepancy. Discussion of Humidity calibration and testing is [here](https://blog.ruuvi.com/humidity-sensor-673c5b7636fc). Water vapor begins to condense onto impurities (such as dust or salt particles) in the air as the RH approaches 100 percent, and a cloud or fog forms. Some devices have been known to report erroneous values and the maximum value is artificially capped at 100%. Condensation inside tag at some point may cause an offset ( we had a few devices with offsets X-rayed and cut open which showed that the sensing element had accumulated salt.) The BME280 can be reconditioning by dry baking at 120°C <5%rH for 2 hours then re-hydrating at 25°C 75%rH for 24 hours as described in the [data sheet section 7.9](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf) .
* **Temperature**: "Full accuracy" is ±2°C(1.8°F) in the 0..65°C(32..149°F) range with a slight reduction to 1.25°C(2.25°F) below that.
* The minimal response time of 1second, i.e. the time needed for the BME280 device to correctly report the data, is when there is 1m/sec airflow which within the enclosure should not be expected. This means that data reported may take a long time to accurately reflect the surrounding environment. In fact, if conditions are changing fast enough the sensor may not report maximums or minimums.
* The BME280 includes oversampling to reduce noise.

An additional discussion regarding one user's testing is [here](https://f.ruuvi.com/t/humidity-readings-problem/3816).
