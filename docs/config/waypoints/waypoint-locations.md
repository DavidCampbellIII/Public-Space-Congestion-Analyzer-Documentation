# WaypointLocations

![WaypointLocation Component](../../img/waypointLocation.png)

## How to Locate

The `WaypointLocation` component is located on any GameObject with a name containing "Waypoint", all of which can be found in the hierarchy.

They are typically children of GameObjects that serve as [`Waypoint`s](waypoints.md).

## Settings

Setting | Description
:-------- | :------------------------------------------------------------------------------------------------------------------------------------
Use This <br/>Location | Toggles whether or not the position of the GameObject this <br/>`WaypointLocation` is attached to represents the position agents will pathfind to.
Location | *Only applicable if `Use This Location` is `false`.*<br/>Reference to position that agents will pathfind to.
Has Queue | Toggles whether or not this location has a queue.<br/>*Note: If this is `false`, agents will not be able to form a queue to wait for this location <br/> if another agent is currently waiting at it.  This is ideal for things like seating, which don't <br/> typically have queues.*
Use Shared <br/>Queue | *Only applicable if `Has Queue` is `true`.*<br/>Toggles whether or not this location shares the same queue as another location.
Queue Location | *Only applicable if `Has Queue` is `true`.*<br/>Reference to the position of the queue for this location.<br/>Typically, this is a child of the GameObject this `WaypointLocation` is attached <br/> to, with the name "Queue Start Location".
Queue | *Only applicable if `Has Queue` and `Use Shared Queue` are `true`.*<br/>Reference to the shared queue this location uses.
Min Max <br/>Wait Time | Min and max wait time in seconds that an agent will wait at this location after <br/>arriving.  Wait time is randomly selected each time an agent arrives.
Override<br/>Outgoing<br/>Connections | Toggles whether or not this location should override the waypoint connections <br/>that are defined by the [`Waypoint`](waypoints.md) this location is a sublocation of.
Connecting <br/> Waypoints | *Only applicable if `Override Outgoing Connections` is `true`.*<br/>All possible [weighted](../../index.md#weights) waypoints an agent can visit after this specific location.<br/>*Note: These can be override the default connections defined by the [`Waypoint`](waypoints.md) <br/>this location is a sublocation of*.
Has Rigid<br/>Queue | *Only applicable if `Has Queue` is `true`.*<br/>Toggles whether or not this location has a [`RigidWaypointQueue`](rigid-waypoint-queues.md).
Rigid Queue | *Only applicable if `Has Queue` and `Has Rigid Queue` are `true`.*<br/>Reference to this location's [`RigidWaypointQueue`](rigid-waypoint-queues.md).
Has Progression<br/>Path | Toggles whether or not this location has a [`ProgressionPath`](progression-paths.md).<br/>[`ProgressionPath`s](progression-paths.md) must be a component on the same GameObject as this <br/>`WaypointLocation`.
Draw Direction <br/>Indicator | Toggles whether or not the visual that shows the direction this location faces <br/> should appear.
Direction <br/>Indicator | [**ADVANCED USER SETTING**](../../index.md#advanced-user-settings). Reference to direction indicator prefab.
Draw Line <br/>Connections | Toggles whether or not connections between each member in this location's<br/>queue should be visualized. The color of the line connection will interpolate <br/>between `Line Color Start` and `Line Color End` as it draws between each agent in the queue.
Line Color <br/>Start | *Only applicable if `Draw Line Connections` is `true`.*<br/>Starting color of the line connection visual.
Line Color <br/>End | *Only applicable if `Draw Line Connections` is `true`.*<br/>Ending color of the line connection visual.
Visualize Queue <br/>Start | Toggles whether or not the start of this location's queue should be visualized.
Visualize Queue <br/>Start Color | *Only applicable if `Visualize Queue Start` is `true`.*<br/>Color of the queue start visual.
Num Agents At <br/>Waypoint | Uneditable field.  Used for debugging how many agents are currently waiting <br/> at this location.
Print Queue <br/>Button | Button that prints the names of all agents currently in this location's queue <br/>to the console.

## Tips

- `Queue Location` should always be positioned a bit back from the `Location` of the `WaypointLocation`.  This is to ensure agents waiting at the `Location` are not too close to agents waiting at the front of the queue.
- If using a [`RigidWaypointQueue`](rigid-waypoint-queues.md), the `Queue Location` should be positioned at the back of the queue where agents would enter the queue.  This is required for Rigid Queues to work correctly.
- If `Has Progression Path` is `true`, a [`ProgressionPath` component](progression-paths.md) must also be added to the same GameObject as the related `WaypointLocation`.  The [`ProgressionPath` component](progression-paths.md) also requires a [`LerpableLine` component](lerpable-lines.md) to work correctly.
