# dataset_for_a2visr

## brief introduction
dataset_for_a2visr is a benchmark dataset for evaluating state-estimation algorithms.

It includes measurements from visual detection, UWB ranging, onboard IMU, optical flow velocity, fixed-altitude laser height, along with the corresponding ground truth from motion capture system.


## Download
### Download the a2visr pkgs to workspace:
```
git clone https://gitee.com/scarlettchen/a2visr_est.git
cd ..
catkin_make
```

### Download the dataset:
```
roscd a2VISR
git clone https://gitee.com/scarlettchen/dataset_for_a2visr.git
```

## Instructions
### Definition:
- Clear scenario: An environment with only obstacles.
- Harsh scenario: An environment with smoke interference, illumination changes, and obstacle occlusions.

### Bagfiles:
- S0: The aerial robot flies in a circular trajectory in a harsh environment, while the unmanned ground vehicle remains stationary (10 laps).
- S1: The aerial robot flies in a circular trajectory in a clear environment, while the unmanned ground vehicle remains stationary (5 laps).
- S2: The aerial robot flies in a circular trajectory in a harsh environment, while the unmanned ground vehicle remains stationary (2 laps).
- L1: Same setup as S1. Used to evaluate the case where visual measurements are set to zero during 30–40 s and 50–60 s.
- L2: Same setup as S2. Used to evaluate the case where visual measurements are set to zero during 13–28 s.
- M1: The aerial robot and the unmanned ground vehicle remain approximately stationary relative to each other in harsh environment, and the ground vehicle performs a reciprocating linear motion in the global frame.
- M2: The aerial robot flies in a circular trajectory in a clear environment, while the unmanned ground vehicle performs an L-shaped reciprocating motion.
- O1: The aerial robot flies in a circular trajectory in a long-range senario outdoors, while the unmanned ground vehicle remains stationary.
- O2: The aerial robot and the unmanned ground vehicle remain approximately stationary relative to each other in a fuzzy scenario (bicycle shed), and the ground vehicle performs a reciprocating linear motion in the global frame.

| ID  | UAV flight | UGV flight | Environment | Extra |
|--------|------------|------------|------------|------------|
| **S1** |  Circular  | Stationary |    Clear   |      —     |
| **S2** |  Circular  | Stationary |    Harsh   |      —     |
| **L1** |  Circular  | Stationary |Same as S1|Visual measurements set to zero at 30–40 s and 50–60 s|
| **L2** |  Circular  | Stationary |Same as S2|Visual measurements set to zero at 13–28 s |
| **M1** |  Relatively static  | Relatively static |    Harsh   |Reciprocating linear motion in the global frame |
| **M2** |  Circular  | L-shaped reciprocating motion |    Clear   |      —     |
| **O1** |  Circular  | Stationary |    Outdoor  |      In long-range senario     |
| **O2** |  Relatively static  | Relatively static |    Outdoor |  Reciprocating linear motion in a fuzzy scenario (bicycle shed)|

### Topics:
- IMU measurements: ```/IMU_data```
- PNP measurements: ```/camA/single_cam_process_ros/ir_mono/T_base_to_estimation```
- UWB measurements: ```/nlink_linktrack_nodeframe3```
- FLOW measurements: ```/mavros/px4flow/raw/optical_flow_rad```
- Ground truth for UAV: ```/uav201/mocap/pos```, ```/uav201/mocap/vel```
- Ground truth for UGV: ```/uwba0/mocap/pos```, ```/uwba0/mocap/vel```
- Compressed imgs: ```/camA/infra1/image_rect_raw/compressed```, ```/camA/infra2/image_rect_raw/compressed```
- TF measurements: ```/T_base_to_servogroup12```, ```/T_servogroup12_to_camA```

### note: 

- The IMU measurements are obtianed in the aerial robot's frame in a normalized form. Therefore, they need to be converted back using the gravitational acceleration before being used.
- The optical flow measurements are obtianed in the aerial robot's frame as well. 
- The pnp measurements have been already transferred to the ground vehichle's frame. They can also be re-solved using the original compressed image and TF changes.