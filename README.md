# AdvancedKinematicController01
A repo holding a Unity Package for Character Controller 
## How to Use: 

* Clone the repo 
* Import the package in Unity 
* In the Character folder, go in TimDete and place the Prefab in your scene
* Select the camera > Add Component > kCam
    * Fill the `Target`, `LookAtTarget`, and `RotationSpeed` fields
* In the TimDete GameObject in the Scene, scroll to kBase and in drop the Camera in the Cam field 
* Enjoy ! 

Check the video at: https://youtu.be/QGN-734hLh4

## Careful ! 
I have my own conventions for inputs name, so make sure to check the `kInput` script to change the name in order to match your config. 


## 18/04 Update: 

* Added support for dash 
* Added support for hit detection. This process relies on a message passing between various scripts. On entering a hit animation, the `tFightInform` script passes the hit information to the fighting module, which activates the adequate hitbox. If the hitbox collides with a hurtbox while being activated, it will give to the hurtbox the hit data (impact strengh, animation to play...) which again will call the fight module with relevant informations. Hit and impact are specific states that imply particular movement function. Specifically, when hitting, the character mobility is somewhat restrained. Also, when being impacted, the movement is driven by the hit animation data. 

Video at: https://youtu.be/CYrc3MgrWUw

## 20/04 Update 

* Added support for locking
* Added CameraShake for hits, and hit effects 

The class used to convey Hit informations to relevant scripts (`HitAnimationData` holding informations such as hit power, impulsion...) has been enhanced with an instance of the `ShakeParameters` class, which, as its name suggests holds the shake parameters related to this specific hit. Which means you can define shakes per hit if needed.  


Video at: https://youtu.be/Sum0ciAz1JE

# 04/05 Update 

This update introduces a important change. Now, all camera movements and effects rely on Cinemachine (which is such a great package, by the way). 

More specifically, the main changes are: 
* Free look Camera for normal mode, using orbits. 
* Impulses are replacing the previous CameraShake approach. 
* FightMode camera for keeping enemy in sight when locked to it


**Notes**: 
* For the camera shake on impact: Impulses are created by the `FightModule` using informations from `HitAnimationData`. It is similar to the previous approach, except that this time, the Impulses are defined to fit Cinemachine expectations. 
* Entering fight mode does two things: Changes the character movement to always face the enemy and adapts some animator values. Changes the priority of the Virtual Camera used for fighting. This camera binding mode is LockToTargetWithWorldUp to clip the x axis value (using SimpleFollow won't allow you to do so). Currently the system is not robust as it only lerps the x axis value to be a constant (-15° in the video). 


Video at: https://youtu.be/yrQGPQ9TPJs

# 05/05 Update

Some quick fixes and a few additions. 
* Added some trails for dashing and hit. They are trails attached to particles. The particles themselves are not rendered, only the trails. These are attached to Empties with the Hitbox script that has been extended to deal with Dashboxes as well. When activated, they will create an instance of the trail effect and destroy it a moment later. Some parameters allow the user to manage the created instance can (whether it will be a children of the box, inital rotation settings and so on)

* Snapping to enemy. Now, this is a cool feature, in my opinion. When locked to a target, if the player asks to hit, the character will quickly snap to the foe it is fighting. There a threshold distance that terminates the process when the player is close enough. I feel this feature adds a lot of punch to the prototype. 

* Enemy impact. I created a ImpactBehaviour class for handling impacts more easily, given the incresing complexity. Relies on a state machine with three states: **normal**, **heavy** and **wall**. Heavy hits (in particular in combo's end), can be set to indicate that this is a projection hit. This set the Impact behaviour to **heavy**  and sends the enemy flying for a short amount of time (controllable from the ImpactBehaviour class parameters, along with speed). When time's over, the animator is set to play the normal impact animation before getting back to normal state. Meanwhile, a `raycast` is sent for behind the character and if a wall is close enough, we enter the **wall** state, which plays the WallImpact animation. 

Video at: https://youtu.be/agAXrZQQBo4


