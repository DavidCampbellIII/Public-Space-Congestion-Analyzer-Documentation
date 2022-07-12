# WaypointPlanner

![WaypointPlanner Component](../../img/waypointPlanner.png)

## How to Locate

The `WaypointPlanner` component is located on the GameObject with the name "AgentManager", which can be found in the hierarchy.

## Settings

Setting | Description
:-------- | :------------------------------------------------------------------------------------------------------------------------------------
Ending Waypoint | Reference to the last waypoint in the simulation (such as the exit).<br />Once an agent reaches this final waypoint, they are removed from the <br />simulation.
Starting Waypoints | List of references to possible starting waypoints.<br />When an agent is first added to the simulation, they will choose one of these <br />waypoints at random to start their plan.
Waypoint Metrics <br />Display | [**ADVANCED USER SETTING**](../../about.md#advanced-user-settings). Reference to metrics display used for waypoints.
