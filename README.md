# mmWave_cross_domain_gesture_dataset
This is an open-source mmWave gesture dataset collected from various domains (i.e. environments, users and locations), and it can be used to develop domain-independent gesture recognition systems based on mmWave radar. The total size of this dataset is 5.3GB and we upload it to Google drive. Following we introduce the composition and implementation details of this dataset. 
# Dataset Composition
![Data collecting setup and five anchor locations](https://github.com/DI-HGR/mmWave_cross_domain_gesture_dataset/blob/9f63656ba07b819de6dcf333e9b1aee2c5f1ac6e/datacollect.png)
- **750 domains**: 6 environments x 25 volunteers x 5 locations
- **6 environments**：meeting room, living room, bedroom, laboratory and 2 office rooms
- **25 volunteers**：25 users with different sex, ages, heights and weights.
- **5 locations**：5 anchor locations with different distances and angles away from the radar, ranging from 0.6m to 1m and -30° ,to 30°.
- **13 gestures**: 6 predefined gestures (push, pull, left swipe, right swpie, clockwise turning, anticlockwise turning) and 7 other actions as negative samples (lifting right arm, lifting left arm, sitting down, standing up, waving hand, turn around, walking).
- **24050 samples**: 10650 gesture samples + 13400 negative samples, with radar frames in total.

# Dataset Implementation
## Hardware Configuration
This dataset is collected by TI AWR1843 mmWave radar and DCA1000 real-time data acquisition board.

The parameters of the radar are set as follows:
Parameter|Value|Parameter|Value
---|:--|:---|:--:
Start frequency|77GHz|Sample points |128
Frequency slope|99.987MHz/µs|Sample rate |4MHz
Idle time |340µs|Chirps in one frame |128
Ramp end time |40µs|Frame periodicity |50ms


Under these settings the radar achieves a frame rate of **20fps**, a range resolution of **0.047m**, a velocity resolution of **0.039m/s**. We activate 2 transmitting antennas and 4 receiving antennas to obtain an approximately angular resolution of **15°**.

## Data preprocessing
The raw signals are processed into **Dynamic Range Agnle Image (DRAI)** sequences through 3D-FFT and noise elimination. DRAI depicts doppler power distribution over spatial positions when people perform gestures. For example, the following figure shows a series of DRAI when user perform gesture "push" . In DRAI, the pixel intensity corresponds to doppler power, the horizontal axis is angle of arrival and the vertical axis is range. We can observe that when users perform push, the brightest spot moves vertically which denotes distance changes of hands.

## File Structure
we save the DRAI as numpy arrays. Each 
