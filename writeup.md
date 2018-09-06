## Reflections on tunnig the PID controller

The PID controller has the form


Proportionality term

The integration is a low-pass filter

The derivative is a high-pass filter, thus amplifies noise


In my experiments I first started by setting all values to zero and then proceeded to slowly increase the proportionality parameter. 

Then I tunned the other parameters, 

I could not get rid of oscilations that crept in on the longer stretches of straight road.

Finnaly I settled on values 
K_p = 1e-1
K_i = 1e-4
K_d = 2.4
 
Since K_i is fairly small, the regulator is very close to the PI controller.
