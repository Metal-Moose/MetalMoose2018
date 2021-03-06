# Autonomous Parsing Language Documentation
This document covers the specifics of the autonomous language used for the Metal Moose 2018 robot.

## Introduction
The robot operates on a set of commands that it reads from the code. It then generates the actual commands to control the various subsystems of the robot.

More on this can be found in our autonomous [language guide](https://github.com/Metal-Moose/MooseGuides/blob/master/Programming/Autonomous%20language.md).

## Command Syntax
All of the commands issued to the robot are in a form `Command(p_1, p_2,..., p_n)`, where each of the parameters is a number (either decimal, or integral). As long as this syntax is present, any whitespace characters for better readability are more than welcome (before or after the commands or parameters).

The parser itself only parses the capital letters of the command, so `Timeout(2)` is the same as `T(2)`, and `DriveDistance(15)` is the same as `DD(15)`.

All of the numbers have to be in either one of the two forms bellow:
* Integral: 1, 5, -3, +7...
* Decimal: 0.6, 2.8, +9.0, -3.5...

The language allows optional parameters (for commands that have them). The form of an optional parameter is best shown on an example: `DriveDistance(10, Speed = 0.4)`.

## Commands
This part of the document goes over the specifics of the respective commands.

### Elevate
Moves the elevator into a certain position.

**Syntax:** `Elevate(position)`, where position is an integral number describing the desired position of the elevator (these are defined as an array in the RobotMap).  
**Default mode:** sequential.  
**Optional parameters:** `Mode` (Parallel/Sequential).

### Outtake
Outtake (using the collector) for a set period of time.

**Syntax:** `Outtake(time)`, where time is the number of seconds.  
**Default mode:** sequential.  
**Optional parameters:** `Speed` (Speed of the outtake).

### Timeout
Times out the drivetrain for a set period of time.

**Syntax:** `Timeout(time)`, where time is the number of seconds.  
**Default mode:** sequential.  
**Optional parameters:** N/A.

### TurnBy
Turns the robot by a certain angle.

**Syntax:** `TurnBy(angle)`, where angle is the number of degrees to turn by.  
**Default mode:** sequential.  
**Optional parameters:** `Speed` (Speed of the turning), `Mode` (Parallel/Sequential).

### TurnDrive
Turns the robot by a certain angle while simultaneously driving.

**Syntax:** `TurnDrive(angle)`, where angle is the number of degrees to turn by.  
**Default mode:** sequential.  
**Optional parameters:** `Speed` (Speed of both the turning and the driving), `Mode` (Parallel/Sequential).

### DriveDistance
Drives the robot by a certain distance.

**Syntax:** `DriveDistance(distance)`, where distance is the number of inches to drive.  
**Default mode:** sequential.  
**Optional parameters:** `Speed` (Speed of the driving), `Mode` (Parallel/Sequential).

### DriveTime
Drives the robot for a certain period of time.

**Syntax:** `DriveDistance(time)`, where time is the number of seconds to drive.  
**Default mode:** sequential.  
**Optional parameters:** `Speed` (Speed of the driving), `Mode` (Parallel/Sequential).

### Chunk and -Chunk
The main functionality of the parser is to insert the Chunk commands in places, where repetitive groups of commands would be. The main purpose is to call the commands and their respective chunks with the various layouts of the field. 

As an example: starting left and the scale being left, we can assume that it is like starting right and the scale being right, only with all the angle command having their angles reversed

**Syntax 1:** `Chunk(chunk number)`, where chunk number is the integral number of the index of the chunk from the chunk String array in RobotMap.  
**Syntax 2:** `-Chunk(chunk number)`. Does the same thing as `Chunk(chunk number)`, but note that this chunk will be inversed (all angles will be negated).