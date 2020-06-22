https://github.com/tuupola/micropython-mpu9250



# By default the library returns 3-tuple of X, Y, Z axis values for either acceleration, gyroscope and magnetometer ie compass. Default units are m/s^2, rad/s, uT and °C. It is possible to also get acceleration values in g and gyro values deg/s. See the example below. Note that both the MPU6500 and the AK8963 drivers are available as separate classes. MPU9250 is actually a composite of those two.


import utime
from machine import I2C, Pin
from mpu9250 import MPU9250

i2c = I2C(scl=Pin(22), sda=Pin(21))
sensor = MPU9250(i2c)

print("MPU9250 id: " + hex(sensor.whoami))


while True:
    print(sensor.acceleration)
    print(sensor.gyro)
    print(sensor.magnetic)
    print(sensor.temperature)

    utime.sleep_ms(1000)
    
    
# More realistic example usage with timer. If you get OSError: 26 or i2c driver install error after soft reboot do a hard reboot.

import utime
from machine import I2C, Pin
from mpu9250 import MPU9250
from mpu6500 import MPU6500, SF_G, SF_DEG_S

i2c = I2C(scl=Pin(22), sda=Pin(21))
mpu6500 = MPU6500(i2c, accel_sf=SF_G, gyro_sf=SF_DEG_S)
sensor = MPU9250(i2c, mpu6500=mpu6500)

print("MPU9250 id: " + hex(sensor.whoami))

while True:
    print(sensor.acceleration)
    print(sensor.gyro)
    print(sensor.magnetic)
    print(sensor.temperature)

    utime.sleep_ms(1000)
