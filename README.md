# LED Controller Blynk App with ESP32+WiFi (LEDctrl App)
In this project, a ESP32 microcontroller is used along with a Blynk app to actuate a strip of 62 WS2812B LEDs over WiFi.

Note that there's also a MP34DT01-M PDM MEMS Microphone that is being used to make the LEDs respond to the current sound volume level.

---

## Demo:
Click [*here*](https://res.cloudinary.com/dhud5kifu/video/upload/v1625382280/demos/LEDctrl_Demo_mkrkv4.mp4) to view the LEDctrl demostration video.


[![](https://res.cloudinary.com/dhud5kifu/image/upload/v1625383367/demos/demo_snippet1_stulrx.png)](https://res.cloudinary.com/dhud5kifu/video/upload/v1625382280/demos/LEDctrl_Demo_mkrkv4.mp4)

---

## Required Hardware:
* [ESP32 + WiFi Onboard](https://www.adafruit.com/product/3405)
* [WS1228B Addressable RGB LEDs strip](https://www.amazon.com/gp/product/B07BKNS7DJ/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [5V 10A DC Power Supply](https://www.amazon.com/gp/product/B07CMM2BBR/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [MP34DT01-M PDM MEMS Mic Breakout](https://www.adafruit.com/product/3492?gclid=CjwKCAjww-CGBhALEiwAQzWxOoJ1X5J6meE_1WD8ngq5gAuR29hyn-5CHDR53ZTJ1IfpZRNiy5qt3BoCwZ4QAvD_BwE)

*NOTE:* Please take a look at the [Schematic/LEDctrl_Schem.png](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/Schematic/LEDctrl_Schem.PNG) to see the LEDctrl project schematic which shows the appropriate wiring of each component mentioned just above.

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

*Note that you don't have to change the designated pin (A1) if you've implemented the wiring in the [Schematic/LEDctrl_Schem.png](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/Schematic/LEDctrl_Schem.PNG) diagram.*

4. Change the designated DATA pin & Clock pin of the PDM MEM Microphone:

```C++
#define I2S_WS_PIN     21          //I2S Word Select pin on ESP32 (GPIO 21)
#define I2S_DATA_PIN   17          //I2S Data pin on ESP32 (GPIO 17)
```

*Note that you don't have to change the designated pins (21 & 17) if you've implemented the wiring in the [Schematic/LEDctrl_Schem.png](https://github.com/an36/LED-Controller-ESP32-Blynk/blob/master/Schematic/LEDctrl_Schem.PNG) diagram.*

<br>

**Now**, compile and upload the LEDctrl.ino source code you've just edited onto your ESP32 Microcontroller by clicking the Arduino IDE *Compile & Upload* button/arrow.

---

## Notes about PDM Microphone's I2S Bus Configration:
There has been some instances where the Mic's configuration (in software) might produce faulty measurements (i.e., reading a high volume spike/pulse even though there are no loud sound/noise in the background).  This could happen if you are using another I2S Microphone (beside [MP34DT01-M PDM MEMS Mic Breakout](https://www.adafruit.com/product/3492?gclid=CjwKCAjww-CGBhALEiwAQzWxOoJ1X5J6meE_1WD8ngq5gAuR29hyn-5CHDR53ZTJ1IfpZRNiy5qt3BoCwZ4QAvD_BwE)) and/or another Microcontroller (beside [Huzzah32](https://www.adafruit.com/product/3405)).

With that being said, I recommend that you test out the Mic's input, using the provided code, to see if you are reading any faulty measurements.  After that, you can change the following flags and variables in the I2S configuration to obtain a better and more accurate reading:

* In some cases, changing the DMA buffer size (`DMA_BUFF_LEN`) to `1024`, the Sample Rate (`SAMPLE_RATE`) to `8000`, and the DMA buffers count (`DMA_BUFF_CT`) to `4` may produce more accurate results, however, I recommend that you try other values as well.

```C++
const int DMA_BUFF_CT = 2;         //number of DMA buffer (minimum 2)
const int DMA_BUFF_LEN = 32;       //samples per DMA buffer (minimum 8)
const int SAMPLE_RATE = 44100;     //44.1kHz
```

<br>

* You might also want to change the number of bits per sample (`.bits_per_sample`) and the I2S channel format (`.channel_format`).  In some case, changing the bits per sample to `I2S_BITS_PER_SAMPLE_32BIT` and the channel format to `I2S_CHANNEL_FMT_ONLY_LEFT` (or `I2S_CHANNEL_FMT_ONLY_RIGHT`) may produce better results.  You can found these under the `MicInit()` function as shown below:

```C++
/*Initializes I2S bus to start reading Mic input*/
void MicInit(){
  esp_err_t err;
  
// The I2S config
  i2s_config = {
    .mode = i2s_mode_t(I2S_MODE_MASTER | I2S_MODE_RX | I2S_MODE_PDM),     // Receive, not transfer
    .sample_rate = SAMPLE_RATE,                    
    .bits_per_sample = I2S_BITS_PER_SAMPLE_16BIT,                         //Number of bits per sample
    .channel_format = I2S_CHANNEL_FMT_RIGHT_LEFT,                         //Do not connect SEL pin.
    .communication_format = i2s_comm_format_t(I2S_COMM_FORMAT_I2S | I2S_COMM_FORMAT_I2S_MSB),
    .intr_alloc_flags = ESP_INTR_FLAG_LEVEL1,                             // Interrupt level 1
    .dma_buf_count = DMA_BUFF_CT,                                         // number of buffers
    .dma_buf_len = DMA_BUFF_LEN                                           // samples per buffer
  };
...
...
}
```

<br>

***NOTE***: if you did change the `.bits_per_sample`, then I would suggest that you change the number of bits read by `i2s_read()` function.  The `i2s_read()` function-call can be found under `MicNormValue()` function, as shown below.  

```C++
float MicNormValue(){
  // Read multiple samples at once
  int err = i2s_read(I2S_PORT, &samples, sizeof(uint16_t)*DMA_BUFF_LEN, &num_bytes_read,  (500 / portTICK_RATE_MS));  //reads two bytes (16-bit)
...
...
}
```

You can change the number of bits read by `i2s_read()` function by changing the third argument `sizeof(uint16_t)` to whicever desired size you picked.  I.e., if you've picked `I2S_BITS_PER_SAMPLE_32BIT` then you'd change the `sizeof(uint16_t)` to `sizeof(uint32_t)`.
