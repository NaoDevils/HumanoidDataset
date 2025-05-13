# HumanoidDataset

### Dataset Metadata (Mandatory)
The metadata should be in JSON format and contain the following information:
- Robot type
- Jointdata description (e.g. number of joints, map of joint label (rShoulderRoll) to description)
- Primary task of the robot (e.g. soccer, delivery packages, climbing stairs, etc.)
- Simulated (yes or no)
Optional Information:
- Location
- Team Color (RoboCup context)

### Dataset
The dataset should be in [MCAP](https://mcap.dev/) format and using X as backend format.
#### Mandatory Information
- Timestamp in milliseconds (unsigned int)
- Gyroscope (x,y,z)
- Acceleration (x,y,z)
- Orientation (x,y)
- Joint angles (current angle)
- Joint angles (target angle)

#### Optional Information
- Image data (compressed)
  - Camera intrinsic 
- Robot state: current task of the robot
- FSR sensor data
- Walk data:
  - State (walking or standing)
  - Request (should the robot walk)
  - Velocity (requested walk velocity)
- RoboCup Gamestate
- etc.
