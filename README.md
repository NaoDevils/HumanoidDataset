# Humanoid Robot Dataset

**This guideline is still a work in progress and is subject to change. We encourage everyone to contribute to its development by sharing feedback and suggestions.**

## Goal

The goal of this project is to crowd-source a diverse dataset of humanoid robots.
For this purpose, we propose a standardized and extensible recording container format.
The dataset will contain many such recordings of humanoid robots accomplishing different tasks in various environments including their sensor measurements, states and actions.

### How to contribute

We are happy to include your recordings in our dataset.
Please make sure, you have the minimal set of information and are allowed to publish your data under the apache-2.0 licence.

Contact us by writing to oliver dot urbann at tu-dortmund.de.

## Dataset Specification

The HumanoidDataset can be understood as a simple collection of [Recordings](#recording).
Additionally, we plan to provide a set of [Tools](#tools) for converting, visualizing and analyzing the data.

A recording is a `.mcap` file and consists out of metadata (task, robot platform, environment, ...) and a sequence of datapoints/messages (on-robot sensor measurements, inferred state, and actions) recorded on a single robot.

### Recording

#### Metadata

The metadata should be in JSON format.
It should be provided as metadata of the recording within the `.mcap` file and contain the following information:

##### Mandatory Metadata

- Robot type (manufacturer, model, version)
- Jointdata description (e.g. number of joints, map of joint label (rShoulderRoll) to description)
- Primary task of the robot (e.g. soccer, delivery packages, etc.)
- Simulated (yes or no)

##### Optional Metadata

- Location
- Team Color (RoboCup context)
- Robot condition (wear and tear)
- Algorithm used (motion, controller, ...)
- Robot description by DH parameter

### Structure of repository

To allow for easy access to specific types of recordings based on metadata, we propose a global metadata file,
which collects all the metadata of the recordings in a single file with path references to the recording `.mcap` files.

Combined with our tooling, this allows querying the dataset for specific recordings.
E.g. _"select all recordings of robots of type X, which are not simulated and have the primary task of soccer"_.

For better overview withing the repository the folder structure should be as follows:
- `recordings/` (folder containing all recordings)
  - `importer/`
    - `robot_type` (script to import the dataset)
        - `experiment|event`
            - `robot_id_date_time.mcap` (recording)
            - ...
  - ...

Example recording path: `recordings/bit-bots/wolfgang-op/robocup-2024/ID_1_2024-01-01T12:00:00.mcap`


### Dataset
The dataset should be in [MCAP](https://mcap.dev/) format and using Protobuf as backend format.

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
- Audiodata (wav)
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
