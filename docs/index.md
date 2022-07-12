# About

This program was created as an internal tool to help simulate the amount of congestion in a public area, and analyze how the placement of queues and waypoints can affect the throughput of agents over a duration of time.

## Advanced User Settings

Advanced User Settings are settings that should not be changed or reconfigured unless the user knows exactly what they are doing.  All Advanced User Settings are specifically labeled on all settings defined in these docs.

**These settings are already configured, and the average user should NEVER need to change them.**

Changing Advanced User Settings can easily break the entire simulation if not careful.

Not all configurable parts of this program are listed in this documentation.  It is restricted to only the most essential pieces that the average user will be required to understand and configure.

## Weights

Many elements of this program use the concept of weights.  This is a way to assign a certain basis that an element will be selected randomly from a group of other elements.  Whenever a weight is used in relation to something in this program, it does **NOT** represent a percent chance that element will be selected.  Rather, it represents the weight relative to the weights of the other elements in the group that it will be selected.

For example, if two elements in a list have a weight of 1, this does not mean they both have a 100% chance of being selected, but rather that they both have an equal chance of being selected.  This is because relative to one another, they have the same weight, with each of their respective weights making up 50% of the total weight of the group (which also gives them each a 50% chance of spawning).

Similarly, if one element in a group has a weight of 0.5, and the another has a weight of 0.05, it does not mean they have a respective chance of 50% and 5% of being selected. That would only equate to 55%, meaning 45% of the time, nothing would be selected (which doesn't make much sense).  Instead, the total weight pool of all elements in the group is 0.55.  The element with the weight of 0.5 makes up roughly 90% of the total weight pool, which means the element with a weight of 0.05 has only about a 10% chance of spawning relative to the first.

## Simulation Limitations

Currently, the simulation has a few limitations in its functionality.  Here are the most noticeable:

- Long queues that push into walls perpendicular to the average direction of the queue don't always wrap correctly
- Poor performance when using the `ALWAYS` local avoidance type.  This is unavoidable without huge changes to the underlying agent logic to convert it to an ECS-based architecture.
- Simulation may be inaccurate in pathfinding and agent processing at high simulation time scales.  If you notice poor framerate while simulating, and accuracy is also an issue, try turning down the time scale for improvements
- Creation and setup of [`ProgressionPath`s](config/waypoints/progression-paths.md) and [`LerpableLine`s](config/waypoints/lerpable-lines.md) is not as user-friendly and self-correcting as it can be
