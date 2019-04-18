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
