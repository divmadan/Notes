# State Estimation

---

## Sensors
- WSS (velocity, yaw rate)
    - very imprecise at high longitudinal acceleration
- Gyroscope (yaw rate)
    - independent of speed and acceleration
    - sensor drift needs to be taken into account
- Acceleration (velocity)
    - high error after a few seconds
- GPS (velocity)
    - velocity estimation with doppler effect
    - precise but time delay
- Ground Speed Sensors (velocity)
- Steering Angle (yaw rate)

## Visual Sensors
- LiDAR
    - precise
    - good for SLAM
- Camera
    - easy cone and color detection
    - low accuracy

## Estimation Techniques (Kalman)
- Used for
    - Maximum likelihood estimator
    - sensor fusion
- For estimating velocity, yaw rate, etc
- $\kappa*motion + (1-\kappa)*prediction$.
Calculate $\kappa$ by prediction and measurement errors

## Odometry (Dead Reckoning)
- Estimate pose from velocity and yaw rate over time
    - velocity estimates from GPS, WSS, accelerometers
    - yaw rate from gyroscopes, WSS
- Useful: **Locally consistent in contrast to GPS**
- Problem: Error adds up
- Visual: Estimate pose from difference in camera frames/ lidar point clouds (ICP)

## SLAM
- Necessary: visual
- Maybe: odometry (for some)
- Why not local navigation?
    - Path planning based on current observations
    - Problems
        - No long term optimmization
        - Local optimization can impact path finding (what to do has to be decided in the last moment)
- Facets
    - Dimensionality: **2D** vs 3D
    - Map representation: grid vs **landmark-based**
    - Belief correction: **particle methods** vs graph-based

## Solution approaches
1. Existing packages (ROS)
    - Sensor setup: Lidar or camera
    - Packages
        - ORB-SLAM2: Camera based, no odometry
        - LOAM: Lidar based, no odometry, no loop closure
        - LeGO LOAM: Lidar based, no odometry, loop closure
        - gmapping: Lidar based, odometry optional, grid based (problematic)
        - HectorSLAM: Lidar based, odometry optional, grid based (problematic)
2. Self made: 1
    - Low acceleration/ velocity
    - Sensor setup: Lidar, WSS
    - FastSLAM1 (particle, online)
        - Design Decision (landmark based + 2d pose estimation)
            - Cones ideal landmarks
            - world flat
        - Requires odometry: WSS
            - high precision at low speeds
            - simple to implement
        - Requires sensor for landmark detection: Lidar
            - accurate
            - at low speeds, no motion compensation required
3. Self made: 2
    - High acceleration/ velocity
    - Sensor setup: Lidar and camera, WSS, GPS, acceleration ...
    - FastSLAM1 (particle, online)
        - Design Decision (landmark based + 2d pose estimation)
        - Requires odometry: **EKF based + outlier removal**
            - EKF combines different sensors to obtain better velocity + yaw rate estimate
            - Outlier sensor measurements are removed
                - Vehicle brakes: WSS measurements are not considered valid
        - Requires sensor for landmark detection: Lidar, camera
            - motion compensation required
            - lidar + camera object fusion must be considered somehow

## Books and papers
- FASTSLAM1, FASTSLAM2 and GraphSLAM: "Probabilistic Robotics" by Sebastian Thrun
- "Robot Mapping: A survey": Sebastian Thrun
