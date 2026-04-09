Simulator Driver.
The driver is case insensitive for tag and signal names.
Names cannot start with @. Every thing starting with a digit is converted into a constant number.

Can be use for internal Tags with or without arithmetic/logic operations/signals.

A pusher can be link to an simulator tag, for instance boxdetection.
A infrared sensor can be link to the same simulator tag with the same name.
… et voila when the box is close to the sensor the pusher enter in action.

Arithmetic (+ - * / %) and logic (& | ^ !)  operations can be done but only with two members.
For instance the pusher can be link to the tag name detector=sensor1 | sensor2

Several equations can be written in one line, separated by ; The used tag is the first one.
    var = a + bc ; bc = b + c  // This is an allowed comment in the tag declaration
    var = a & bc ; bc = b + !c  // ! is for boolean variable

Some simulation signals (all with an output from 0 to 1) are available and can be used in tag.

signal=sinus(periode in seconds,temporal shift in seconds, amplitude, drift) such as 
   var=sinus(8.5) for a sin with a 8.5 seconds period with an output from 0 to 1
   var=sinus(8.5,2) for the same but with a phase shifted by 2 seconds -> f(t-2)
   var=sinus(8.5,2,4) for an output from 0 to 4 given by the multiplicator factor ->f(t-2)*4
   var=sinus(8.5,2,4,-1) for an output from -1 to 3 -> f(t-2)*4-1
   all values are real, don't leave any empty value with two successive comma
   ... a conveyor speed can be linked to such a signal to simulates motor instability.

var=triangle(periode in seconds,temporal shift in seconds, amplitude, drift)
    output from 0 to 1 between 0 to periode/2 then back to 0 between periode/2 to periode
var=square(periode in seconds,temporal shift in seconds, amplitude, drift)
    output 1 between 0 to periode/2 and output 0 during the remain time
var=sawtooth(periode in seconds,temporal shift in seconds, amplitude, drift)
    output from 0 to 1 then back to 0
var=random(periode in seconds,temporal shift in seconds, amplitude, drift)
   periode and shift are only here for compatiblity with the other signals, but are required
var=user(periode in seconds,temporal shift in seconds, amplitude, drift, val1, val2, ..... valx)
   output is val1 then val2 up to valx during the periode at fixed change rate of periode/x

With simulation signal, parameters can be a tag or another signal :
    var=sinus(8,0,amplitude) ; amplitude=square(4)
       ... with an partial sinus output between 0 and 4 when the square wave is not at 0.
    var=user(4,0,1,0,var1,var2, 12, var4); var1=sinus(0.1); var2=random(); var4=4*var1
       ...sinus, then random, then a const 12 an finally the same sinus with a multiplier
