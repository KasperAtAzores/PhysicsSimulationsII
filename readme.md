# Blender physics engine II

In this lecture we will continue to explore the physics simulations in the blender game engine.

In particular, we will look at the following four aspects:

* Elasticity and softness
* Rigid body joints (hinges, ball and 6dof)
* Vehicles

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
	

## Control of the simulator
* Framerates
* Physics steps
	* `physics_step_max`. Maximum number of physics step per game frame if graphics slows down the game, higher value allows physics to keep up with realtime
	<br>Type:	int in [1, 10000], default 5
	* `physics_step_sub`. Number of simulation substep per physic timestep, higher value give better physics precision. <br>
Type:	int in [1, 50], default 1

Example: In the `chain.blend` example. If the Scene physics are set to (5,1,30), you can see that one of the rings falls of (you can see it in wireframe mode). If you increase the `physics_step_sub` to 2, this does not happen.

## Pendulums

This [little video](https://www.youtube.com/watch?v=U39RMUzCjiU) shows the difference between a regular pendulum and a multi-arm pendulum.

### Rigid body joints

Each rigid object can be attached to an other object using a `Rigid Body Joint`. 

With the outset in (joints01) we will make the pendulum swing. To do this one need to make sure the location of the joint (called pivot) and the center of mass is not the same spot.

* Notice, the pivot can be outside of the child object.
* Notice, the pivot of the child is relative to the center of mass of the parent.

Explain physical ball joints (physicalBallJoint). In particular notive the margins of error and the difference in effect of the different bounding box types. It is best seen in wiremesh view.

One of the peculiar things in blender and other physics engines is that one can join objects into a whole even when they appear to be unconnected - you do not need a stick or glue to join two objects.

### A full chaos pendulum script

Notice, the script do not color the balls.
