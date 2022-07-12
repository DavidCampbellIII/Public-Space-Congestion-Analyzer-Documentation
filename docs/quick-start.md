# Simulation Quick Start

## Setting up the Environment

To correctly set up the simulation environment, there are a few main steps to follow.  First, add in all objects to the scene with their colliders, and ensure they are marked static.  Next, be sure to rebake the Nav Mesh.  Finally, set up the camera so all areas of the simulation environment area viewable.

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

Once the object has been positioned, ensure that the object has a `Collider` component attached to it.  This can be done by selecting the object, and pressing the "Add Component" button near the button of the Inspector.

Objects can contain `SphereCollider`s, `BoxCollider`s, or `MeshCollider`s.  `SphereCollider`s and `BoxCollider`s are preferred due to their simplicity and efficiency, so prefer these two colliders when possible.

If the object in question has a more complex shape, a `MeshCollider` can be used.  Read the Unity documentation for [`MeshCollider` components](https://docs.unity3d.com/Manual/class-MeshCollider.html) to see details on how to configure the component.

After the desired collider has been added to the object, modify the collider to ensure it surrounds the entirety of the object.  These collision bounds will be used in following steps to ensure the object is correctly blocked out on the Nav Mesh.

### Marking GameObjects as Static

After placing your GameObjects wherever you wish to create your environment, the only requirement is that every object in the environment that should block agents from passing through it (walls, queues, pillars, food lockers, tables, chairs etc.) **MUST** be marked as static.  To mark any GameObject as static, ensure the `Static` checkbox is checked.  The `Static` checkbox is located in the top right corner of the inspector for the current GameObject selected, to the right of the GameObject's name textbox.

If the GameObject has children GameObject's, ensure those are marked as static as well.

Any GameObject that does not directly block agents (such as [`PenaltyArea`s](config/simulation/penalty-area.md)) should **NOT** be marked as static, as this should only be done for solid, blocking objects.

### Rebaking the Nav Mesh

To rebake the Nav Mesh, first ensure all GameObjects in the scene that should block agents are [marked as static](#marking-gameobjects-as-static).

Next, open the Navigation window.  This can be found via Unity's menu bar (Window>AI>Navigation).  Select the Bake tab in the Navigation window.  Leave the settings as they are, and click the Bake button at the bottom of the Navigation window.  If done correctly, all walkable areas should be highlighted in blue, and all non-walkable areas should not be highlighted at all.

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

## Tips

- Never change **anything** while the simulation is running, as this can cause errors. Also, any changes made while the simulation is running are reverted to their origin values when the simulation is stopped
