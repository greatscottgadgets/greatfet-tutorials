## Writing a Python Program for GreatFET

Writing a GreatFET Python program is only slightly different than using the
GreatFET interactive Python shell.  The main difference is that you need to
import and instantiate the GreatFET object yourself:

```python
from greatfet import GreatFET
gf = GreatFET()
```

Here is an example of a complete program that blinks LED3 a few times:

```python
#!/usr/bin/python

import time
from greatfet import GreatFET

gf = GreatFET()

for i in range(10):
	gf.leds[3].toggle()
	time.sleep(0.2)
```

For more examples see the programs in host/greatfet/commands/.
