![A(%FH4(PZ8IKNOL~5`PMGT4](https://github.com/user-attachments/assets/bc184c7c-3fd5-4d32-bd35-75a7cf3e5120)
# BrainLink Dual with Heart rate is supported. 
## Not compatible with BrainLink Pro.
## Not compatible with BrainLink Lite.
## Not compatible with BrainLink Tune.
## Not compatible with BrainLink Dual without heart rate.
# Basic information of this guidance
![gpt17261921232250](https://github.com/user-attachments/assets/1b30ee62-785f-4ba6-bb40-7fcf995508f5)



# 1.Explanation for each brainwave values
## Raw EEG of 2 channels
- The original brain wave value RawData (Raw value). The range of values is (-32768, 32767), with data being 512 per second; during transmission, if packet loss occurs, the data is discarded and not displayed. The original brain wave value has no unit and is not the original signal collected by the EEG sensor, but a digital signal converted by the hardware.
- The original EEG data includes the original signals collected from two channels, namely Fp1 (left frontal) and Fp2 (right frontal).
- voltage value, the calculation formula is: voltage = Rawdata L/R * (3.3/1024) / 1100, with the unit being volts. Note that this is voltage, not high or low level, hence there will be no negative numbers; Rawdata should be a single or double precision floating-point number.

# 2.Start to use this SDK, BrainLinkDualParser

**功能：**

解析双通道脑波数据，支持iOS和Macos

**支持的硬件设备：**
   - BrainLinkDual

**支持的Swift版本**

- Swift 5.0
- iOS 12
- Macos 10.13

## Class

# DualParser

### Parameters

`var delegate: DualParserDelegate?` [#](#delegate)

数据回调代理

### Functions

`func parsing(data: [UInt8], length: Int)`

传入需要解析的数据

`func startParsing()`

开始解析

`func stopParsing()`

停止解析

## Protocol

# DualParserDelegate <a id="delegate"></a>

### Functions

`func onRaw(raw1: Int, raw2: Int)`

raw1: 通道1原始脑波
raw2: 通道2原始脑波

`func onSignal(signal: Int)`

signal: 0 - 100，0为未佩戴，100为佩戴好

`func onBattery(battery: Int)`

battery: 设备电量 0 - 100

`func onFrequency(frequency1: [Float], frequency2: [Float])`

frequency1: 数组长度为140，代表通道1脑波频率0-70hz的数值
frequency2: 数组长度为140，代表通道2脑波频率0-70hz的数值

`func onEEG(eeg1: [Float], eeg2: [Float])`

eeg1: 数组长度为10，代表通道1脑波数值
eeg2: 数组长度为10，代表通道2脑波数值

- Delta（0.5-4 Hz）：活动较缓慢的脑波，其在脑电图上的形状则是平缓的曲线，往往在深度睡眠时出现。德尔塔波在用户清醒状态下, 容易受到眨眼、转头、皱眉所产生的肌肉电干扰. 如德尔塔波数值较高, 请用户尽量保持静止再采集数据
- Theta（4-8 Hz）：浅度睡眠或半醒觉状态，在冥想中深度放松时也会出现 Theta 脑波
- Alpha（8-13 Hz）：醒觉状态下的深度放松状态。大脑运作较为畅顺，是思考和学习最佳状态
- SMR（12-15 Hz）： SMR 波，也称为传感器摩斯节律（Sensorimotor Rhythm），是由位于美国旧金山的加利福尼亚州立大学的 M.B. Sterman 博士发现的。它在大脑皮层中的感觉皮层和运动皮层被发现。SMR 波与大脑的觉醒状态密切相关，是衡量大脑觉醒程度的一个尺度。SMR 波的增强与提高注意力和认知功能有关。例如，某些神经反馈训练技术会尝试增加 SMR 波的强度，以帮助改善注意力缺陷障碍（ADHD）患者的症状
- Beta (15-30hz) : MidBeta和HighBeta
- MidBeta（15-20 Hz）：大脑较为专注的状态，精神开始集中于一项事物，同时大脑的血氧耗能也会加快
- HighBeta（20-30 Hz）：专注力高度集中，警觉或精神紧张的状态
- Gamma（30-50 Hz）：涉及较高的处理任务以及认知功能。对学习，记忆和信息处
理非常重要。同时伴随极端的情绪出现，例如喜乐、亢奋或极度沮丧等
- Total 脑波数值之和
- Max 脑波数值最大值

`func onGyro(x: Int, y: Int, z: Int)`

陀螺仪数据

`func onExtend(heart: Int, rr: [Int], temperature: Float)`

heart: 心率数据
rr: 心跳RR值
temperature: 额头温度

# 3.Other tips

