# Global Metrics

Various metrics about the current simulation's state are tracked and information about the agents is processed as the simulation runs.

## Simulation Status Display

The Simulation Status Display shows the current progress of the simulation.  It shows the current number of agents that have spawned out of the number of agents that will spawn by the time all [`AgentSpawnBlock`s](../config/simulation/agent-spawn-config.md#agentspawnblock) are processed.  It also shows the simulation's percentage of completion.

## Simulation Metrics

On the left side of the simulation screen, the Metrics Panel can be found.  It lists the following metrics:

Metric Name | Description
:-----|:----------
Max Capacity | Max number of agents that have been active in the simulation at one time.
Agents Simulating | Current number of agents active in the simulation.
Agents Processed | Number of agents that have been processed since the simulation began.
Agents in Line | Number of agents currently in line.
Total Time in Line | Sum of all time agents have spent in line since the simulation began.
Avg Time in Line | Average time any one agent has spent in line since the simulation began.

The Metrics Panel can be toggled on and off while the simulation is running with the `m` key.
