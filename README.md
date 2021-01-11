# Autosteer_USB_4.3.10_BN08x
Original AgOpenGPS Autosteer USB 4.3.10 adapted for BNO08x

# Introduction

This is an adapted version of the original AgOpenGPS Autosteer USB 4.3.10 INO code (https://github.com/farmerbriantee/AgOpenGPS/) to use BNO08x instead of MMA/Dogs2 (for roll) and/or BNO055 (for heading).
BNO08x is an Inertial Measurement Unit that use a 3-axis accelerometer, a 3-axis gyroscope and (eventually) a 3-axis magnetometer to provide yaw, pitch and roll angles.
This code is compatible with Adafruit BNO085  or Sparkfun BNO080 breakout board.
The code is based on the Sparkfun BNO080 library, with some specific improvement of the library for AgOpenGPS needs.
With this code you can choose to:
* Use BNO08x to provide roll to AgOpenGPS instead of MMA or DOGS2
* Use BNO08x to provide heading to AgOpenGPS instead of BNO055
* Use BNO08x to provide both heading and roll to AgOpenGPS

# Pinouts
## Adafruit BNO085 breakout board

Connect your BNO085 board to your AgOpenGPS PCB as follow:

__BNO085 board --> AOG PCB__

VIN --> +5V (one of the +5V pin available on the PCB): the board include a voltage regulator to step-it down to 3.3V
           
GND --> GND (one of the GND pin available on the PCB)
           
SCL --> SCL (one of the SCL pin available on the PCB)
           
SDA --> SDA (one of the SDA pin available on the PCB)
           
Note the 3.3V pin of the BNO085 breakout board is the output of the embeded voltage regulator.

## Sparkfun BNO080 breakout board

Connect your BNO080 board to your AgOpenGPS PCB as follow:

__BNO080 board --> AOG PCB__

3V3 --> +3.3V: for PCBv2, the only one available is where the MMA is normaly connected. For custom PCB, refer to this PCB layout

GND --> GND (one of the GND pin available on the PCB)
           
SCL --> SCL (one of the SCL pin available on the PCB)
           
SDA --> SDA (one of the SDA pin available on the PCB)

# Board orientation

Incomming...

# Calibration

Incomming...

# Autosteer_USB_4.3.10_BN08x configuration and upload.

File "Autosteer_USB_4.3.10_BN08x.ino" shall be placed in the ...\Support_Files\ArduinoCode\Autosteer_USB_4.3.10 folder instead of of the original "Autosteer_USB_4.3.10.ino" file.
Files "BNO08x_AOG.cpp" and "BNO08x_AOG.h" shall also be place in the ...\Support_Files\ArduinoCode\Autosteer_USB_4.3.10 folder (these are additional files that do not replace any other files in the folder).

Then, you can open the "Autosteer_USB_4.3.10_BN08x.ino" with Arduino IDE.

At the begining of the sketch, you will find some config lines:

For not "advanced user", let the config lines with "advanced user" mention into default values.

__BNO08x_ADRESS:__ adresse of the BNO, choose 0x4A for Adafruit BNO085 board, 0x4B for Sparkfun BNO080 board

__USE_BNO08X_ROLL:__ set to 1, it will force the .INO to use the BNO08x for roll instead of MMA/DOGS2 (regardless of the Inclinometer you have choose in AOG module configuration page)

__USE_BNO08X_HEADING:__ set to 1, it will force the .INO to use the BNO08x for heading instead of BNO055 (regardless if BNO is selected or not in AOG module configuration page)
 
 __USE_GAME_ROTATION:__ for advanced user, use Game Rotation Vector Report (BNO08x use only gyroscope and accelerometer to provide yaw, pitch and roll values) when set to 1 (in this mode, heading is not referenced to north). If set to 0, use Rotation Vector Report (BNO08x wil use magnetometer, gyroscope and accelerometer to provide yaw, pitch and roll values). In Rotation Vector mode, heading is normally referenced to north but to do this it's required to calibrate magnetometer (see calibration chapter above).
 
__REPORT_INTERVAL:__ for advanced user, if you want to change report interval of the Rotation Vector (or Game Rotation) Report
 
 
__ENABLE_GYRO_CAL:__ for advanced user: 
* Set to 1 if you want to enable gyroscope background calibration (not enable by default)
* Set to 2 if you want to disable background calibration for all sensors
By default, in Rotation Vector, background calibration is enable for magnetometer and accelerometer. In Game Rotation Vector, background calibration is enable only for accelerometer.

Then you can upload the sketch to your Arduino Nano.

Even if you choose to use BNO08x for roll, in the AOG module configuation page you can still choose the inclinometer axis: the "MMA axis" selection menu, will change the BNO08x axis used for roll. If you need to inverse roll value for BNO08x, you just have to activate “invert roll” in AOG module configuration page.
