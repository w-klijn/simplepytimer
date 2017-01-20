# simplepytimer
Measure the duration of python code by creating an timer objects with only a name.

Two simple time measurement classes:
Timer is single entrant and measure time since last occurrence.
MultiTimer remembers the name for a measure point and can be used in loops.

Display results by calling a class function

Not thread save, but if you want to do performance tests for such a program,
you should not be looking at a timer with 'simple' in it's name.

```python
import time
from simplepytimer import MultiTimer

MultiTimer("start")
time.sleep(0.1)
MultiTimer("end")

MultiTimer.print_timings()
```

## Features
1. Construct the object with only a string and create a measure point
2. Optional jump in level for displaying results
3. Optionally exclude most of the timer work in the timing results
4. Optionally export to file (csv, standard), with # comments
5. Reset internal state to Null
6. Only standard imports
7. Self test when running the python file.

## Usage
Construct two timer object with a name to start a measurement. Construct more
to get durations between the timer.
call print_timings to get the results on the screen

See run_example() for a detailed use-cases with line by line comments

### MultiTimer(name, level=0 [, exclude_timer_work=False])
    Constructor initializes a measure point. You need a minimum 
    of two to measure a stretch of time.
    
    name:  string identifier, printed in the results
  
    level: how much to jump in when printing
  
    [exclude_timer_work]: bool option available for the MultiTimer. Do not
         measure some calculations internal in the timer. The timing might be
         a little better but the total duration of the programm will no be the 
         same anymore as measured in the timer. 

### @classmethod reset()
    Clears the timer as if not being seen before.
    
     
### @classmethod print_timings(cls, header=True, seperator=" : ", prefix="  ")
    Display the results currently stored in the timer (can be called multuple times)

    header: Print a header with info of metrics before printing results

    seperator: seperator between metrics

    prefix:  What character to print before name to jump in.

### @classmethod to_file_like_as_csv(cls, fp, header=True)
    Print 
    
    fp:   'file like' object to send output data to
    
    header: Print explaining header

# run_example output
```
#Total run time time (sec)  :  1.40700006485
#% : name : count : total time spend (sec)
  0 : Start : 1 : 0.0
  7 : Second timer : 1 : 0.101000070572
  7 :   Third timer, with a jump in : 1 : 0.0999999046326
 14 : Fourth timer : 2 : 0.200999975204
 71 : Fifth timer seen 10 times! : 10 : 1.00500011444

 Second timing results:
#Total run time time (sec)  :  1.21000003815
#% : name : count : total time spend (sec)
  0 : Start : 1 : 0.0
  0 : loop : 7 : 0.000999927520752
  0 :       Timer 1 : 1 : 0.0
  0 :       Timer 10 : 10 : 0.0
  0 :       Timer 100 : 100 : 0.0
  0 :       Timer 1000 : 1000 : 0.00500011444092
  3 :       Timer 10000.0 : 10000 : 0.0319998264313
 10 :       Timer 100000.0 : 100000 : 0.117000102997
 87 :       Timer 1000000.0 : 1000000 : 1.05500006676

 Timing of the timer:
#Total run time time (sec)  :  1.21600008011
#% : name : total time spend (sec)
  0 : start : 0.0
  0 : Timer 1 : 0.0
  0 : Timer 10 : 0.0
  0 : Timer 100 : 0.0
  0 : Timer 1000 : 0.00500011444092
  3 : Timer 10000.0 : 0.0319998264313
 10 : Timer 100000.0 : 0.118000030518
 87 : Timer 1000000.0 : 1.06100010872
Press any key to continue . . .
```

# TODOS
1. Timer is not as feature complete as MultiTimer
2. Better function doc strings
3. Refactor out common print capability
4. Decorator?
5. Python 3?

Keywords: python timer timing timeit performance runtime duration