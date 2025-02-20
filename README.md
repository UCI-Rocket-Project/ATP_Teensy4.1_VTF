# UCIRP Avionics Flight Sensor (AFS)
v1.1 "Rigel" (a star in Orion's constellation)

The board includes: 
- [Adafruit BMP388](https://www.amazon.com/Adafruit-BMP388-Precision-Barometric-Altimeter/dp/B07JXYK9ZB) Barometric and Pressure Sensor
- [Hitlego MPU-6050](https://www.amazon.com/HiLetgo-MPU-6050-Accelerometer-Gyroscope-Converter/dp/B01DK83ZYQ/ref=pd_ybh_a_1?_encoding=UTF8&refRID=VTDTAEY02AXR1SPZ293G&th=1) Accelerometer and Gyroscope
- [Adafruit Ultimate GPS](https://www.adafruit.com/product/746#description)
- [Digi XBee-PRO XSC S3B](https://www.mouser.com/ProductDetail/Gravitech/XBee-USB?qs=Vxac6xGyzPnMlpwH9hhfHQ%3D%3D) 
- [Sparkfun XBee Adapter](https://www.sparkfun.com/products/11373)
- Teensy 4.1
- [Linear Regulator (9V -> 5V)](https://www.digikey.com/en/products/detail/stmicroelectronics/L7805CV/585964)

Communication Protocols Used:
| Component  | Communication Protocol | 
| ------------- | ------------- |
| BMP388  | SPI  | 
| ECU 1.5 "Orion" | I2C (Wire) |
| GPS  | UART (Serial 2) |
| MPU-6050  | I2C (Wire 1)  |
| SD Module | SPI |
| XBEE  | UART (Serial 6) |



Pinouts:

BMP
- CS	 -> 10 CS
- SDI  -> 11 MOSI
- SDO  -> 12 MISO
- SCK  -> 13 SCK

ECU 1.5 "Orion"
- SDA2  -> 18 SDA
- SCL2  -> 19 SCL

GPS (Serial2 port in Teensy 4.1)
- TX	 -> 7 RX2
- RX	 -> 8 TX2

MPU (Wire1 port in Teensy 4.1)
- SDA  -> 17 SDA1
- SCL	 -> 16 SCL1

SD Module 
- MISO -> 39 MISO1
- MOSI -> 26 MOSI1
- SCK  -> 27 SCK1
- CS   -> 38 CS1

XBEE (Serial6 port in Teensy 4.1)
- DOUT -> 25  RX6
- DIN  -> 24 TX6




## Used Packages
- Teensy 4.1 [symbol](https://github.com/XenGi/teensy_library) and [footprint](https://github.com/XenGi/teensy.pretty). Related files and license is located under `/teensylib`.


## Notes
- The board requires an external 9V battery to power sensors and the Teensy. The onboard regulator will step down to 5V and provide stable 5V power.
- The GPS uses an optional "CR1220 coin cell to keep the RTC running and allow warm starts"
- The XBee module (not on AFS PCB) mounts on top of the XBee USB adapter. The USB adapter board has power and serial pass-through to the XBee module
- The board was renamed from "Avionics Test Payload (ATP)" to "Avionics Flight Sensor (AFS)"

### v1.1
- Changed [Adafruit XBee USB Adapter](https://www.adafruit.com/product/247?gclid=Cj0KCQiA1sucBhDgARIsAFoytUtwdYkYjMLGpFy2WvyzD8O8x4Ewsu3eSLwTMnisukgy84cH7zYznMQaAjZiEALw_wcB) to [Sparkfun XBee Adapter](https://www.sparkfun.com/products/11373)
- XBee receives 5V from regulator, instead of 3.3V from Teensy. During testing we found out that Teensy did not supply enough power for Xbee communication and after sending 1 or 2 packages of data, the Teensy would stop working.
- Regulator is flipped, so we can attach a heat sink 
