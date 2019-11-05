# Pixel 4/XL MotionSense Mod with OsloBridger App
This is the official Magisk Module for the Pixel 4/4XL MotionSense mod and OsloBridger App


## OsloBridger App
It is possible to send a service intent of "com.jcarletto.oslobridger.TOGGLE_SERVICE" which will activate the service without needing to load up the UI.

### Sensor Settings:
#### Trigger Distance: 
  * Value between 1 and 10 that represents how far from the sensor a gesture triggers an intent

#### Gesture Sensitivity:
  * The threshold of how closely the gesture should resemble a "proper" gesture before triggering
  * Lower triggers more often

#### Gesture Granularity:
  * How often the the bridge checks the sensor for a response,
  * Higher triggers more often


### Gesture Types:
#### Reach : A Single-Fire Gesture
  * Sends Intent - com.jcarletto.oslobridger.REACH_GESTURE
  * Intent Sends Extras : distance, azimuth, elevation

#### Presence : Like Reach, but ongoing
  * Sends Intent - com.jcarletto.oslobridger.PRESENCE_GESTURE
  * Intent Sends Extras : distance, confidence, angle
  * Confidence extra is not reliable
  * Angle extra is not reliable

#### Flick : Direction Sensitive Motion Gesture
  * Sends Intent - com.jcarletto.oslobridger.FLICK_GESTURE
  * Intent Sends Extras : direction
  * Direction is always relative to the device orientation


#### Swipe : Direction Agnostic Motion Gesture
  * Sends Intent - com.jcarletto.oslobridger.SWIPE_GESTURE
  * Intent Sends Extras : direction, intensity
  * Direction extra is not reliable, usually only sends 0
  * intensity extra only sends 0.0f
  
Return Val | Flick/Swipe Directions
-----------|----------------
1 | E
2 | NE
3 | N
4 | NW
5 | W
6 | SW
7 | S
8 | SE
Other | Unknown/Error



#### Note about Gestures:
I recommend only having one of (Reach or Presence) enabled and one of(Swipe or Flick) enabled as one gestures output will almost certainly overpower the other.


#### Launching the service from Tasker
    Start OsloBridger Service
    	A1: Send Intent [ 
     Action:com.jcarletto.oslobridger.TOGGLE_SERVICE 
     Cat:Default 
     Mime Type: 
     Data: 
     Extra: 
     Extra: 
     Extra: 
     Package: 
     Class: 
     Target:Service 
     ] 
    
