https://github.com/caemor/epd-waveshare

https://harrystern.net/halldisplay.html

# EPD datasheet
https://github.com/CursedHardware/epd-datasheet/blob/main/epd-display.csv
https://www.waveshare.com/wiki/2.13inch_e-Paper_HAT_Manual#Demo_code
https://files.waveshare.com/upload/4/4e/2.13inch_e-Paper_V4_Specification.pdf
https://files.waveshare.com/upload/4/44/2.13inch_e-Paper_HAT_Schematic_diagram.pdf

# EPD Pins
https://forum.arduino.cc/t/waveshare-e-paper-displays-with-spi/467865?page=35
```
IoT example wiring 1.54inch e-Paper to Wemos D1 Mini:

BUSY->D6(MISO), RST->D4, DC->D3, CS->D8(SS), CLK->D5(SCK), DIN->D7(MOSI), GND->GNG, 3.3V->3.3V

SHT_SCL->D1, SHT_SDA->D2, 5V->300k->A0, D0->0.1k->RST(deep sleep wakeup)

BUSY wired to MISO to free D2 for 2-wire SHT31

2.9inch example:

BUSY->D2, RST->D4, DC->D3, CS->D8(SS), CLK->D5(SCK), DIN->D7(MOSI), GND->GND, 3.3V->3.3V
```
https://github.com/GitJer/XiaomiMiaoMiaoCe
The follwing connections (defined in XiaomiMiaoMiaoCe.h) to the ESP8266 are made:

|Breakout|ESP8266|Function|
|---|:--|:--|
|1|D2|BUSY_N|
|2|D7|SPI ENABLE|
|3|D1|SPI CLK|
|4|D6|SPI MOSI|
|5|-|not connected|
|6|D5|RST_N|
|7|3V3|VCC 3V3|
|8|GND|GND|
|9|-|not connected (VDH)|
|10|-|not connected (VDL)|

---

在電子技術中，**VCOM Pin** 通常指以下兩種定義，最常見於**顯示器面板**或**微控制器開發**：

1. 顯示面板的「公共電壓」引腳 (Common Voltage)

在 TFT-LCD 或電子紙 (e-Paper) 螢幕中，VCOM Pin 是最重要的參考電壓引腳之一。 

- **功能：** 提供像素電極的基準電壓，控制液晶分子的偏轉或電子墨水顆粒的移動。
- **重要性：** 必須精確調整 VCOM 電壓以平衡正負電荷。若 VCOM 設定不當，螢幕會出現**閃爍 (Flicker)**、**殘影 (Ghosting)** 或**影像模糊**。
- **位置：** 通常位於螢幕的 [T-CON 板 (邏輯板)](https://www.facebook.com/groups/246591440943423/posts/1089588016643757/) 或驅動 IC 上。

# Arduino Display Library for SPI E-Paper Displays
https://github.com/ZinggJM/GxEPD2
