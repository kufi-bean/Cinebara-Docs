# Gizmos

A gizmo is an interactable overlay used while editing a [Stage](stages.md). There are many types and they serve as a more convenient way to edit node properties.

Gizmos are drawn after everything else in the Stage, and even after post processing to avoid the controls being hidden by effects. Gizmo inputs are handled before anything else in the Stage but are rendered after everything else in the Stage. This gives Gizmos input and render priority.

Technically, while in edit mode, Gizmos are always running regardless of if Nodes are being modified or not. As long as a Gizmo has been created by some context switch or mode, it is available to use by any number of tools. This is handy as binding a Gizmo to a specific tool's enable/disable state would mean selecting in select mode and then switching to transform mode would remove the Gizmos, when in reality the User probably intended to move the selected Nodes.

Some Gizmos depend on data provided by other Gizmos. The Translate Gizmo operates on Transform3D Nodes that are ancestors of the selected nodes provided by the Select Gizmo. In Translate mode, you may click on a Node which adds it to the Select Gizmo's targets which the Translate Gizmo can then use. This is just a convenience feature that makes Selection feel more universal.

!!!question
If I select a mesh renderer and want to move it around, how is that handled? A mesh renderer has no transform as that is given by a transform node. A transform node has no selectable bounds, though, so how do you select it without using the hierarchy?
!!!

!!!question
Are Gizmos Nodes? 
If so, can a user create them in a Stage?
If not, what are they?

If they were nodes, it would open up the opportunity for custom gizmos and custom tools made by users via scripting. It would make the process of creating custom gizmos quite familiar to those already initiated with the Node based workflow.
!!!

!!!question
Does selecting a Node show the bounds of all of the children? What about a shared bounds? Local, or globally oriented? Do we show icons for the nodes? Might get busy...
!!!

## Select

!!!warning
Selection is not fully implemented.
!!!

Clicking sends a linecast from the active camera into the Stage. The linecast tests queryable nodes (currently only MeshRenderer). When it intersects more than one eligible node, the closest intersection becomes the selected target.

A normal click replaces the existing selection with that target. A normal click that does not hit eligible geometry clears the existing selection. Holding either [Shift] or [Ctrl] changes the click into a toggle. Clicking an unselected target adds it to the selection, while clicking a selected target removes it. Holding [Shift] or [Ctrl] while clicking empty space leaves the selection unchanged.

### Intended selection workflow

The selection tools are intended to support cycling through overlapping targets, drag or box selection, and optional visibility filtering for box selection. VR selection is intended to use a three-dimensional selection box, where screen-space visibility does not apply. These behaviors are not implemented. There is also no distinct Ctrl+Shift deselection mode yet.

## Translate

Allows translating selected `Transform3DNode` targets. If a selected node has no transform of its own, the gizmo can instead translate its transform ancestor.

The gizmo shows 3 interactable axes to drag, but you may also move objects relative to the viewplane by pressing `G`. Pressing `G` and then an axis (X, Y, or Z keys) will constrain translation to that axis. Holding shift when pressing an axis will constrain the transformation to the other 2 axis, allowing you to slide the node on a plane instead.

The axis point along world +X, +Y, and +Z by default but local coordinates may also be used.

!!!warning  Not implemented
The final editing workflow is intended to add snapping to grids, vertices, edges, and faces, together with alignment, mirror or symmetry tools, and surface orientation.
!!!

## Rotate

Allows rotating selected `Transform3DNode` targets. If a selected node has no transform of its own, the gizmo can instead rotate its an ancestor.

The gizmo shows 3 interactable rings to grab and drag, but you may also rotate nodes relative to the viewplane by pressing `R`. Pressing `R` and then an axis (X, Y, or Z keys) will constrain rotation to that axis.

The rings are oriented to face world +X, +Y, and +Z by default but local coordinates may also be used.