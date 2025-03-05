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
## Delta（0.5-4 Hz）
These are slower brainwaves with a flat waveform on an electroencephalogram (EEG), often appearing during deep sleep. Delta waves can be easily disturbed by muscle electrical interference when the user is awake, such as from blinking, turning the head, or frowning. If the Delta wave values are high, please ask the user to remain as still as possible when collecting data.
## Theta（4-8 Hz）
Appears during half awaken or light sleep states, sometime can also be found in deep relaxation stage during mediation.
## Alpha（8-13 Hz）
A state of deep relaxation while being awake. The brain operates more smoothly, which is the optimal state for thinking and learning.
## SMR（12-15 Hz）
SMR waves, also known as Sensorimotor Rhythm, were discovered by Dr. M.B. Sterman at California State University in San Francisco. They are found in the sensory and motor cortices of the cerebral cortex. SMR waves are closely related to the brain's state of alertness and serve as a measure of the degree of brain arousal. The enhancement of SMR waves is associated with improved attention and cognitive functions. For instance, certain neurofeedback training techniques attempt to increase the intensity of SMR waves to help alleviate symptoms in patients with Attention Deficit Hyperactivity Disorder (ADHD).
## MidBeta（15-20 Hz）
Appears during the early stage of concentration tasks, the brain’s consumption of body energy starts to increase.
## HighBeta（20-30 Hz）
Appears when highly focused, alerted, or nervous. 
## Gamma（30-50 Hz）
Associated with high level mental cognition and performance. Sometime accompanied with extreme emotions such as ecstasy, hyper excitement, or sorrow.
## Heart rate
Heart rate usually refers to the number of heartbeats per minuteThe heart of a healthy adult beats 60-100 times per minute.
## Heart rate variability
This SDK provides the RR interval values needed to calculate HRV. Heart rate usually refers to the number of heartbeats per minute, while the RR interval refers to the time distance between two consecutive R-wave peaks on an electrocardiogram (ECG). Both heart rate and HRV can be measured through RR intervals. Each RR interval is measured in milliseconds.
**Output rate:** The RR intervals are output once per second. Each output is an array, which may contain 2 to 3 RR interval data points.
**Why only provide RR values instead of directly outputting HRV? **
This is because HRV algorithms can range from short-term to long-term, even up to 24 hours. Developers need to calculate HRV based on their own customers' requirements. https://www.kubios.com/blog/hrv-analysis-methods/
## Forehead temperature
Forehead temperature: This is the temperature of user's forehead. The normal body temperature of the human body is between 36～37℃. Fever is 37.1℃. Low fever is between 37.3-38℃. High fever is between 38.1-40℃. Above 40°C, life is in danger at any time.
## Gyroscope
**Gyroscope Activation
**1. Do not turn on the brainwave module first.  
2. Assemble the brainwave module onto the headband.  
3. After placing the brainwave module **horizontally**, press and hold the power button to turn it on.
Pitch: The movement when nodding or raising the head backward.
Yaw: The rotation angle when shaking the head around the vertical axis.
Roll: The rotation angle when rotating the head side way to the right or left. 
## Signal
Its value ranges from 0 to 100. A value of 100 indicates that the electrodes are in contact with the user's skin properly.
## Battery
Its value ranges from 0 to 100. The device should be charged as soon as possible when the battery level drops below 20. Severe battery depletion can lead to an increased packet loss rate in data transmission.


# 2.Start to use this SDK, BrainLinkDualParser

**Brief Description of Functions**
This SDK is used for parsing dual-channel EEG data and supports iOS and macOS systems.
Note：Third-party developers need to write their own code for **Bluetooth scanning and connection**. The brainwave device communicates with the mobile phone via Bluetooth for data transmission.

**EEG hardware**
   - BrainLinkDual with Heart rate

**Our development environment is as follows:**
- Swift 5.0
- iOS 12
- Macos 10.13

## Class

# DualParser

### Parameters

`var delegate: DualParserDelegate?` [#](#delegate)

Data Callback Proxy

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

