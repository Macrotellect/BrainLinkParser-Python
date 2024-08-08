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

## BrainLinkData类说明

- signal 设备佩戴质量，当值为200设备未佩戴，当值为0表示已经戴好

- attention 专注度

- meditation 放松度

- delta

- theta

- lowAlpha

- highAlpha

- lowBeta

- highBeta

- lowGamma

- highGamma

## BrainLinkExtendData类说明

- ap 喜好度

- battery 电量

- version 硬件固件版本

- gnaw 咬牙

- temperature 额头温度

- heart 心率

## 代码参考

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


# 在TouchDesigner中使用

- Macos：把BrainLinkParser.so放到/Applications/TouchDesigner.app/Contents/MacOS/Lib，可在TouchDesigner中直接使用模块

- Windows: 把BrainLinkParser.pyd放到C:\Program Files\Derivative\TouchDesigner\bin\Lib目录下，可在TouchDesigner中使用

![TD](https://github.com/Macrotellect/BrainLinkParser-Python/blob/main/TD.png)
