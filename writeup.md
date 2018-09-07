## Reflections on Tunnig the PID Controller

Before starting to tune the parameters, I read a bit about Ziegler-Nichols method, but eventually realized that it is not practically useful for this application. 

I thought about finding parameters using optimization, which however requires defining a cost function. I came to realize that the cost function is simply not well defined. Suppose we define our cost as a total CTE over one lap. How does one evaluate such cost? One has to run the simulation with one set of values for `(Kp, Ki, Kd)` and wait for the car to complete lap. But wait, what if the car crashes on the way? That means it won't complete the lap, which means we won't be able to evaluate the cost. One way around that would be to assume that the car should need some maximum time to complete the lap. "Time" could be measured in number of data points one receives. Our cost would only sum up `T_lap` of data points (i.e. CTEs), where `T_lap` is the expected time to complete the lap under given throttle. I reasoned that if I am to do optimization, I'd rather do it in Model Predictive Control, which is more powerful than PID control. 

And thus, eventually, I decided to tune the parameters manually. In my experiments, I first started by setting all parameter values to zero and then proceeded to slowly increase the proportionality parameter. Increasing the integration gain `K_i` only led to the car deviating to the side right at the start of the lap, which is why I moved on to tunning the derivative gain `K_d`. 

Finally, I settled on values `K_p = 1e-1`, `K_i = 1e-4` and `K_d = 2.4`. Since `K_i` is fairly small, the regulator is very close to the PI controller.
