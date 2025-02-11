# Govee Glide Lively H610A WLED Mod

I have modded my Govee Glide Lively (Dual Connector) to WLED since my original controller got bricked by an OTA firmware update.

## Requirements
To convert the Govee controller to a WLED controller, you need the following components:
- Soldering station
- ESP32 [I bought this](https://de.aliexpress.com/item/1005006458998450.html)
- Buck converter (24V to 5V) [I bought this](https://de.aliexpress.com/item/1005006648976219.html)
- Govee Glide Lively H610A
- Jumper wires
- (Optional) 3D Printer for Case (files included)

  
![Buck Converter](/images/LM2596S.png)
![ESP32](/images/ESP32.png)

## Step 1: Flashing ESP32 with WLED
1. Connect your ESP32 to your computer via USB cable.
2. Go to the WLED website: [WLED Installer](https://install.wled.me/).
3. Follow the instructions on the website to flash WLED onto the ESP32.
4. Check if the WLED GUI is accessible via a browser. If it is, you can proceed.

## Step 2: Extracting the Cable from the Original Controller
1. Open the original controller. It is just clipped into place and can be easily opened by hand or with a small flathead screwdriver.
2. On the output side, there is a 4-pin cable connected. Desolder it carefully without damaging any of the short cables.
   I've forgotten to take a Picture of the original Controller with the Cable still attached.

## Step 3: Preparing the Buck Converter
1. The LM2596S buck converter has the correct input size for the original Govee PSU.
2. We need to bridge the 24V to the Govee cable.
3. Desolder the blue cable connector and solder a pair of jumper wires onto the original pads.
![24V Buck](/images/solder_24V.jpg)
5. On the 5V side of the buck converter, you can either screw in a pair of jumper wires or desolder and solder jumper wires onto the original pads.
![5V Buck](/images/solder_5V.jpg)

## Step 4: Connecting Buck Converter, ESP32, and Govee Cable
![Scematic](/images/scematic.jpg)
On the desoldered cable, you will see four wires:
- **Red:** +24V
- **Black:** -24V
- **Green:** Data
- **White:** Data

1. Solder the 24V jumper wires from the buck converter to the red and black wires of the original cable. Ensure you connect +24V to red and ground to black.
2. Extend the green and white wires by soldering two jumper wires.
3. Connect the +5V output of the buck converter to **VIN** on the ESP32 and the -5V output to **GND** on the ESP32.
4. Connect the green and white wires from the original cable to **GPIO 2** and **GPIO 4** on the ESP32. It does not matter which color is attached to which GPIO.
![solder Cable](/images/solder_connector.jpg)
![connection](/images/connection.jpg)

## Step 5 (Optional): Printing a Case
I designed a case for the new controller. You can download the STL files and print them if you like.
You can download the Models here [MakerWorld](https://makerworld.com/de/models/1097917)
- The buck converter and ESP32 will clip into the bottom part of the case.
- The top part can be screwed onto the bottom part using M1.4x6 screws.
- It can be tricky to get the screws into place. I recommend poking through the screw holes a few times to make them easier to use.
![bottom](/images/insert.jpg)

## Step 6: Setup
1. Connect your LEDs with the original cable and the 24V Govee PSU to the buck converter.
2. Once your ESP32 has booted, you can open the WLED GUI from your browser using its IP address.
3. Navigate to **Config -> LED Preferences -> Hardware Setup**.
4. Change the default output GPIO from **16** to **2**. The protocol is **WS281X**.
5. For each plastic LED unit, you need **4 LEDs in length**. With the original **3 units per side**, this totals **12 LEDs**.
6. Click **+** below the first LED length setting to configure a second LED output.
7. Set the **Data GPIO to 4**.
8. Again, calculate the LED length as **4 LEDs per plastic unit** and enter the value.
9. Click **Save** at the top of the WLED GUI.

Now, the entire Govee Glide should light up, and the modification is complete!
![finished](/images/finished.jpg)

If you have any questions, suggestions or want to contribute open a Issue or Pull Request

