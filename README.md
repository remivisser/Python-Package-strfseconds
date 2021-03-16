Strfseconds is a simple function that convert seconds to units of 
time. Units of time are supplied in the formatstring parameter, 
they range from week to microsecond.
All but the smallest time units are floored. The smallest time unit 
has decimals the size of the ndecimals parameter. Functionality 
looks like `timeit.default_timer` but this function allows for 
choosing which time unit to be displayed and in what format.


## Function parameters are:

- :param float or int seconds: The seconds to format
- :param str formatstring: The formatstring containing the format specifiers.
  Time units are:
  - %w for weeks
  - %d for days
  - %h for hours
  - %m for minutes
  - %s for seconds
  - %l for milliseconds (0.001 second)
  - %f for microseconds (0.000001 second)
  - %o for the unchanged seconds value
- :param int ndecimal: The number of decimals applied to the smallest unit
- :return: str: The formatted formatstring with all format specifiers replaced
- :rtype: str



# Quick start
```
from strfseconds import strfseconds
>>> print( strfseconds(seconds=1948))
00:32:28.000
```

Display same number of seconds but only in minutes
```
>>> print( strfseconds(seconds=1948, formatstring='%m', ndecimal=3))
32.466
```

Or in hours 
```
>>> print( strfseconds(seconds=1948, formatstring='%h', ndecimal=3))
0.541
```

Only the smallest time unit gets decimals, see example below with both 
days an hours

```
>>> print( strfseconds(seconds=1948, formatstring='%d days, %h hours'))
0 days, 0.541 hours
>>> 
```

## Format masks

Units can be given a format mask of zeros before the decimal sign by up to 9.
Add a number between 1 and 9 after the format specifier, '%s3' will have 
format mask '000'
```
>>> print(strfseconds(seconds=5, formatstring='%s3', ndecimal=0))
005
```

## Rounding 
In order to prevent time units from incrementing this module does not round. 
All decimal values are truncated after the decimal sign, '0.99' with 'ndecimal'
'0' will return '0'

```
>>> print(strfseconds(seconds=0.999, formatstring='%s3', ndecimal=0))
000
>>> print(strfseconds(seconds=0.999, formatstring='%s3', ndecimal=2))
000.99



