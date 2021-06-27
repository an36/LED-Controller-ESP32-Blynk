# LED Controller Blynk App with ESP32+WiFi (LEDctrl App)
In this project, a ESP32 microcontroller is used along with a Blynk app to actuate a strip of 62 WS2812B LEDs over WiFi.

Note that there's also a MP34DT01-M PDM MEMS Microphone that is being used to make the LEDs respond to the current sound volume level.

---

## Demo:

---

## Required Hardware:
* [ESP32 + WiFi Onboard](https://www.adafruit.com/product/3405)
* [WS1228B Addressable RGB LEDs strip](https://www.amazon.com/gp/product/B07BKNS7DJ/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [5V 10A DC Power Supply](https://www.amazon.com/gp/product/B07CMM2BBR/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [MP34DT01-M PDM MEMS Mic Breakout](https://www.adafruit.com/product/3492?gclid=CjwKCAjww-CGBhALEiwAQzWxOoJ1X5J6meE_1WD8ngq5gAuR29hyn-5CHDR53ZTJ1IfpZRNiy5qt3BoCwZ4QAvD_BwE)

*NOTE:* Please take a look at the [Schematic/LEDctrl_Schem.png](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/Schematic/LEDctrl_Schem.png) to see the LEDctrl project schematic which shows the appropriate wiring of each component mentioned just above.

---

## Required Software:
* [Arduino IDE](https://www.arduino.cc/en/software)
* [LED Controller Code (LEDctrl.ino)](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/src/Arduino%20IDE/LEDctrl.ino)
* [Blynk Mobile App](https://blynk.io/en/getting-started)
* [LEDctrl Blynk App Clone Barcode](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/src/Blynk%20App%20Clone/LEDctrl%20Blynk%20App%20Clone.png)

<br>

*After downloading the [Arduino IDE](https://www.arduino.cc/en/software) software, you'd need to install the following Arduino IDE libraries/packages to be able to compile, upload, and run the [LEDctrl.ino](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/src/Arduino%20IDE/LEDctrl.ino) source code*
#### Arduino IDE Required Libraries:
* [ESP32 Board Library](https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/)
* [Arduino IDE WiFi.h Built-in Library](https://www.arduino.cc/en/Reference/WiFi)
* [Blynk Library](http://help.blynk.cc/en/articles/512105-how-to-install-blynk-library-for-arduino-ide)
* [Adafruit NeoPixel Library](https://github.com/adafruit/Adafruit_NeoPixel)

<br>

**Next**, you'll need to create an [LEDctrl Blynk App](https://blynk.io/en/getting-started) using the provided [clone barcode](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/src/Blynk%20App%20Clone/LEDctrl%20Blynk%20App%20Clone.png).  Once you've created a Blynk Mobile App, you'll receive an **authentication token** via email.

<br>

**After that**, open the [LEDctrl.ino](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/src/Arduino%20IDE/LEDctrl.ino) code, using Arduino IDE, and edit the following:
1. Copy and paste the **authentication token** you've received upon creating an LEDctrl Blynk Mobile App into `char auth[]`. 

```C++
// You should get Auth Token in the Blynk App.
// Go to the Project Settings (nut icon).
char auth[] = "Your Auth Token";
```

2. Add your WiFi SSID name and Password into `char ssid[]` & `char pass[]`, respectively:

```C++
// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "SSID";
char pass[] = "PASSWORD";
```

3. Change the number of LEDs/Pixel in the used LEDs' strip and the designated signal pin for the LEDs:

```C++
/*<------------------------ NeoPixel LED Ring Macros and Global Variables ------------------------>*/
#define LED_PIN    A1		//Designated pin to set addressable LEDs signal (LEDs' Data In)
#define LED_COUNT  62		//Number of LEDs/Pixel in a strip
```

*Note that you don't have to change the designated pin (A1) if you've implemented the wiring in the [Schematic/LEDctrl_Schem.png](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/Schematic/LEDctrl_Schem.png) diagram.*

4. Change the designated DATA pin & Clock pin of the PDM MEM Microphone:

```C++
#define I2S_WS_PIN     21          //I2S Word Select pin on ESP32 (GPIO 21)
#define I2S_DATA_PIN   17          //I2S Data pin on ESP32 (GPIO 17)
```

*Note that you don't have to change the designated pins (21 & 17) if you've implemented the wiring in the [Schematic/LEDctrl_Schem.png](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/Schematic/LEDctrl_Schem.png) diagram.*

<br>

**Now**, compile and upload the LEDctrl.ino source code you've just edited onto your ESP32 Microcontroller by clicking the Arduino IDE *Compile & Upload* button/arrow.
