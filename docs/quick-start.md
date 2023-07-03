# Simulation Quick Start

This quick start guide will teach you how to create a new simulation scene, configure new and existing simulation scenes, and run simulations!

1. [Creating a New Simulation Scene](#creating-a-new-simulation-scene)
2. [Setting up the Environment of a New or Existing Scene](#setting-up-the-environment)

## Creating a New Simulation Scene

To create a new simulation scene, simply [duplicate the example scene](#duplicating-the-example-scene) and [reconfigure the new scene](#configuring-the-new-scene) with the desired layout and settings.

### Duplicating the Example Scene

Find the example simulation scene.  It is located in the Project Panel, under the folder named "Scenes".  The example scene is named "Main".

Single click on the example scene so that it is selected, and then press `Ctrl` + `d` to duplicate the scene.  A new scene icon should appear in that folder.

Rename the new scene to whatever is desired.  To rename a file or folder, right click on it and select "Rename", or press `F2` while it is selected.

To open the new scene, simply double click on it.  To verify which scene is currently active, look at the top of the hierarchy.  The current scene name will be displayed at the top of the hierarchy next to the Unity icon.

Once the new simulation scene has been created and loaded as the current scene, the environment can be configured.

*Note: All simulations must be contained within the same Unity project, with each simulation existing in its own independent scene.<br/>To create a simulation using these tools in a brand new Unity project would require a far more detailed set up and is not within the scope of this documentation.*

### Configuring the New Scene

When configuring the environment, the following GameObjects are allowed to be duplicated, moved, deleted, or otherwise changed:

- Blocking volumes
- Waypoints
- Any object that is a part of the environment (props, walls, etc.)
- [`PenaltyArea`s](config/simulation/penalty-area.md)

**Any GameObject that is not listed above should never be moved, duplicated, or deleted.  Doing so can cause a variety of issues for that simulation scene.**

For detailed instructions on how to configure the environment, see [Setting up the Environment](#setting-up-the-environment).

---

## Setting up the Environment

To correctly set up the simulation environment, there are a few main steps to follow.

1. [Import Objects](#importing-objects-into-the-unity-project)
2. [Place Objects and Add Colliders](#placing-gameobjects-and-adding-colliders)
3. [Mark Objects as Static](#marking-gameobjects-as-static)
4. [Rebake Nav Mesh](#rebaking-the-nav-mesh)
5. [Configure Pathfinding Grid](#configure-pathfinding-grid)
6. [Set Up Simulation Camera](#setting-up-the-simulation-camera)

*Note: Steps 3 and 4 must be preformed every time anything about the environment changes.  If an object is added, moved, or removed, ensure all objects are still static, and rebake the Nav Mesh.*

### Importing Objects into the Unity Project

To import objects into the Unity project, create a folder in the Project Panel for your assets.  The folder "Raw Imports" contains the currently imported assets.

Right-click in the desired folder and select the "Import New Asset" menu option.  Alternatively, dragging and dropping the model's file into the Project Panel also works to import it into the project.

### Placing GameObjects and Adding Colliders

Once the object is imported into the project, drag and drop it into the scene.  Position it, scale it, and rotate it to the desired values.

Once the object has been positioned, ensure that the object has a `Collider` component attached to it.  This can be done by selecting the object, and pressing the "Add Component" button near the bottom of the Inspector.

Objects can contain `SphereCollider`s, `BoxCollider`s, or `MeshCollider`s.  <br/>`SphereCollider`s and `BoxCollider`s are recommended due to their simplicity and efficiency, so prefer these two colliders when possible.

If the object in question has a more complex shape, a `MeshCollider` can be used.  Read the Unity documentation for [`MeshCollider` components](https://docs.unity3d.com/Manual/class-MeshCollider.html) to see details on how to configure the component.

After the desired collider has been added to the object, modify the collider to ensure it surrounds the entirety of the object.  These collision bounds will be used in following steps to ensure the object is correctly blocked out on the Nav Mesh.

### Marking GameObjects as Static

After placing your GameObjects wherever you wish to create your environment, the only requirement is that every object in the environment that should block agents from passing through it (walls, queues, pillars, food lockers, tables, chairs etc.) **MUST** be marked as static.  To mark any GameObject as static, ensure the `Static` checkbox is checked.  The `Static` checkbox is located in the top right corner of the inspector for the current GameObject selected, to the right of the GameObject's name textbox.

If the GameObject has children GameObjects, ensure those are marked as static as well.

Any GameObject that does not directly block agents (such as [`PenaltyArea`s](config/simulation/penalty-area.md)) should **NOT** be marked as static, as this should only be done for solid, blocking objects.

### Configuring GameObjects for the Nav Mesh

After all GameObjects have been given a collider and marked as static, the next step is to ensure all objects that should block agents contain a `NavMeshModifier` component.  This component is used to tell the Nav Mesh what areas are walkable and what areas are not.
If set up correctly, the object will appear to cut out a hole in the blue walkable area of the Nav Mesh (see [Rebaking the Nav Mesh](#rebaking-the-nav-mesh)).

To add a `NavMeshModifier` component to a GameObject, select the GameObject and press the "Add Component" button near the bottom of the Inspector.  Search for "Nav Mesh Modifier" and select the component.  The default values for this component do not need to be changed.

### Rebaking the Nav Mesh

To rebake the Nav Mesh, first ensure all GameObjects in the scene that should block agents are [marked as static](#marking-gameobjects-as-static), [have colliders on them](#placing-gameobjects-and-adding-colliders), and [have a `NavMeshModifier` component](#configuring-gameobjects-for-the-nav-mesh) attached to them.

Next, find the GameObject that acts as the floor for the environment.  If you're using the duplicated example scene, this object is just called "Floor".  Make sure this Floor object has both a `NavMeshSurface` and `NavMeshModifier` component attached to it.  If not, add both components to the Floor object.  The default values for these components (whether you had to add them manually or not) are fine as they are and do not need to be changed.

Click the Bake button at the bottom of the `NavMeshSurface` component.  If done correctly, all walkable areas should be highlighted in blue, and all non-walkable areas should not be highlighted at all.

### Configure Pathfinding Grid

Once the Nav Mesh has been rebaked, the Pathfinding Grid needs to be reconfigured.  The Pathfinding Grid allows the agents to move from point to point and works with the Nav Mesh to provide accurate pathfinding.

First, locate the GameObject with the name "A\*", which can be found in the hierarchy.  There should only be a single component attached to it, called `Pathfinder`.  If a grid is not seen overlaid across your simulation environment in the Unity Scene window, scroll to the bottom of the "A\*" GameObject and ensure the option `Show Graphs` is set to `true`.

Once the grid has been located, position it near the center of the simulation environment.

After it is positioned, increase or decrease the grid size so that the entire simulation environment is covered.  This can be done by changing the `Width (nodes)` and `Depth (nodes)` settings on the `Pathfinder` component.

The grid should encompass the entire simulation environment, but it should not be any larger than necessary.  Massively large grids are slower and less accurate than smaller ones.

There are other settings on the `Pathfinder` that affect how the agents' pathfinding works, but these are all considered [**ADVANCED USER SETTINGS**](index.md#advanced-user-settings) and should only be changed if the user is absolutely certain of what they are doing.

### Setting up the Simulation Camera

Whenever a new environment for a simulation is created, the camera that views the simulation environment must be configured so all parts of the simulation are viewable.  See [CameraController](config/simulation/camera-controller.md) for details.

---

## Setting up Waypoints

Due to how the simulation works, waypoints are grouped into two categories:

- Starting/Ending Waypoints
- Main Waypoints

### Setting up Starting and Ending Waypoints

To set up the starting and ending waypoints for the simulation, use the [`WaypointPlanner` component](config/simulation/waypoint-planner.md).

### Setting up Main Waypoints

To set up all main waypoints (any waypoint that is not a starting or ending waypoint), see [Setting up Waypoints](config/waypoints/waypoints.md#setting-up-waypoints).

---

## Configuring Agent Spawn Rates

To configure the rate and frequency in which agents spawn over the duration of the simulation, use the [`AgentSpawnConfig` component](config/simulation/agent-spawn-config.md).

---

## Pathfinding and Queue Formation Influencing

One way to influence how agents pathfind from waypoint to waypoint and how queues are formed while agents wait for waypoints is with the [`PenaltyArea` object](config/simulation/penalty-area.md).

---

## Time Control

For more details about how to change the time scale of a simulation, see [Time Control](config/simulation/time-control.md).

---

## Metrics

To view and analyze metrics relating to the global state of the simulation, see [Global Metrics](metrics/global-metrics.md).

To view metrics specific to a single agent or waypoint, see [Specific Metrics](metrics/specific-metrics.md).

To view visualizations of connections between waypoints and connections between a waypoint and it's sublocations, see [Visualizations](metrics/visualizations.md).

---

## Playback and Alerts

To view simulation playback history and alert flags, see [Playback](metrics/playback.md).

To set up alerts for specific waypoints, see [Waypoint Alerts](config/waypoints/waypoints.md#setting-up-alerts).

---

## Tips

- Never change **anything** while the simulation is running, as this can cause errors. Also, any changes made while the simulation is running are reverted to their origin values when the simulation is stopped
