# SentryTurret

This project licensed under GNU GENERAL PUBLIC LICENSE
https://www.gnu.org/licenses/gpl.txt

Video of a working example prior to my updating: 

<a href="http://www.youtube.com/watch?v=bgmDVvE1pLw
" target="_blank"><img src="http://img.youtube.com/vi/bgmDVvE1pLw/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

Attach raspberry pi to arduino uno that has a relay shield with usb cable
[Raspberry pi and Arduino](http://i.imgur.com/sse6CTF.jpg)

A sentry turret style robot which will detect motion, then track and fire at the object. The robot's "turret" is rotated by two servos (X/pan axis and Y/tilt axis). The "eye"(webcam) and "gun" of the robot should be mounted on the turret. The arduino is attached by usb to the raspberry pi and is given the signal to fire over serial usb.


When activated, the robot will initialize an average image and wait to detect motion above a threshold size. It will target the mean HSV of a moving object and begin blob detection to center the camera's view (using turret servos) on the object. When the object is centered, it will fire by sending a serial signal to the arduino.

See main.py for further comments.

To run with display: $python main.py 1

The program starts a thread for the turret which is continually updated with target coordinates by the OpenCV frame processing. A separate thread handles terminal keyboard input:

- q = quit
- ' ' = reset
- 1 = start motion detect
- 2 = sample center for target
- f/v = +/- threshhold area
- a,s,d/z,x,c = +/- H,S,V
- p = toggle armed
- l/m = +/- target sensitivity
- f = fire

---

The working example was built on RaspberryPi2 with Raspian and OpenCV(python) 2.4, using GPIO pins connected to a servo hat from adafruit. https://learn.adafruit.com/adafruit-16-channel-pwm-servo-hat-for-raspberry-pi/overview
Arduino uno and relay board are the fire control system
