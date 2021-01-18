# Unity 3D Notes

## Introduction to unity

a Unity project is simply a directory full of various asset and setting files.

Scripts in Unity are more akin to individual OOP classes and script attached to objects in the scene are object instances.

script that inherit from ``MonoBehaviour`` are component.``MonoBehaviour`` defines how component attach to game objects.

inheriting from ``MonoBehaviour`` provide:

- ``Start()`` - called once when the object is active
- ``Update()`` - called every frame

nearly all video games built around a core game loop, where the code execute in a cycle while the game is running. a **frame** is a single cycle of the looping game code.

### Unity's Pros

- productive visual workflow
- high degree of cross-platform support
- modular component system used to construct game object(mix-and-match). In a component system, object exist on a flat hierarchy and different objects have different collections of components.

### Unity Cons

- can lose track of which objects in the scene that has specific components attached.
- doesnt support linking in external code libraries(manual copy and paste only. can be solved with version control system)
- working with prefab is awkward

## Unity interfaces

### Scene View

where we:
- construct the game
- add all models, cameras, etc.
- visually place assets in the game

### Game View

where we:
- play the game
- see the mechanic work with one another
- see game in different aspect ratio

### Hierarchy window

where:
- list of all the current GameObject used

#### Scene

represent a single level in the game.

### Project window

where:
- contain all assets.
- organize assets
- all changes must be perfomed here(instead of through the OS file system) because unity maintain all assets metadata

### Inspector Window

where:
- list all components and properties of a GameObject.

### Toolbar

* from left to right
Q - hand tool
W - Translate tool
E - Rotate
R - Scale
T - rect Tool (used in 2D)
Y - transform tool

play/pause/step

**collab** button for that help big team collaborate on a single project.

**services**(cloud-like icon) to add additional Unity services like:
- cloud
- analytics
- ads
- multiplayer
- in-app purchasing
- performance report
- Collaborate
- add team members to the project
- set age restricts

**account** to manage Unity acount

**layers** for:
- prevent the rendering of GameObjects
- excluding GameObject from physics events

**Layouts** for switching, create and save layout of views in editor.

## GameObject

empty containers that can be customized by adding components.

act like folders, containing other GameObjects.

label colors and why:
- black (normal)
- blue (instance of a model or connected with a prefab)
- brown (lost connection to prefab)

important GameObject concept:

- nested GameObject allows organizing and parenting of GameObjects that are related to each other. changes to parent may affect children.
- Models are converted into GameObjects.
- everything contained in the Hirarchy is a GameObject.

## Prefabs

special type of asset that represent a GameObject or collection of GameObjects with components that are already set up.

each instance will link to the prefab asset. changing the asset will change all versions of the prefab in all Scenes.

let you save GameObjects so they're easily duplicated.

when changing prefabs, the instance change as well.

to create: grab GameObject from Hierarchy to Project window.

## Materials

determines the appearance of objects. Unity achieves this by encapsulating a shader with each material.

provide models with color and texture based upon lighting conditions.

### shader

simple program written in a C-like language that runs on the GPU to render texture on a cube, simulate water, .. etc.

## Camera

### Projection

**Perspective** - the closer the object the larger it appears(like our eye does).
**Orthographic** - object appear the same in any distance.

### Cinemachine

- one or more 'virtual' camera are created in a Scene
- Cinemachine Brain manage the virtual cameras
- Cinemachine Brain decide which virtual camera(or combination of virtual cameras) the actual camera should follow

## Physics

if GameObject doesn't have a **RigidBody** component, its considered as **static collider**(since Unity uses physics for **collision detection**).

inorder for a GameObject to react to physics, we need ``RigidBody`` and ``Collider``.

### RigidBody

marks a GameObject as something that is part of the physics system that can move.

**Is Kinematic** - if you want to move a GameObject manually, but still register for collisions. cannot be affected by external forces.

### Colliders

define the shape of an object for the purpose of physical collisions.

listen and respond to collisions.

displayed using green lines.

**Is Trigger** - **kinematic GameObjects** cant register normal collisions, but can listen to trigger events from other kinematic objects.

## Unity optimizations tips

list of unity best practice i found throughout tutorials:

- all moving GameObject must have **RigidBody** component
- using too many light will affect performance
- disable auto save when editing prefab(enabling will slow me down)
- ``thenameofmodel@animationname`` for animation file name convention
- changing a script file doesn't change the class name inside  it(it is better to delete and create a new one)
- all variable in C# use camelCase except for non-public variable which use pascalCase.

## Understanding 3D coordinate space

numbers indicate points in space and the way those numbers correlate to the space is through coordinate axes.

unity uses left-handed coordinate system.

the data type to represent a vector in Unity is called **Vector3**.

## Models

models are made up of mesh of triangles, and a Mesh Renderer "renders" that mesh.

**Skinned Mesh Renderer** allows the mesh to change shape based on the position and rotations of all of a models bones.

in Unity, models work like read-only Prefabs.  They’re blueprints for creating instances of that model, but the blueprint itself cannot be changed.

**NavMesh** is and invisible shape over the ground that defines an area within which selected GameObject can Move.

**baking** is the process of creating NavMesh.

## Animation

**Animation controllers** contain a **state Machine** which determines what animation the Animator component should be setting for its hierarchy at any given time.

 state machine makes decisions based on the current values of its **Animator Parameters**.

 types of parameter:

 - **float**
 - **int**
 - **bool**
 - **trigger**(special type of parameter which doesn't hold a value. this cause a change from one animation to another.)

**Root Motion** is the movement of a parentless/root GameObject.

**Quaternation** are a way of storing rotation as a 3D Vector.

## Lighting

two type of lighting in Unity:

- **Direct Lighting** is a specific light source, such as the sun
- **Indirect Lighting** is additional lighting that occurs when direct light bounces off surfaces

Gradient in environment lighting source is broken into three color fields:

- Sky (controls light that comes from above scene)
- Equator (controls light from horizon towards the middle of scene)
- Ground(light from below scene)

## Post Processing

involves applying filters and effects to the game image before its rendered on screen.

### Anti-aliasing

**Aliasing** is when the edge of an object looks jagged and the pixel outline can be seen.

**Anti-aliasing** is a post-processing effect that reduce the prominence of these jagged lines by surrounding them with pixels of intermediate shades of color.

### Post process Volume

the area of the game world which have profiles assigned to them.

### Ambient Occlusion

mimics the real-life effect of light not reaching tighter corners by darkening those areas.

### Vignette

darken the edges of the camera.

## UI

### Components

- **Canvas** - control how UI elements which belong to that Canvas are rendered
- **Canvas Scaler** - easy way of controlling the relative sizes of UI elements when they are displayed on different screen sizes.
- **Graphic Raycaster** - determine which UI element was clicked on and send the event to that element so the appropiate component can react.

### Rect Transform Component

the position of a Rect Transform is relative to an area of their parent(Rect Transform's Anchors) instead of a single pivot on their parent.

position of element is measured in pixels.

when the anchors are all together and they show a point, the Rect Transform shows a position in pixels that the UI element is offset from that point. if anchors are separated the Rect Transform shows a pixel offset from the sides of the anchor area.

anchors are relative to their parent: 0 is leftbottom and 1 is right top.

### Canvas Group

allows to control some aspects of all the visible UI elements on a GameObject and all of its children.

## Raycast

its possible to check whether there are any Colliders along the path of a line starting from a point.

this line is called Ray and checking a Colliders along a ray is called Raycast.

## Audio

three main parts in audio in Unity:

- Audio Clips
- Audio sources(origin of the sound in the game)
- Audio Listener (the virtual ears of the player)

the **spatial blend** of a particular Audio source determines whether it sounds like its coming from a particular point in the game world

**Audio Listener** is on Camera by default.

### Non-Diegetic Audio

has no identifiable source(e.g. soundtrack).

### Diegetic Audio

identifiable source(e.g. gunfire).

### 3D Sound Settings

**Max distance** the distance the player will start hearing the audio but faintly.

**Volume Rolloff** control the way the volume change with distance. Logarithmic by default which works well for longer distance. can be customized.

**spread** controls the range in degree that a sound seems like its coming from.

## Build, run, distribut

the application created from the editor to distribute the game to user is called **Player**.

## Quick Start

### Effects

- Particle Systems

### manipulating GameObject

method used:

- ``GetComponent`` for getting component.
- ``Vector3`` for positioning coordinate
- ``Time.Delta`` for game to move with correct Frame
- ``Transform`` for moving
- ``className`` for accessing other scripts
- ``GameObject.Find`` to access a gameObject beside the ``this`` gameObject

### User Input

method used:

- ``Input``
- ``KeyCode`` for type of keys pressed

### Animation

- ``Animator``
- ``AddForce``
- animator window
- animator clips

## Game Object Interactions

### Collisions

use method ``OnCollisionEnter`` with a parameter of a collision type.

we can manipulate the Game Object that collide with our current game Object through the parameter.

### Triggers

- ``OnTriggerEnter``.
- ``OnTriggerStay``.
- ``OnTriggerExit``.

### Raycasting

casting out a line to a certain direction from a certain point.

- ``RaycastHit``
- ``Ray``
- ``Debug.DrawRay``
- ``Physics.Raycast``

### Instantiation

copying certain prefabs. for example when instantiating a certain treasure from a chest in the game.

- ``Instantiate``

### Destruction

destroy and object when it doesnt need to appear anymore.

- ``Destroy()``

## Animation in Unity

ways to animate a game Object:

- animation clips
- modify transform component in scripts

### Animation Clips

Holds Keyframes which have data from the transform object.

## Physics fundamentals

- Rigidbody
- colliders utilizing joints
- ragdolls

### Rigidbody

- scale doesnt effect mass

#### Drag

emulate the air resistence of moving object.

#### Angular Drag

Modifies the resistance in the rotational value of the object.

#### Interpolate

because physics is running at fixed interval, and graphics can run much faster than that could cause jitteriness. Interpolate fix this.

**interpolate** - looking at the previous frame
**extrapolate** - looking at the forward frame

#### Collision Detection

for changing the rate of detection in collision.

this is helpful in detecting collisions from a fast object, preventing mismatch in detection.

higher will cost higher computation.

### Colliders

use Mesh Colliders for when the gameobject have complex shape but will be computationally expensive.

an object can have more than one colliders.

#### Mesh Colliders

**Convex** and **Inflate Mesh** - able to create a low CPU cost mesh from the original mesh of a game object

### Physic Material

#### Dynamic Friction

the amount of friction needed to apply to get an object in motion to stop.

#### Friction combine

**Combine** taking 2 values between 2 object interacting with each other and figuring out how to combine them.

### Fixed Joins

connect an object to something.(connected to the world by default)

useful for if you want to create a destructable game object.

### Spring Joins

allows interactivity between 2 objects will draw back and forth with one another.

difficult to control jittyness when too many objects joined.

### Hinge Joins

emulating how door works.

#### Use Motor

for self opening doors.

### Configurable Joints

for a very custom joints that you want.

## Wheel Collider

### Wheel Damping rate

determine how quickly the simulation is going to settle.

### Suspension distance

how far wheels goes up and down when simulating physics.

### Suspension spring

**Damper** - the higher the value faster the suspension going to a rest.

### Forward Friction

determine the amount of friction the wheel have when rolling forward.

### Sideway Friction

determine the amount of friction the wheel have when rolling sideways.

enables us to create drift.

### Sripting Wheel Colliders

the forward is the Z axis.

## C# Scripting in Unity: Beyond the Basics

### Getting Organized

- code Formatting
- Naming Conventions
- Namespaces
- effective use of Comments

### Formatting Code File

Consistency triumps style.

### C# Naming Convention for Unity

#### PascalCase

- namespaces
- classes
- structs
- Method
- Enums

#### camelCase

- fields
- all variables
- parameters

#### Guidelines

- descriptive names
- easily readable
- avoid abbrevation
- no underscore between words
- consistent

``#Region`` - to group lines of code that can be hidden in code editor.

### Types

Components of a program

- Data
- Logic

Types tells:

- The kind of data stored
- amount of memory required
- location in memory
- min and max value
- kinds of operations permitted

#### Stack vs Heap

| Stack                    | Heap                    |
| allocated when compiled  | during runtime          |
| Data stored sequentially | randomly                |
| Variable size must be known | can be unknown       |
| Not subject to garbage collection | subject to garbage collection |
| Fast | Slower |

#### Anonymous types

- unnamed container for properties
- properties are read-only
- no type name available to source code
- the type of each property is inferred

#### Enumeration

a value type that represents a set of related named integral constants. declared using ``enum``.

### Generic Types

allows to defer type declaration until use.

Benefits:

- Flexible
- Code reuse
- performance
- type safety

## Queues and Stack

both used for transient or temporary data.

### Queue

the element is stored in First In First Out.

### Stacks

the element is stored in Last In First Out.

## Coroutines

in Unity a coroutine is a function declared with a return type of IEnumerator that allows execution to be suspended and resumed using the yield keyword.

allow processes to be split across multiple frames and allows them to execute in parallel without affecting frame rate.

### Stopping Coroutines

- ``StopAllCoroutines()``
- ``StopCoroutine()``

How a coroutine is started is how it stopped.(stopping by using string or reference).

### Caveats

- can result in unexpected behaviour
- harder to debug
- can become complex and difficult to manage


## Interface

an interface contains definitions for related functionality in the form of methods, properties, events, and indexers that can be implemented by classes and structs.

## Delegation

In C# a delegate is a type designed to hold a reference to a method in a delegate object.

