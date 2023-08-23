# Digital_Clock with Stopwatch and Alarm implimentation using verilog
The digital alarm clock described by our Verilog hdl code has many features, such as: setting desired time on the clock, setting am/pm, setting alarm and starting a stopwatch count without pausing or disturbing the actual clock time. 
The inputs to the main module are:

Clk_1sec = This input takes a 1Hz clock pulse, to drive the clock module. 
reset = When this input is made high, the clock resets to 12:00:00 am.
set_time = When this is high, the clock takes user’s input to set its time.
set_hour = User can input hour to set up and start the clock
set_minute = User can input minute to set up and start the clock
set_am_pm = User can input 1 to set the clock at pm or keep 0 to set it at am 
alarm_hour = User can set desired alarm hour with this input 
alarm_minute = User can set desired alarm minute with this input 
alarm_am_pm = User can set desired alarm am or pm with this input. For am it is kept at 0, for pm it is kept at 1. 
stopwatch_on = This is used to turn the stopwatch on, when it is made zero after turning on stopwatch, it will hold the counted time.
stopwatch_reset = This is made high to reset the stopwatch to 00:00:00.

The outputs from the main module are:

seconds = Shows main clock’s seconds 
minutes = Shows main clock’s minutess 
hours = Shows main clock’s hourss 
am_pm = When it is am, output is 0, when it is pm, output is 1 
stopwatch_hours = Shows stopwatch’s hour count. 
stopwatch_minutes = Shows stopwatch’s minute count. 
stopwatch_seconds = Shows stopwatch’s second count. 
alarm_ringing = When the alarm rings, output becomes 1 

next are declared some internal variables, which gets changed inside the always blocks. There are two separate ‘always’ blocks; first one is for the main clock and the second block is for the stopwatch, so that one does not disturb or pause the other when running simultaneously.
First always block controls the clock functionality. In the first ‘if’ statement, if reset=1, then clock time resets to 12:00:00 am, otherwise the program moves on to the next ‘else if’ statement. Here, if set_time=1, clock’s time is set according to the user’s inputs, set_hour, set_minute, set_ampm. Then the program moves on to the next ‘else if’ statement. A 1Hz clock pulse is given as input to Clk_1sec, so it goes high every second, and else_if condition checks out. So, ‘seconds’ variable is incremented by 1 at every clock pulse. Then, when it reaches 60, ‘minutes’ variable is incremented by 1 and ‘seconds’ is made 0. Then 
the same thing happens again. After ‘minutes’ variable reaches 60, ‘hours’ variable is incremented by 1, then ‘minutes’ is made 0. Again, program goes back to the beginning of this ‘else if’ statement and the same operations happen. When ‘hours’ variable reaches 12, if time was at am, it will be pm and vice-versa. So, every time ‘hours’ reaches 12, ‘am_pm’ variable is toggled between 0 and 1. When ‘hours’ reach 13, it is made as 1, so that time is shown as 1:00:00 am or 1:00:00 pm. Thus a 12-hour clock is implemented. At the end of checking each conditional statement and incrementing, the time is compared with alarm time, and if they match, ‘alarm_ring’ is made high.   Next comes the stopwatch’s ‘always’ block. This block also operates the same way as the main clock. Difference is that, the stopwatch can count up to 23:59:59 and there is no am or pm indicator. So when the ‘stopwatch_hours’ reach 24, it is reset to 0. After turning the stopwatch on, if ‘stopwatch_on’ is made 0, it holds the previous count and can be resumed again by turning the stopwatch on. If stopwatch_reset is 1, it resets to 00:00:00.
