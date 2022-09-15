***************************************************************
* Arduino PID Library - Version 1.2.1
* by Brett Beauregard <br3ttb@gmail.com> brettbeauregard.com
*
* This Library is licensed under the MIT License
***************************************************************

# What is PID?
Give PID a target value (like target temperature, "Setpoint") and current value (like current temperature, "Input") and PID will measure difference between those ("Error") and constanly adjusts output value (like heater power level, "Output") to match and stay at target as quickly and steady as possible. 

PID = proportional–integral–derivative.

For an ultra-detailed explanation of why the code is the way it is, please visit: 
http://brettbeauregard.com/blog/2011/04/improving-the-beginners-pid-introduction/

# Documentation:
For function documentation see:  http://playground.arduino.cc/Code/PIDLibrary

or read here: 

## PID()
### Description
Creates a PID controller linked to the specified Input, Output, and Setpoint. The PID algorithm is in parallel form.
### Syntax
`PID(&Input, &Output, &Setpoint, Kp, Ki, Kd, Direction)`
`PID(&Input, &Output, &Setpoint, Kp, Ki, Kd, POn, Direction)`
### Parameters
Input: The variable we're trying to control (double)
Output: The variable that will be adjusted by the pid (double)
Setpoint: The value we want to Input to maintain (double)
Kp, Ki, Kd: Tuning Parameters. these affect how the pid will change the output. (double>=0)
Direction: Either DIRECT or REVERSE. determines which direction the output will move when faced with a given error. DIRECT is most common.
POn: Either P_ON_E (Default) or P_ON_M. Allows Proportional on Measurement to be specified.
### Returns*
None 

## Compute()
### Description
Contains the pid algorithm. it should be called once every loop(). Most of the time it will just return without doing anything. At a frequency specified by SetSampleTime it will calculate a new Output.
### Syntax
`Compute()`
### Parameters
None
### Returns
True: when the output is computed
False: when nothing has been done 

## SetMode()
### Description
Specifies whether the PID should be on (Automatic) or off (Manual.) The PID defaults to the off position when created.
### Syntax
`SetMode(mode)`
### Parameters
mode: AUTOMATIC or MANUAL
### Returns
None 

## SetOutputLimits()
### Description
The PID controller is designed to vary its output within a given range. By default this range is 0-255: the arduino PWM range. There's no use sending 300, 400, or 500 to the PWM. Depending on the application though, a different range may be desired.
### Syntax
`SetOutputLimits(min, max)`
### Parameters
min: Low end of the range. must be < max (double)
max: High end of the range. must be > min (double)
### Returns
None 

## SetTunings()
### Description
Tuning parameters (or "Tunings") dictate the dynamic behavior of the PID. Will it oscillate or not? Will it be fast or slow? An initial set of Tunings is specified when the PID is created. For most users this will be enough. There are times however, tunings need to be changed during run-time. At those times this function can be called.
### Syntax
`SetTunings(Kp, Ki, Kd)`
`SetTunings(Kp, Ki, Kd, POn)`
### Parameters
Kp: Determines how aggressively the PID reacts to the current amount of error (Proportional) (double >=0)
Ki: Determines how aggressively the PID reacts to error over time (Integral) (double>=0)
Kd: Determines how aggressively the PID reacts to the change in error (Derivative) (double>=0)
POn: Either P_ON_E (Default) or P_ON_M. Allows Proportional on Measurement to be specified.
### Returns
None 

## SetSampleTime()
Decription
### Determines how often the PID algorithm evaluates. The default is 200mS. For robotics applications this may need to be faster, but for the most part 200mS is plenty fast.
### Syntax
`SetSampleTime(SampleTime)`
### Parameters
SampleTime: How often, in milliseconds, the PID will be evaluated. (int>0)
### Returns
None 

## SetControllerDirection()
### Description
If my Input is above Setpoint, should the output be increased or decreased? Depending on what the PID is connected to, either could be true. With a car, the output should be decreased to bring the speed down. For a refrigerator, the opposite is true. The output (cooling) needs to be increased to bring my temperature down.
This function specifies which type of process the PID is connected to. This information is also specified when the PID constructed. Since it's unlikely that the process will switch from direct to reverse, it's equally unlikely that anyone will actually use this function.
### Syntax
`SetControllerDirection(Direction);`
### Parameters
Direction: DIRECT (like a car) or REVERSE (like a refrigerator)
### Returns
None 

## Display Functions
`GetKp()`
`GetKi()`
`GetKd()`
`GetMode()`
`GetDirection()`
### Decription
These functions query the PID internals to get current values. These are useful for display purposes.
### Syntax
GetKp()
GetKi()
GetKd()
GetMode()
GetDirection()
### Parameters
None
### Returns
The corresponding internal value 
