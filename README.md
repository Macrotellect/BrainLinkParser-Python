# BrainLinkParser-Python

## 环境说明

- Python 3.6

## SDK

- BrainLinkParser-Python.pyd

## 引入模块

- from BrainLinkParser import BrainLinkParser

## 接口列表

- **BrainLinkParser(eeg_callback(BrainLinkData)=None, eeg_extend_callback(BrainLinkExtendData)=None, gyro_callback(int, int, int)=None, rr_callback(int, int, int)=None, raw_callback(int)=None)** 构造函数

    | 参数     | 说明     |
    | ------- | ------- |
    | eeg_callback   | EEG数据回调函数，参数为BrainLinkData对象，默认为None |
    | eeg_extend_callback   | EEG扩展数据回调函数，参数为BrainLinkExtendData，默认为None |
    | gyro_callback   | 陀螺仪数据回调函数，参数为整型x，y，z，默认为None |
    | rr_callback   | 心跳RR数据回调函数，参数为整型rr1, rr2, rr3，默认为None |
    | raw_callback   | 原始数据回调函数，参数为整型raw，默认为None |

- **parse(byteData)** 解析数据

    | 参数     | 说明     |
    | ------- | ------- |
    | byteData   | 参数为bytes |

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