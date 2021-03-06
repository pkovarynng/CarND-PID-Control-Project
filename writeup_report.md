# CarND-Controls-PID

Writeup report for the submission of the PID Control Project

---

## Introduction

This project implements a PID Controller in C++. The PID Controller generates steer values for a vehicle using the crosstrack error (CTE) as input from the Udacity simulator.

The steering angle generated by the PID controller is the negative sum of the products of three coefficients with their respective error terms. Each product in the sum plays a different role in the steering angle value.

The three coefficients are the following:

| coeff name | respective error term |
|:----------:|:---------------------:|
| Kp         | proportional          |
| Ki         | integral              |
| Kd         | differential          |

## Tuning

The proportional error term, p_error in the code, is the CTE. The product Kp \* p_error is the component of the steering angle that is proportional to the CTE. The effect of this component is that the vehicle oscillates around the center line. If I set only the Kp component in the code to non-zero and left the other two coeffs as zero then the oscillations became large around the first turn and the vehicle lost the road very shortly.

Watch the video of using only Kp(=-0.5): https://youtu.be/r6rADZPQI0Y 

The differential error term, d_error in the code, is the difference of the CTEs at the current and the previous timestamps. The product Kd \* d_error is the component of the steering angle that mitigates the large oscillation effects of the proportional component. And indeed, if I used Kd along with Kp, then the steering started to oscillate less and less around turns. With some tuning the vehicle could make it through the first turn of the track and then could successfully finish a whole lap.

Still not sufficiently tuned but showing some signes of improvement in the following video. The coeffs were at Kp=-0.5, Kd=-0.5, Ki=0: https://youtu.be/qsh71QQSUo8 

The integral error term, i_error in the code, is the cummulative error, the sum of the CTEs up to the current timestamp. The product Ki \* i_error is the component of the steering angle that can compensate for a bias from incorrectly calibrated steering. I did not find that the vehicle in the simulator preferred one of the two sides, so I did not use this coefficient, left it at zero.

## Final Parameters

The final parameters, the PID coefficients, were chosen through manual tuning. The final set of values are the following:

| coeff name | value |
|:----------:|:---------------------:|
| Kp         | -0.25          |
| Ki         | 0              |
| Kd         | -0.75          |

[Watch the final video](https://youtu.be/1XFYtiHuXaU)
