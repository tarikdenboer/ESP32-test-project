# ESP32 test project

This project is a toy project to increase my knowledge with ESP32 in a Home Assistant environment as well as working with Git and GitHub. The aim is to build a combined sensor and control unit to do the following:
- Measure Temperature, Humidity and Pressure
- Measure eCO2 and tVOC
- Measure ambient light
- Output Temp/Humid/eCO2/tVOC on an OLED display
- Control play/pause, volume and next/previous of a Sonos Play 1
- Output currently playing song and artist on the OLED Display

It uses:

- ESPHome (https://esphome.io/)
- Home Assistant (https://www.home-assistant.io/)

Operation:

Temperature is measured with a BME280 Temperature/Humidity/Pressure,  sent to Home Assistant every 60 seconds and displayed on a SSD1306 OLED display. The eCO2 and tVOC are measured with a CCS811 sensor and sent to the Home Assistant the eCO2 is also displayed on the OLED display. 
The ambient light intensity is measured with the BH1750 in Wemos D1 Shield form factor and sent to Home Assistant. The idea is to use it in other Home Assistant automations. 
The 3 physical touch buttons used to control the Sonos sent their states to Home Assistant and so do the 2 wire based touch  sensors.


![Photo of prototype](https://raw.githubusercontent.com/tarikdenboer/ESP32-test-project/master/Images/ESP32_Test_Sensor_image.JPG)

# ESP 32 project pin layout

## Elements:
-   BME280
-   CCS811
-   BH1750
-   3 Touch Sensors (TTP223)
-   2 Captive Touch Sensors (Open Wire)
-   SSD1306 SPI display


**ESP**

![ESP32 Pinout](https://raw.githubusercontent.com/tarikdenboer/ESP32-test-project/master/Images/ESP32%20Lilygo%20T7%20v1.4%20pinout.png)

X means pin used see below for mapping

GPIO Row 1 | GPIO Row 2      | GPIO Row 3    | GPIO Row 4 
-----------|------------     |------------   | ----------
GND        |     RST         |   TX0         |    GND    
NC         |     VP          |   RX0         |    27 - X
VN         |     26          |22(I2C_SCL) - X|    25 - X
35         | 18(SPI_SCK) - X |21(I2C_SDA) - X|    32 - X
33 - X     | 19(SPI_MISO)    |   17          |    TDI
34 - X     | 23(SPI_MOSI) - X|   16          |    4 - X
TMS        | 5(SPI_SS) - X   |   GND         |    0
NC         |     3V3         |   5V          |    2 - X
SD2        |     TCK         |   TD0         |    SD1
CMD        |     SD3         |   SD0         |    CLK

**Sensors**

BME280       |     CCS811      |     ssd1306     |       TTP223s      | Captive Touch | BH1750 
--------     |-------          |-------          |-------             | -----         | -----  
SDO          | VCC - ESP 3V3   |  GND - ESP GND  |  T1 VCC -  ESP 3V3 | 1 - ESP 0     | D1 - ESP 22
CSB          | GND - ESP GND   |  VCC - ESP 3V3  |  T1 I/O - ESP 2    | 2 - ESP 33    | D2 - ESP 21
SDA - ESP 21 | SLC - ESP 22    |  DO - ESP 18    |  T1 GND - ESP GND  |               | 3v3 - ESP 3V3  
SCL - ESP 22 | SDA - ESP 21    |  D1 - ESP 23    |  T2 VCC - ESP 3V3  |               | GND - ESP GND 
GND - ESP GND| WAK - ESP GND   |  RST - ESP 27   | T2 I/O - ESP 34    | 
VCC - ESP 3V3| INT             |  DC - ESP 25    | T2 GND - ESP GND   |              
|            | RST             |  CS - ESP 5     | T3 VCC - ESP 3V3   | 
|            |ADO              |                 | T3 I/O - ESP 4     |
|            |                 |                 |T3 GND - ESP GND

