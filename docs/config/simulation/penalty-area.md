# PenaltyArea

`PenaltyArea`s are areas that can be used to discourage queue formation and agent pathfinding within a specific area.  Any pathfinding nodes that are contained with the bounds of a `PenaltyArea` are given a penalty upon first starting the simulation.

When agents attempt to pathfind from one point to another, they will always choose the cheapest path possible.  By adding penalties to certain nodes, we can discourage agents from moving across these nodes, as they are considered more expensive to them.

## How to Create

To create a `PenaltyArea`, simply create a new GameObject with a `BoxCollider` on it, and add the `PenaltyArea` component to it.

For an even easier way, simply duplicate an existing `PenaltyArea` (which can be found in the hierarchy as GameObjects containing the name "PenaltyArea") and move it to your desired location.  `PenaltyArea`s can also be scaled via the scale vector of their `Transform` component.

## Tips

- Always ensure the bounds of the `PenaltyArea`'s collider is hitting the ground, so the penalties can correctly be added to the pathfinding nodes
- The more red the nodes appear on the pathfinding grid, the more penalty they have.  Node colors are viewable after the simulation is started
- Use the `Avoidance Strength` slider on the `PenaltyArea` component to control how much of a penalty is applied to an area
