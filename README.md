# Pixel 4/XL MotionSense Mod with OsloBridger App
This is the Magisk Module for the Pixel 4/4XL MotionSense mod and OsloBridger App


## OsloBridger App
It is possible to send a service intent from Tasker with an action of "com.jcarletto.oslobridger.TOGGLE_SERVICE" which will activate the service without needing to load up the UI.

## V1.1.0
I've changed the OsloBridger App to now allow for selecting a task from Tasker. Make sure "Allow External Access" is checked in the Tasker Misc Preferences. If No task is picked it will still send the normal Broadcast intents for active gestures.

### Sensor Settings:
#### Trigger Distance: 
  * Value between 1 and 10 that represents how far from the sensor a gesture triggers an intent
  * Recommended Value : 3-5

#### Gesture Sensitivity:
  * The threshold of how closely the gesture should resemble a "proper" gesture before triggering
  * Recommended Value : Low

#### Gesture Granularity:
  * How often the the bridge checks the sensor for a response,
  * Recommended Value: Medium


### Gesture Types:
#### Reach : A Single-Fire Gesture
  * Sends Intent - com.jcarletto.oslobridger.REACH_GESTURE
  * Intent Sends Extras : distance, azimuth, elevation

#### Presence : Like Reach, but ongoing
  * Sends Intent - com.jcarletto.oslobridger.PRESENCE_GESTURE
  * Expect this one to trigger constantly, try to avoid using Flashes as they'll clog up quickly
  * Intent Sends Extras : distance, confidence, angle
  * Confidence extra is not reliable in Current Soli API
  * Angle extra is not reliable in Current Soli API

#### Flick : Direction Sensitive Motion Gesture
  * Sends Intent - com.jcarletto.oslobridger.FLICK_GESTURE
  * Intent Sends Extras : direction
  * Direction is always relative to the device orientation


#### Swipe : Direction Agnostic Motion Gesture
  * Sends Intent - com.jcarletto.oslobridger.SWIPE_GESTURE
  * Intent Sends Extras : direction, intensity
  * Direction extra is not reliable in Current Soli API
  * The trigger is probably all we'll get reliably from the API here
  * intensity extra only sends 0.0f
  
Return Val | Flick/Swipe Directions
-----------|----------------
1 | E
3 | N
5 | W
7 | S
0 | Unknown/Error



#### Note about Gestures:
I recommend only having one of (Reach or Presence) enabled and one of(Swipe or Flick) enabled as one gestures output will almost certainly overpower the other.

#### Note on launching the service
I recommend launching the service from within Tasker based on criteria like the Running application is your (previously unsupported) media app, Android Auto or just when your screen is off. The intent is a toggle, so simply execute the same task to stop the service.

#### Task to launch the service from Tasker
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

