# keigan-motor
Playing with two keigan motors https://keigan-motor.com/en/

### Setup

```sh
git clone https://github.com/keigan-motor/pykeigan_motor.git
cd pykeigan_motor
sudo python steup.py install
```

### BLE scan

Look for tools in https://github.com/keigan-motor/pykeigan_motor

### Docs

[motor settings](https://en.document.keigan-motor.com/motor-control-command/command-settings.html)

[motor commands](https://en.document.keigan-motor.com/motor-control-command/command-motor-action.html)

[Python API file](https://github.com/keigan-motor/pykeigan_motor/blob/master/pykeigan_motor/KMControllers.py)


### Example

```py
#!/usr/bin/python3

import time
from pykeigan_motor import KMControllers
m1 = KMControllers.BLEController("f8:7f:03:b6:fa:42")
m2 = KMControllers.BLEController("df:a1:59:7a:90:76")

m1.enable()
m2.enable()

m1.enableIMU()
m2.enableIMU()
m1.read_imu_measurement()
m2.read_imu_measurement()

# Default is too big (10 !)
m1.maxTorque(0.27)
m2.maxTorque(0.27)

m1.speed(5)
m2.speed(5)

# Set current position as the "zero" rad position
m1.presetPosition(0)
m2.presetPosition(0)

# Go to 5 and -5 rad
m1.moveTo(5)
m2.moveTo(-5)

# position, velocity, torque
m1.read_motor_measurement()
m2.read_motor_measurement()

time.sleep(3)  # 3 seconds

# run !
m1.runForward()
m2.runReverse()

time.sleep(3)  # 3 seconds

m1.stop()
m2.stop()

m1.free()
m2.free()

m1.disconnect()
m2.disconnect()

quit()
```