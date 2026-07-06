# Nodes

A Node is a thing which may have other Nodes as children. A Node's parent is the singular Node that it is a child of. A Node can not have more than one parent, but it might have no parent at all.

A Node with no parent is considered the root of its tree. A tree is all Nodes descendant of a root Node and the root itself. A Node's relationships (its parent & children) are always transparent, as in, they are always readable.

There are many types of Nodes, all of which have their own specific purpose. As a general rule, a Node should have at most one purpose.

A few example nodes:

=== Node
The simplest type of Node. It has no special behaviour.
===

=== Camera
Draws the scene from the perspective of the Node.
===

=== Node3D
Translates this node and all of its descendants by the specified offset position, rotation, and scale.
The transformations defined in the node are accumulated onto the transformations defined in any parent Node3Ds.
===

# Sessions

A session can contain many trees that serve different purposes. 
One specific tree that the session holds is the Stage, which is the primary tree you interact with.

Any node created for a session is remembered so that when the session closes, all of its resources can be cleaned up. This means that if a node ever falls into Limbo, it is still remembered by the session.

# Stages

A Stage holds the content of the session and is also the thing you conceptually save (when closing a session) and load (when starting a session).
One Node serves as the root of a Stage.

# Limbo

A node that is not inside of a session's trees is considered to be in "Limbo". A node may be intentionally placed in Limbo to temporarily hide it and potentially bring it back. This concept is used for Entities, where disconnecting the tree of an entity and the stage is an important concept for protecting the content of the entity.

# Entities

An entity is some separate tree that does not exist in a Stage's tree but is referenced by some node within the Stage's tree. The node that sits in the Stage is called an Entity Instance and exposes a dynamic set of configurable properties that allow data to be shared between the Stage and the Entity.

Events like ticks or inputs being received by an Entity Instance are propagated to their referenced Entity root.

# Ghosts

A ghost is a tree in a session that represents a user connected to that session. A user acting via a ghost can interact with the Stage with limited access.

# Process order

Events like "Actions" and "Ticks" need to be distributed to the nodes of a session. This is done one tree at a time, and for each tree you broadcast depth first.

```
function broadcast_to(node, event_to_run)
    for each child of node
        broadcast_to(child)
    event_to_run.execute
```

This can also be thought of as "ascending the tree", though this phrase can be confusing as trees are usually depicted upside-down. You ascend from the root to the leaf nodes, but you descend down the tree as depicted in a GUI.

First, all ghost trees are processed in order of session age descending. Older ghosts are processed first. Then the stage is processed.

Some events may bypass certain trees for security or sensibility reasons. For example, your personal inputs are sent to your personal ghost and then to the stage. They are never propagated to other user's ghosts.

# Input handling

Raw inputs are transformed into Actions via a series of Action Generators. An Action Generator can be though of as a keybind, something that turns a raw input concept (Like pressing the W key) into an Action with a purpose (Like "move forward").

At the start of a frame, raw inputs are turned into a list of actions. The actions are processed through the session following the process order defined above. Nodes can then listen for a certain Action and read it before optionally consuming it (implying other nodes should not use it again).

Some nodes may intend to use inputs from a specific user while ignoring inputs from other users. For this, Actions have an owner which can be used as a filter by Nodes.
