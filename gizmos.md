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

Clicking on a Node wth a "surface" will select it. If there are multiple Nodes intersecting the ray you clicked, clicking again will progressively increment through the intersected Nodes. Clicking and dragging will select all Nodes that intersect the drawn box that are also deemed "visible". This visibility check can be disabled. In VR, the visibility check is not done as you are drawing a 3D box and so such a concept doesn't mean anything.

Holding [Shift] and clicking an unselected Node will expand your selection to contain the new Node. If you clicked a Node which was already selected, it will remove the Node from your selection instead. The same [Shift] modification can be applied to the box selection, but it will always expand your selection. Holding [Ctrl] + [Shift] will deselect.

## Translate

!!!warning
Translation is not yet implemented.
!!!

!!!
Alignment tools & mirror / symmetry tools
!!!

!!! Snapping
Grid
Vertex
Edge
Face / Surface

Orient to surface
!!!