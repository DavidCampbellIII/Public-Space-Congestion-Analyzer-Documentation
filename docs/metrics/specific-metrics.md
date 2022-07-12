# Specific Metrics

Metrics of specific elements of the simulation, such as agents and [`Waypoint`s](../config/waypoints/waypoints.md) can be viewed.

Metrics for specific agents or [`Waypoint`s](../config/waypoints/waypoints.md) can only be viewed when the simulation is running.

## Agent Metrics

To see a specific agent's metrics, simply click on the agent in the simulation.  An `AgentMetricsDisplay` will appear, and show information about the agent.

Metric Name | Description
:------|:-----------
Total time in line | Total time the agent has spent in line.
Avg time in line | Average time the agent has spent in line.
Currently in line? | Whether or not the agent is currently in a line.
In line at waypoint | If currently in a line, which waypoint the line belongs to.
Currently targeting | [`Waypoint`](../config/waypoints/waypoints.md) the agent is currently targeting.
Next waypoint target | [`Waypoint`](../config/waypoints/waypoints.md) the agent is will be targeting next.

## Waypoint Metrics

To see a specific [`Waypoint`'s](../config/waypoints/waypoints.md) metrics, simply click on the red sphere that represents the root of the [`Waypoint`](../config/waypoints/waypoints.md).  A `WaypointMetricsDisplay` will appear, and show information about the [`Waypoint`](../config/waypoints/waypoints.md).

Metric Name | Description
:------|:-----------
Max capacity | Max number of agents that have been in line for this waypoint at one time.
Total time in line | Sum of all time agents have spent in line for this waypoint.
Avg time in line | Average time a single agent has spent in line for this waypoint.
Num agents in line | Number of agents currently in line for this waypoint.
Num agents processed | Total number of agents that have been processed at this waypoint <br/>since the simulation began.
