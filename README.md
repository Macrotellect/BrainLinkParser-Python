## BrainLink Pro is supported.
![Pro_girl](https://github.com/user-attachments/assets/5d5a1047-63f5-4135-87d2-fa34a8e66f19)
## BrainLink Lite is supported.
![Lite20240909-110821](https://github.com/user-attachments/assets/1770eaf6-7683-4ada-b8ea-bc322457f6df)
![data_stream](https://github.com/user-attachments/assets/7479371b-65a9-4000-9aa0-31282bdc5934)
# BrainLinkParser-Python（EEG data stream, Windows, MacOS, TouchDesigner）

## Python Version

- Python 3.11. You need to have a brainwave detection device(BrainLink Lite or BrainLink Pro) to use the following code.
- Buy from our website: https://o.macrotellect.com/index.html#v1
- BrainLink Pro 259 USA$

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
from cushy_serial import CushySerial
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

serial = CushySerial('/dev/cu.BrainLink_Pro', 115200)

@serial.on_message()
def handle_serial_message(msg: bytes):
    parser.parse(msg)
    # print(f"[serial] rec msg: {msg}")
```


# Use in TouchDesigner

- Macos：Place the BrainLinkParser.so file into the directory `/Applications/TouchDesigner.app/Contents/MacOS/Lib`, so that the module can be used directly within TouchDesigner
- Windows system: Place the BrainLinkParser.pyd file into the directory `C:\Program Files\Derivative\TouchDesigner\bin\Lib` to use it in TouchDesigner

![TD](https://github.com/Macrotellect/BrainLinkParser-Python/blob/main/TD.png)

# FAQ

## 1.Don't know which COM port to choose for connection in Windows system?

### video tutorial in this url https://youtu.be/ENkKVI4Av3k
After the computer's Bluetooth searches for the BrainLink Bluetooth device, pair it. The Bluetooth interface of the computer may display two BrainLink Pro device names. When pairing, please select the one with **the headphone pattern** in front of the device name.
![chooseQQ20250522-134407](https://github.com/user-attachments/assets/ae5eecde-387c-4bc5-92fe-d1136d14002f)

The computer will generate two virtual Bluetooth COM ports. When opening TouchDesigner, you don't know which COM port to choose for connection?

The correct answer is to select the output COM port for connection. So, how can you distinguish which COM port is for input and which is for output? You can go to the computer's Bluetooth settings interface, select more Bluetooth options, and then click on the COM port to see which one is the output port.
