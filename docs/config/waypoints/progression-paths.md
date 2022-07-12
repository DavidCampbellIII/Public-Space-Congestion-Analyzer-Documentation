# Progression Paths

![ProgressionPath Component](../../img/progressionPath.png)

## How to Locate

The `ProgressionPath` component is located on the same GameObject as any [`WaypointLocation`](waypoint-locations.md) that has `Has Progression Path` set to `true`.

If a `ProgressionPath` component is not there, it needs to be added manually.

## Settings

Setting | Description
:-------- | :------------------------------------------------------------------------------------------------------------------------------------
Min Perc To<br/>End Location | Min percent of the progression path an agent must always travel before <br/> breaking out of the progression path.
Draw Progression <br/>Path | Toggles whether or not the progression path visual should appear.
Progression <br/>Path Break Out<br/>Region Width | *Only applicable if `Draw Progression Path` is `true`.*<br/>Width of the visual for the break out region of the progression path.
Break Out<br/>Region Color | *Only applicable if `Draw Progression Path` is `true`.*<br/>Color of the visual for the break out region of the progression path.

## Tips

- `ProgressionPaths` must also have a [`LerpableLine`](lerpable-lines.md) component attached to the same GameObject as they are.  If it is not there, it must be added manually.
