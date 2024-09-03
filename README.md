# MCD-Gesture Dataset: mmWave Cross Domain Gesture Dataset
# News
- We have released various human sensing datasets based on wireless signals, including [WiFi localization](https://github.com/H-WILD/human_held_device_wifi_indoor_localization_dataset) and [mmWave imaging](https://github.com/ruixv/RadarEyes). 
  
- This dataset has been downloaded by researchers from over **60 institutions** worldwide. 

- We have released the **raw ADC data** to support custom signal processing techniques.

# Overview
This is the dataset for paper **"Towards Domain-Independent and Real-Time Gesture Recognition Using mmWave Signal, IEEE TMC 2022".** It is an open-source mmWave gesture dataset collected from various domains (i.e. environments, users, and locations), and it can be used to develop mmWave gesture recognition systems and domain-independent machine learning algorithms. Following we introduce the composition and implementation details of this dataset. 

# Dataset Introduction
![Data collecting](https://github.com/DI-HGR/mmWave_cross_domain_gesture_dataset/blob/f1116dc135d9783a0f1a806ae63b8e577bc41a09/env.png)
- **750 domains**: 6 environments x 25 volunteers x 5 locations
- **6 environments**：meeting room, living room, bedroom, laboratory and 2 office rooms
- **25 volunteers**：25 users with different sex, ages, heights and weights.
- **5 locations**：5 anchor locations with different distances and angles away from the radar, ranging from 0.6m to 1m and -30° ,to 30°.
- **13 gestures**: 6 predefined gestures (push, pull, slide left, slide right, clockwise turning, counterclockwise turning) and 7 other actions as negative samples (lifting right arm, lifting left arm, sitting down, standing up, waving hand, turn around, walking).
- **24050 samples**: 10650 gesture samples + 13400 negative samples, with 695193 radar frames in total.

# Dataset Implementation
## Hardware Configuration
- This dataset is collected by TI AWR1843 mmWave radar (left) and DCA1000 real-time data acquisition board (right).

![dca](https://github.com/DI-HGR/mmWave_cross_domain_gesture_dataset/blob/7eea4fdf0b61f3463a1812acf46e9c2c5cf7c994/awr1843dca1000.png)

- The parameters of the radar are set as follows:

Parameter|Value|Parameter|Value
:--:|:--:|:--:|:--:
Start frequency|77GHz|Sample points |128
Frequency slope|99.987MHz/µs|Sample rate |4MHz
Idle time |340µs|Chirps in one frame |128
Ramp end time |40µs|Frame periodicity |50ms


Under these settings the radar achieves a frame rate of **20fps**, a range resolution of **0.047m**, a velocity resolution of **0.039m/s**. The number of activated transmitting antennas and receiving antennas are 2 and 4, respectively.

## Data preprocessing
The raw signals are processed into **Dynamic Range Agnle Image (DRAI)** sequences through 3D-FFT and noise elimination. DRAI depicts doppler power distribution over spatial positions when people perform gestures. For example, the following figure shows a series of DRAI when user perform gesture "push". In DRAI, the pixel intensity corresponds to doppler power, the horizontal axis is angle of arrival and the vertical axis is range. It can be observed that when users perform push, the brightest spot moves vertically which denotes distance changes of hands.

![push](https://github.com/DI-HGR/mmWave_cross_domain_gesture_dataset/blob/89f8dedbbcbbabd2eb627e8d10712dab9f5016d2/push.png)
## Dataset Structure
- The DRAI sequence of each gesture sample is saved as numpy array with 3 dimensions T x 32 x 32, where the first dimension represents the frame length of the DRAI sequence, and the last two dimensions represent the size of one frame DRAI.  The format of each .npy filename is **y/n_GestureName_EnvironmentLabel_UserLabel_PositionLabel_SampleLabel.npy** and the first character represents whether it is a predefined gesture (y) or negative sample (n). For example, the filename "y_SlideRight_e6_u21_p5_s4" denotes that it is the 4th sample of predefined gesture "SlideRight" performed by user21 at location5 in environment6.
- The example video of how to perform the predefined gestures can be viewed [here](https://github.com/DI-HGR/cross_domain_gesture_dataset/blob/df3663a87b71f58edaf694b033793218bb766ac1/gesture_sample.MP4).

- The number of samples collected from each volunteer is as follows:

User|Sample
:--:|:--:
User A-User G (7) | 7 Users x 5 Rooms x  5 Locations x (6 Gestures  x 5 Instances + 60 Negative samples) = 12250 Samples
User H-User I (2) | 2 Users x 4 Rooms x  5 Locations x (6 Gestures x 5 Instances + 60 Negative samples) = 2800 Samples
User J-User L (3) | 3 Users x 3 Rooms x 5 Locations x  (6 Gestures x 5 Instances + 60 Negative samples) = 3150 Samples
User M-User N (2) | 2 Users x 2 Rooms x 5 Locations x (6 Gestures x 5 Instances + 60 Negative samples) = 1400 Samples
User O-User R (4) | 4 Users x 1 Room x 5 Locations x (6 Gestures  x 10 Instances + 60 Negative samples) = 2000 Samples
User S-User Y (7) | 7 Users x 1 Room x 5 Locations x (6 Gestures x 5 Instances + 60 Negative samples) = 2450 Samples

# How to access the dataset
To obtain the dataset, please sign the [agreement](datasetAgreement.pdf), scan and send it to yadongli@mail.ustc.edu.cn. You will receive a notification email which includes the download links of the dataset in three days.

## Citation
-If you find this dataset useful for your research, please consider citing the following papers:
```
@ARTICLE{9894724,
  author={Li, Yadong and Zhang, Dongheng and Chen, Jinbo and Wan, Jinwei and Zhang, Dong and Hu, Yang and Sun, Qibin and Chen, Yan},
  journal={IEEE Transactions on Mobile Computing}, 
  title={Towards Domain-Independent and Real-Time Gesture Recognition Using mmWave Signal}, 
  year={2023},
  volume={22},
  number={12},
  pages={7355-7369},
  doi={10.1109/TMC.2022.3207570}}

```

```
@INPROCEEDINGS{10001175,
  author={Li, Yadong and Zhang, Dongheng and Chen, Jinbo and Wan, Jinwei and Zhang, Dong and Hu, Yang and Sun, Qibin and Chen, Yan},
  booktitle={GLOBECOM 2022 - 2022 IEEE Global Communications Conference}, 
  title={DI-Gesture: Domain-Independent and Real-Time Gesture Recognition with Millimeter-Wave Signals}, 
  year={2022},
  volume={},
  number={},
  pages={5007-5012},
  doi={10.1109/GLOBECOM48099.2022.10001175}}
```


-You may also be interested in the Human Indoor Behavior Exclusive RF dataset [HIBER](https://github.com/wuzhiwyyx/HIBER/tree/master).





