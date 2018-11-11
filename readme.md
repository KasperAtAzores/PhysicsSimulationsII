# Blender physics engine II

In this lecture we will continue to explore the physics simulations in the blender game engine.

In particular, we will look at the following three aspects:

* Elasticity and softness (30 min)
* Rigid body joints (hinges, ball and 6dof) (60 min)
* Vehicles (60 min)

### Recap from last week:
The key concepts to have from last week is:

* gravity
* collision
* center of mass
* bounding boxes

## Elasticity & softness

The examples we have seen so far, when there is a collision nothing happens, the objects stops. In the real world they might bounce (elasticity), or they might deform (like a ballon full of water).

* Elasticity (gravity05)
	* Boing - physics of materials - remember to make both objects springy
		*  Double ball bounce

* Soft objects (gravity06)
	*  Key parameters (`Shape Match`, `Liniar Stiffness`, `Margin`)
	

#### Control of the simulator
* Framerates (real time render)
* Physics steps
	* `physics_step_max`. Maximum number of physics step per game frame if graphics slows down the game, higher value allows physics to keep up with realtime
	<br>Type:	int in [1, 10000], default 5
	* `physics_step_sub`. Number of simulation substep per physic timestep, higher value give better physics precision. <br>
Type:	int in [1, 50], default 1

Example: In the `chain.blend` example. If the Scene physics are set to (5,1,30), you can see that one of the rings falls of (you can see it in wireframe mode). If you increase the `physics_step_sub` to 2, this does not happen.

## Rigid bodies - examplified by Pendulums

This [little video](https://www.youtube.com/watch?v=U39RMUzCjiU) shows the difference between a regular pendulum and a multi-arm pendulum.

### Rigid body joints constraints

Each rigid object can be attached to an other object using a `Rigid Body Joint`. 

There are two parts to the joint:
The ***owner*** of the constraint, and the ***target*** of the constraint. The target is the objects that will have its movement restricted by the owner. Often the owner will be a static object.

With the outset in (physicalBallJoint.blend) we will make the pendulum swing. Making the green parent the owner of a ball joint constraint, and the red ball the target should do the trick.

#### Multi ball pendulum
It is possible to make a multi ball pendulum in several ways. 

1. More than one ball at the same owner. Remember to make them fully elastic for the best effect.
2. Multi arm pendulum. Here you make the second ball be the target of a constraint owned by the first ball. For the best chaos effect you need the second ball to have less mass then the first.

You might even be able to combine the two types.

#### An aside

Adding sound

### A "water mill"
Just an other example I made to show how physics can do funne things. Take a look at 

### Home made joints
It actually possible to make a ball-joint without using a constraint. 
Physical ball joints (physicalBallJoint). In particular notive the margins of error and the difference in effect of the different bounding box types. It is best seen in wiremesh view.

	To do this one need to make sure:
	
	1. the location of the joint (called pivot) and the center of mass is not the same spot.
	2. BGE runs best of all physical objects are scale 1. You need to apply all rotation and scales you do. (Object menu/apply)

One of the peculiar things in blender and other physics engines is that one can join objects into a whole even when they appear to be unconnected - you do not need a stick or glue to join two objects.

##### A full chaos pendulum script

There is a script that build it. There is no constraints and rigid joints here, instead there is a ball inside a ball - making a "ball bearing". 

Notice, the script do not color the balls. I did that outside the script to be able to follow what goes on.


## Vehicles
For a vehicle to move nicely, the wheels have to turn in correspondance with the road, the wheels must turn for the car turn, there should be suspension movement if you run over a bump, and it should sink a bit to the outside in turns.

Basically there are too many forces involved to make it possible to do this using the physics engine of blender (or any other 3D real time physics simulator). Instead blender (and other 3D game engines) has a fixed way to make a vehicle.

To make a vehicle in blender you need to have:

* A body - all but the wheels
* A set of wheels

You need two kind of python scripts to run the vehicle:

* One to **set up** the vehicle (number of wheels, their properties (size, position, etc).
* One script to code **how the vehicle should move**. Mostly that will be in response to keyboard (or joystick) control, but other options are possible too.

The vehicle api has controls for driving the car (turns, speed and brake).

I have stolen an example from youtube "[Car Game Tutorials](http://blender.freemovies.co.uk/car-game-tutorials/)". All the material to make a simple moving vehicle is there. But it will take some studying and understanding of the blender api to understand all.

I have simplified the set-up script somewhat compared to the one used in the tutorial.

I have added a bumpy surface - [all is in this blender file](getStTut7_KOE.blend)

 
