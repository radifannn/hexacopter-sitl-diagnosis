# Hexacopter SITL Simulation Diagnosis

## Purpose

This repository contains my custom hexacopter simulation for my Electrical Engineering final project.

The goal is to develop a six-rotor hexacopter simulation using Gazebo and ArduPilot SITL.

## Environment

- Ubuntu 24.04
- ROS 2 Jazzy
- Gazebo
- ArduPilot SITL

## Current simulation

Gazebo custom model:

- hexacopter
- six rotor joints
- custom hexacopter_with_ardupilot wrapper
- custom hexacopter_runway world

## Gazebo launch command

cd ~/gz_ws/src/ardupilot_gazebo

gz sim -v4 -r worlds/hexacopter_runway.sdf

## ArduPilot launch command

cd ~/ardupilot

sim_vehicle.py -v ArduCopter -f gazebo-iris --model JSON --map --console

## Current ArduPilot parameters

FRAME_CLASS = 2
FRAME_TYPE = 1

## Current status

- Gazebo successfully loads the custom six-rotor hexacopter.
- Six rotor cmd_force topics exist.
- ArduPilot SITL connects successfully.
- IMU data is available.
- GPS data is available.
- ArduPilot reports MAV Errors: 0 in the clean diagnostic run.
- The vehicle can arm.
- Actual flight/motor-response validation has not yet been completed.

## Important issue to diagnose

Please carefully inspect whether:

1. The six physical rotors are correctly mapped to ArduPilot motor outputs.
2. Rotor CW/CCW directions are correct.
3. Thrust signs and force multipliers are correct.
4. Hexa/X geometry is correct.
5. ArduPilot's internal Hexa/X motor numbering matches the physical rotor numbering in the SDF.
6. The Gazebo model and ArduPilot mixer are physically consistent.
7. The current use of `-f gazebo-iris` is appropriate or should be replaced by a dedicated hexacopter frame configuration.

Please do not assume that the simulation is correct simply because Gazebo loads successfully. I specifically want a technical audit of the motor mapping and dynamics.
