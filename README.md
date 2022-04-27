# WHITEBoard-DevKitC-S3

![20220426_194849](https://user-images.githubusercontent.com/30090189/165363639-11fd5551-2a3d-4173-af4b-b816168512f7.jpg)

WHITEBoard DevKitC S3 is a development board based on ESP32 S3 module. It has all features that ESP32 S3 offers, plus some aditional. In this repo you will find all the data you need to make this board, that include schematic, gerber files, etc. In adition, there are examples for all features that this DevKitC S3 variant offers.
## Features

* ESP32-S2-WROOM N8R8
  * MCU
    * 384 KB ROM
    * 320 KB SRAM
    * 16 KB SRAM in RTC
    * two cores
  * Wi-Fi
    * 802.11b/g/n
    * Bit rate: 802.11n up to 150 Mbps
    * A-MPDU and A-MSDU aggregation
    * 0.4μs guard interval support
    * Center frequency range of operating channel:2412~2484 MHz
  * Bluetooth
    * Bluetooth LE: Bluetooth 5, Bluetooth mesh
    * 2 Mbps PHY
    * Long range mode
    * Advertising extensions
    * Multiple advertisement sets
    * Channel selection algorithm #2
  * Hardware
    * Interfaces: 45 GPIO, 4x SPI, 3x UART, 2x I2C, 2x I2S, LCD interface, 14x Touch, RMT, LED PWM, TWAI, USB-OTG 1.1, 2x 12-bit ADC, PWM, JTAG
    * 40 MHz crystal oscillator
    * 8 KB SPI FLASH
    * 8 KB PSRAM
    * Operating voltage/Power supply: 3.0~3.6 V
    * Operating temperature range: –40~85 °C
    * Dimensions: (18 × 25.5 × 3.1) mm
  * Certification
    * Green certification: RoHS/REACH
    * RF certification: FCC/CE-RED/SRRC
  * Test
    * HTOL/HTSL/uHAST/TCT/ESD
* All GPIO pins breaks into two header rows
* UART CP2102N chip with auto reset circuit
* User Buttons
  * BOOT
  * RST
* WS2812C LED
  * WS2812C is fully compatible with WS2812B
  * Operating Currentof 5 mA
  * Built-in signal reshaping circuit
  * Built-in electric reset circuit and power lost reset circuit
  * Send data at speeds of 800 Kbps
  * Scan frequency 2 KHz
  * 256 brightness display
  * 16777216 color
* Li-Po JST connector with MCP73831 charging circuit
* Micro USB UART port
* Micro USB OTG port
* Power switch

![20220426_194859](https://user-images.githubusercontent.com/30090189/165365498-66672f09-f268-4140-a906-78bf8142508a.jpg)

## Getting started

WHITEBoard DevKitC S3 is a development board that can be programmed with CircuitPython and MicroPython. Arduino IDE support is just around the corner. 

### Arduino IDE C/C++

-not available at the moment.

#### PROG PORT

-not available at the moment.

#### OTG PORT

-not available at the moment.

### CircuitPython

If your choice is a CircuitPython, you need to have installed the latest version of Python. To check what version you have, open Command Prompt and type in:

*python --version*

For erasing and uploading a firmware on ESP32-S3 you need Development mode Esptool, download it by typing:

*git clone https://github.com/espressif/esptool.git*

*cd esptool*

*pip install -e .*

If no problem you should get a message everything is ok. To check if everything is ok, type in:

*esptool.py*

You should get a list of commands with list of supported chips, in our case esp32s3. The next step is to download a BIN fajl of CircuiPython. Go to https://circuitpython.org and search for N8R8 as that is the modul of ESP32-S3 we use here. Select DevKitC, that will get you to the download page. Download BIN fajl on some location on your PC. At this moment, ONLY version 7.2.0 works as expected.
The next step is to erease Flash of Esp32-S3. To do so connect WHITEBoard DevKitC S3 to a PC with PROG port, and type in:

*esptool.py --chip esp32s3 erase_flash*

Now it is time to upload the CircuitPython firmware to the WHITEBoard DevKitC S3. To do so check on which COM port is DevKitC S3 (say it is COM7). In prompt type:

*esptool.py --chip esp32s3 --port COM7 --baud 921600 write_flash -z 0x0 C://{adafruit-circuitpython-espressif_esp32s3_devkitc_1_n8r8-en_GB-7.2.0.bin}*

Here you should use the appropriate COM port and appropriate path to a downloaded file. The name of the file might not be as the one here. A version of the software will change in time to come. After successfully uploaded CircuitPython unplugs DevKitC S3 and plugs it again, this time through the OTG port. DevKitC S3 will mount as a drive CIRCUITPY.

The next steps are to use your favorite CircuitPython editor and program this board. I use Thonny. Select WHITEBoard DevKitC S3 in Thonny by clicking Run->Select Interpreter, and then select Generic CircuitPython and proper Port. The name of a code to works automatically has to be main.py. When done, just Save, press Run, and DevKitC S3 will automatically start running the code.

### MicroPython

Not supported yet.

![20220426_194914](https://user-images.githubusercontent.com/30090189/165367177-1734f3f4-d175-467f-abe5-c8beb15dbb6c.jpg)

## Features

### RGB LED

RGB LED is tied to a GPIO48. There is an open solder jumper which you can close in the way of your need. Of course, you can not have both.

### LiPo charging meter

There are two resistors, 22K and 5.6K as a voltage divider. They are tied to a GPIO01, which is Analog pin A0. As for RGB and BTN, under WHITEBoard Saola, there is a solder jumper. You can choose if you want to use GPIO01 on the header, or to measure battery voltage level.

## Power

For power management, this board uses two ICs. MCP73831 For battery management check the LiPo charging section below.
WHITEBoard DevKitC S3 can be powered up by any of the micro USB connectors. 5V rail is going to the SE5218 voltage regulator. This is an LDO that provides 3.3V@500mA. While testing, I had ZERO issues with stability. But it also means that DevKitC S3 can not directly power up some power-hungry sensors or modules. In such a case, use an external power supply.
There is no dedicated VIN pin to power WHITEBoard DevKitC S3 through pinout. However, pin 5V can be used to power DevKitC S3 with REGULATED 5V DC. Do not use pin 3V3 in a similar manner. However, you CAN NOT charge battery through 5V pin.
The switch under the board is manipulating with the EN pin of the LDO. This way powers up the board. There is a MOSFET for switching the power supply. DevKitC S3 will cut the battery when there is 5V power on micro USBs or 5V pin. Charging the battery remains all the time when there is 5V. The same goes for the power switch position.

## LiPo charging

For Li-Po charging there is the MCP73831 IC. With a resistor R16 of 2K, charging is set to 500mA charging current. By replacing this resistor you can change the charging current. Here is the table:
* 10K - 100mA
* 5K  - 200mA 
* 2K  - 500mA
* 1K  - 1000mA

Onboard there is a JST 2.00mm pitch connector. As JST is NOT standardized, please check the battery polarity. Wrong polarity can destroy the board and/or battery. Supported batteries are standard Li-Ion/Li-Po with 3.7V nominal voltage. You can use a battery of any capacity.

If the project is for use with a battery, there is a switch on the right side that basically switch from VCC to GND on the EN pin of a voltage regulator. This way you can enable or disable power to the BOARD. In case you can not upload the sketch to a WHITEBoard DevKitC S3, please check the position of this switch. While turned OFF by this switch, you can still charge the battery by any of the micro USB ports.

![20220426_194941](https://user-images.githubusercontent.com/30090189/165368291-d5de6f68-ba82-42a6-a5be-5ce7b7780f4c.jpg)

## Pinout

WHITEBoard Saola has a two-row header with 44 pins in total. Plus additional 4-pin JTAG header. Here you can find the boards diagram so check it out. As I mention, WHITEBoard DevKitC S3 has all ESP32-S3 N8R8 pins break out. That is the reason for the size of the board, besides 0805 components and soldering on one side only. To power additional sensors and modules, there are two GND pins and two power pins (5V and 3.3V). There is no VIN pin (check the Power part above). GPIO pins are NOT 5V TOLERANT!!! Use some logic shifter, voltage divider, or OP-AMP when interfacing 5V devices.

* First Row
  * 3V3
  * 3V3
  * EN
  * GPIO4
  * GPIO5
  * GPIO6
  * GPIO7
  * GPIO15
  * GPIO16
  * GPIO17
  * GPIO18
  * GPIO8
  * GPIO19
  * GPIO20
  * GPIO3
  * GPIO46
  * GPIO9
  * GPIO10
  * GPIO11
  * GPIO12
  * 5V
  * G
* Second Row
  * G
  * GPIO1
  * GPIO2
  * TX
  * RX
  * GPIO42
  * GPIO41
  * GPIO40
  * GPIO39
  * GPIO38
  * GPIO37
  * GPIO36
  * GPIO35
  * GPIO0
  * GPIO45
  * GPIO48
  * GPIO47
  * GPIO12
  * GPIO14
  * GPIO13
  * G
  * G

## PROS

* LiPo battery
* RGB LED
* WiFi
* Bluetooth
* OTG and UART micro USB
* Complete GPIO pinout

## CONS

## Dimensions

Dimensions of this board are 28x90mm. The hight is 7mm (without headers).

## Disclaimer

WHITEBoard DevKitC S3 is an open-source development board. My small contribution to the community, that gave me so much. Feel free to use and modify as you want. It would be nice to add some credits if you do.
