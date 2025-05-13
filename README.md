# HumanoidDataset

### Dataset Metadata (Mandatory)
The metadata should be in JSON format and contain the following information:
- Robot type (manufacturer, model, version)
- Jointdata description (e.g. number of joints, map of joint label (rShoulderRoll) to description)
- Primary task of the robot (e.g. soccer, delivery packages, etc.)
- Simulated (yes or no)
Optional Information:
- Location
- Team Color (RoboCup context)
- Robot condition (wear and tear)
- Algorithmus used (motion, controller, ...)
- Robot description by DH parameter

### Dataset
The dataset should be in [MCAP](https://mcap.dev/) format and using X as backend format.
#### Mandatory Information
- Timestamp (UNIX) in milliseconds (unsigned int)
- Gyroscope (x,y,z)
- Acceleration (x,y,z)
- Orientation (x,y)
- Joint angles (current angle)
- Joint angles (target angle)

#### Optional Information
- Image data (compressed)
  - Camera intrinsic 
- Robot state: current task of the robot (combination of e.g. grasping, fallen, walking, climbing stairs, ...)
- FSR sensor data
- Walk data:
  - State (walking or standing)
  - Request (should the robot walk)
  - Velocity (requested walk velocity)
- RoboCup Gamestate
- Compass
- Forces and torques of joints
- Current energy consumption of joints
- etc.
