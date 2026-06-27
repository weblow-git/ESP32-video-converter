# 🎬 ESP32 OLED Video Player (Pro Edition)

A web-based tool for converting any video into a smooth 1-bit monochrome animation that can run on a 128x64 OLED display (SSD1306 / SH1106) using an ESP32.

This project does more than extract frames. It also includes advanced image-processing techniques commonly found in professional tools such as Image2cpp, helping your video and text stay sharp, preserve smooth gradients, and avoid turning into solid black silhouettes.

## ✨ Key Features
* 🧮 **Advanced Dithering Algorithms:** Supports **Bayer 8x8** for ultra-smooth video, **Atkinson** for reducing harsh black shadows, and **Floyd-Steinberg** for balanced error diffusion.
* 📏 **Smart Scaling & Panning:** Choose from **Best Fit**, **Stretch**, **Fill / Cover** to fill the screen without distorting aspect ratio, or **Custom** to set W, H, X, and Y manually.
* 🖋️ **Sub-Pixel Thickness Control:** Fine-tune text and line thickness with decimal precision so small details are not lost on the OLED display.
* 👁️ **NTSC Luminance Conversion:** Uses human-perception-based luminance math to detect gray and brown tones more accurately before converting them to black and white.
* ⚡ **High-Performance ESP32 Code:** Generated code uses a `millis()`-based non-blocking approach for stable FPS, plus **I2C overclocking** up to 800 kHz for smoother playback.
* 💾 **Auto-Save Settings:** All sliders and dropdowns are saved locally in your browser automatically.

## 🛠️ Required Hardware
1. **ESP32** (NodeMCU / WROOM)
2. **128x64 OLED display** with an SSD1306 or SH110X chip, using I2C
3. Jumper wires

### Pin Configuration (Standard Wiring)
| OLED Pin | ESP32 Pin |
| :---: | :---: |
| VCC | 3.3V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

## 📦 Required Software
Make sure the following libraries are installed in Arduino IDE through Library Manager:
* `Adafruit GFX Library`
* `Adafruit SSD1306` (for SSD1306-based OLEDs)
* `Adafruit SH110X` (for SH1106-based OLEDs)

## 🚀 How to Use

### 1. Extract Video in the Web Converter
1. Open the Web Converter page by opening `index.html` in your browser or visiting the project’s GitHub Pages link.
2. Load the video you want to display. *(Tip: Use the "Rotate 90°" button for vertical videos or Reels.)*
3. Adjust the **Dithering**, **Scale**, and **Line Thickness** settings until the preview looks right.
4. Click **Start Extract Frame-by-Frame** and wait for the process to finish.

### 2. Upload to ESP32
1. Click **Copy Data Array**, then paste the result into a new file/tab in Arduino IDE named `VideoFrame.h`.
2. Click **Copy Main.ino Code**, then paste it into your main Arduino sketch file.
3. In `Main.ino`, choose the OLED type you are using by uncommenting (`//`) either `#define PAKAI_SSD1306` or `#define PAKAI_SH1106`.
4. **⚠️ IMPORTANT:** The generated video array uses a lot of Flash memory, so go to **Tools > Partition Scheme** in Arduino IDE and select **"Huge APP (3MB No OTA/1MB SPIFFS)"**.
5. Click **Upload** to flash the ESP32.

## 💡 Image Tuning Tips
* **For people and landscape videos:** Use **Bayer 8x8 Dithering**. It creates a stable dot pattern that looks smooth and does not flicker as the video plays.
* **For text animations or simple cartoons:** Use **Solid Threshold**. If the text looks broken, increase **Line Thickness** toward **White +** (for example, 0.5 or 1.0).
* **To keep dark objects from merging into a silhouette:** Use **Atkinson Dithering** and slightly increase **Brightness**.

## 👨‍💻 Creator
Built and tuned with 💻 by **Weblow**.
* 📸 Instagram: [@Weblow](https://www.instagram.com/weblow.official)


If this tool helps your robotics project, thesis, or just a fun experiment, please leave a ⭐ on the repository.
