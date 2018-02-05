# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

[//]: # (Image References)

[image1]: ./images/update_eqs.png "Update Equations"

## The Model

### State

State is a vector described as follows:
```
[ x co-ordinate, y co-ordinate, orientation, velocity, cross track error, orientation error ]
```

### Actuators

Actuators can be described as a vector of following two values:
```
[ steering angle, throttle ]
```

### Update equations

![alt text][image1]

## Timestamp Length(N) and Elapsed Duration(dt) Choice

The best value in this submission is N is 15 and dt is 0.1. For the cost function the above values seem to work best i.e the car drives around the track with good stability.

I have tried the default value of 25 and 10 for N with 0.05 for dt and I noticed that the car becomes unstable quickly and drives out of the track.

I have tried 25 for N and 0.1 for dt and this seems to make the car somewhat unstable due to considering much more data across time and though the car does complete the track it wobbles a lot.

All the above tuning has been considered with speed limit of 35, 45 and 65. And 65 seems to work best with N of 15 and dt of 0.1.

## Polynomial Fitting and MPC Preprocessing

The given co-ordinates are transformed to vehicle's prespective before fitting the ploynomial of order 3. This simplies the state vector which is the input to the MPC's Solve() method. This makes x and y co-ordinates and orientation value to be 0.

## Model Predictive Control with Latency

The 100 millisecond actuation latency is handled by using the values from two time steps ago for steering angle and throttle after time step 1 to the update equations, lines 130 and 135 of MPC.cpp.



