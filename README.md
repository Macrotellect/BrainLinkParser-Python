# BrainLinkParser-Python

## Python Version

- Python 3.11

## SDK

- Windows: BrainLinkParser.pyd
- Macos: BrainLinkParser.so

## Import

- from BrainLinkParser import BrainLinkParser

## Interface Parameters and Return Values

- **BrainLinkParser(eeg_callback(BrainLinkData)=None, eeg_extend_callback(BrainLinkExtendData)=None, gyro_callback(int, int, int)=None, rr_callback(int, int, int)=None, raw_callback(int)=None)** Constructor

    | Parameters     | Description     |
    | ------- | ------- |
    | eeg_callback   | EEG Data Callback Function, parameter is an object of BrainLinkData, default is None. |
    | eeg_extend_callback   | EEG Extended Data Callback Function, parameter is an object of BrainLinkExtendData, with a default value of None. |
    | gyro_callback   | Gyroscope Data Callback Function, parameters are integer values for x, y, z, with a default value of None. |
    | rr_callback   | Heartbeat RR Data Callback Function, parameters are integer values for rr1, rr2, rr3, with a default value of None. |
    | raw_callback   | Raw Data Callback Function, parameter is an integer type for 'raw', with a default value of None. |

- **parse(byteData)** Parse Data

    | Parameters     | Description     |
    | ------- | ------- |
    | byteData   | Parameter is of type 'bytes' |

## BrainLinkData Explanation

- signal

- attention

- meditation

- delta

- theta

- lowAlpha

- highAlpha

- lowBeta

- highBeta

- lowGamma

- highGamma

## BrainLinkExtendData Explanation

- ap

- battery

- version

- gnaw

- temperature

- heart

## Sample code provided for development reference

```
import time
import serial
from BrainLinkParser import BrainLinkParser

def onRaw(raw):
    # print("raw = " + str(raw))
    return

def onEEG(data):
    print("attention = " + str(data.attention) +
          " meditation = " + str(data.meditation) +
          " delta = " + str(data.delta) +
          " theta = " + str(data.theta) +
          " lowAlpha = " + str(data.lowAlpha) +
          " highAlpha = " + str(data.highAlpha) +
          " lowBeta = " + str(data.lowBeta) +
          " highBeta = " + str(data.highBeta) +
          " lowGamma = " + str(data.lowGamma) +
          " highGamma = " + str(data.highGamma))
    return

def onExtendEEG(data):
    print("ap = " + str(data.ap) +
          " battery = " + str(data.battery) +
          " version = " + str(data.version) +
          " gnaw = " + str(data.gnaw) +
          " temperature = " + str(data.temperature) +
          " heart = " + str(data.heart))
    return

def onGyro(x, y, z):
    print("x = " + str(x) + " y = " + str(y) + " z = " + str(z))
    return

def onRR(rr1, rr2, rr3):
    print("rr1 = " + str(rr1) + " rr2 = " + str(rr2) + " rr3 = " + str(rr3))
    return

parser = BrainLinkParser(onEEG, onExtendEEG, onGyro, onRR, onRaw)

ser = serial.Serial('/dev/cu.BrainLink_Pro', 115200)
try:
    while True:

        data = ser.read(512)

        parser.parse(data)

        time.sleep(0.1)

finally:
    ser.close()
```


# Use in TouchDesigner

- Macos：Place the BrainLinkParser.so file into the directory `/Applications/TouchDesigner.app/Contents/MacOS/Lib`, so that the module can be used directly within TouchDesigner
- Windows system: Place the BrainLinkParser.pyd file into the directory `C:\Program Files\Derivative\TouchDesigner\bin\Lib` to use it in TouchDesigner

![TD](https://github.com/Macrotellect/BrainLinkParser-Python/blob/main/TD.png)
