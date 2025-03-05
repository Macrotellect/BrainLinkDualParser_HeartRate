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

Input the data that needs to be parsed.

`func startParsing()`

start to parse

`func stopParsing()`

stop parsing

## Protocol

# DualParserDelegate <a id="delegate"></a>

### Functions

`func onRaw(raw1: Int, raw2: Int)`

raw1: RawEEG of Channel one 
raw2: RawEEG of Channel two 

`func onSignal(signal: Int)`

signal: 0 - 100，100 is good.

`func onBattery(battery: Int)`

battery: 0 - 100，100 is full.

`func onFrequency(frequency1: [Float], frequency2: [Float])`

frequency1: The array length is 140, representing the values of brainwave frequencies from 0 to 70 Hz for Channel 1.
frequency2: The array length is 140, representing the values of brainwave frequencies from 0 to 70 Hz for Channel 2.

`func onEEG(eeg1: [Float], eeg2: [Float])`

eeg1: The array length is 10, representing the EEG values of Channel 1.
eeg2: The array length is 10, representing the EEG values of Channel 2.

- Delta（0.5-4 Hz）
- Theta（4-8 Hz）
- Alpha（8-13 Hz）
- SMR（12-15 Hz）
- Beta (15-30hz) : The sum of the values of MidBeta and HighBeta
- MidBeta（15-20 Hz）
- HighBeta（20-30 Hz）
- Gamma（30-50 Hz）
- Total： The sum of all brainwave values
- Max： The maximum value among all brainwave data

`func onGyro(x: Int, y: Int, z: Int)`

Gyroscope data

`func onExtend(heart: Int, rr: [Int], temperature: Float)`

heart: heart rate
rr: The RR interval data used for calculating HRV.
temperature: Forehead temperature

# 3.Other tips
**3-1** What information can be provided to help us resolve issues more quickly during the development process?
Please ask the developers to save **screenshots or videos of the error** at the first moment. Then, please provide this information to the following email address: alexander@macrotellect.com.
We will respond within 24 hours and strive to resolve all issues within 3 working days.
