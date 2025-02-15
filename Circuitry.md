# Circuitry

## Motor control

### Free spin.

MOTOR_ENA = 0  
MOTOR_IN1 = x  
MOTOR_IN2 = x

### Brake.

MOTOR_ENA = 1  
MOTOR_IN1 = 1  
MOTOR_IN2 = 1

### Anti-clockwise (Facing wheel)

MOTOR_ENA = pwn_speed  
MOTOR_IN1 = 1  
MOTOR_IN2 = 0

### Clockwise (Facing wheel)

MOTOR_ENA = pwn_speed  
MOTOR_IN1 = 0  
MOTOR_IN2 = 1

## Circuitry and Connections

In this project, direction refers to linear-direction, where 1 is forwards.

For rotational-direction, 1 refers to clockwise (when facing the wheel)

On the L298N, for both motors to produce identical output(same
rotational-direction)  
IN1 = IN3  
IN2 = IN4  
ENA = ENB  
OUT1 = OUT3  
OUT2 = OUT4

For connecting the motor to the L298N  
M1 -> OUT1 or OUT3  
M2 -> OUT2 or OUT4

## Rotational to Linear

For wheels on the left, a linear-direction of 1 is equal to rotational direction
0 (anti-clockwise).

For wheels on the right, a linear-direction of 1 is equal to rotational
direction 1 (clockwise).

Left  
MOTOR_IN1 = direction  
MOTOR_IN2 = !direction

right  
MOTOR_IN1 = !direction  
MOTOR_IN2 = direction

## Encoder Counting

For typical encoders, a clockwise turn increases the encoder count, and
anti-clockwise decreases it. However, to match the functionality of the
direction pin, the encoders on the left should be modified so that the encoder
count increases when the wheel moves forward.

### Left Motors

MOTOR_ENA = pwn_speed  
MOTOR_IN1 = direction  
MOTOR_IN2 = !direction  
ENC_PRI = 2  
ENC_SEC = 1

### Right Motors

MOTOR_ENA = pwn_speed  
MOTOR_IN1 = !direction  
MOTOR_IN2 = direction  
ENC_PRI = 1  
ENC_SEC = 2

## L298N Connection

The L298N breakout has become a commonly cloned part. Due to this each board is
slightly different in their tolerances and measurements. To address this, the
norm control board will take L298Ns as shields. This means instead of being
soldered on, they will be screwed on and wired up. This allows them to be
replaced if needed.

Connecting to the 3 screw terminals will be easy, using short wires soldered to
the main board, and then screwed into the L298N board. Connecting to the 6
control pins will be slightly harder, and may involve desoldering the pins from
the L298N board.

## Upside Down Board

This board is designed to be fit to the underside of the N.O.R.N. robot. This
means that the "left" motors are on the right and vice versa. The top of the
board will be at the front of the robot.

## Implementation

Controlling all 8 direction pins will be handled via a 74HCT595.
