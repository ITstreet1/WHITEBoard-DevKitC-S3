# WHITEBoard-DevKitC-S3

![20220426_194849](https://user-images.githubusercontent.com/30090189/165363639-11fd5551-2a3d-4173-af4b-b816168512f7.jpg)

WHITEBoard DevKitC S3 is a development board based on ESP32 S3 module. It has all features that ESP32 S3 offers, plus some aditional. In this repo you will find all the data you need to make this board, that include schematic, gerber files, etc. In adition, there are examples for all features that this DevKitC S3 variant offers.
## Features

* ESP32-S2-WROOM N8R8
  * MCU
    * 384 KB ROM
    * 320 KB SRAM
    * 16 KB SRAM in RTC
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

*esptool.py --chip esp32s3 --port COM7 --baud 921600 write_flash -z 0x000 C:\{adafruit-circuitpython-espressif_esp32s3_devkitc_1_n8-en_US-7.2.0.bin}*

Here you should use the appropriate COM port and appropriate path to a downloaded file. The name of the file might not be as the one here. A version of the software will change in time to come. After successfully uploaded CircuitPython unplugs DevKitC S3 and plugs it again, this time through the OTG port. DevKitC S3 will mount as a drive CIRCUITPY.

The next steps are to use your favorite CircuitPython editor and program this board. I use Thonny. Select WHITEBoard DevKitC S3 in Thonny by clicking Run->Select Interpreter, and then select Generic CircuitPython and proper Port. The name of a code to works automatically has to be main.py. When done, just Save, press Run, and DevKitC S3 will automatically start running the code.

### MicroPython

Not supported yet.

![20220426_194914](https://user-images.githubusercontent.com/30090189/165367177-1734f3f4-d175-467f-abe5-c8beb15dbb6c.jpg)

## Features

### RGB LED

RGB LED is tied to a GPIO48. There is an open solder jumper which you can close in the way of your need. Of course, you can not have both.

