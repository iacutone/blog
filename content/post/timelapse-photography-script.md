---
title: "Timelapse Photography Script"
date: 2018-11-17T13:59:49-05:00
draft: true
---

I want a way to auto-magically make time lapses with my digital camera. There is plethora of information on the internet in order to accomplish this task. Specifically, I would like to attach my camera to my Rapsberry Pi in order to auto-save the photos to an external hard drive. Furthermore, I would like the Pi to control the camera ISO, apeture and exposure settings. The goal is to run a script to create a timelapse. I travel often and would like to point my camera out a hotel window at night in order to capture the sunset and sunrise. In the future, I would like to attach the camera to a slow moving trolley for greater photographic effect. But, one step at a time.

The first step in automating the phototaking process is to have my my auto-take photos via [gphoto2](http://gphoto.org/). Let's inspect the meta-data from snapping a photo with the gphoto2 software.


This is a great first step in automating the timelapse process. However, in order to shoot photos throughout the night, I need the ability to adjust the camera ISO, shutter and exposture settings on the fly.


--
Helpful Resources:
[](http://blog.davidsingleton.org/raspberry-pi-timelapse-controller/)
[](https://github.com/dps/rpi-timelapse)

[](https://github.com/Moving-Electrons/TravelPhotoBackup)
[](http://www.movingelectrons.net/blog/2017/08/09/Camera-Time-lapse-Controller-with-Python-and-Raspberry-Pi.html)