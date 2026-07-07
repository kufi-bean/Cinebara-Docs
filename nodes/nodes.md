---
order: 100
expanded: false
---
# Nodes

A Node is a thing which may have other Nodes as children. A Node's parent is the singular Node that it is a child of. A Node can not have more than one parent, but it may have no parent at all.

# Trees {#trees}
A Node with no parent is considered the root of its tree. A tree is all Nodes descendant of a root Node and the root itself. A Node's relationships (its parent & children) are always transparent, as in, they are always readable.

There are many types of Nodes, all of which have their own specific purpose. As a general rule, a Node should have at most one purpose.

# Ghosts

A ghost is a tree in a session that represents a user connected to that session. A user acting via a ghost can interact with the Session's Stage with limited access (Just enough to "escape" limbo).

# Limbo

A node that is not inside of the Stage tree is considered to be in "Limbo". A Node may be intentionally placed in Limbo to temporarily hide it and potentially bring it back. This concept is used for Entities, where disconnecting the tree of an entity and the stage is an important concept for protecting the content of the entity.

# Process order

Events like "Actions" and "Ticks" need to be distributed to the nodes of a session. This is done one tree at a time, and for each tree you broadcast depth first.

```
function broadcast_to(node, event_to_run)
    for each child of node
        broadcast_to(child)
    event_to_run.execute
```

This can also be thought of as "ascending the tree", though this phrase can be confusing as trees are usually depicted upside-down. You ascend from the root to the leaf nodes, but you descend down the tree as depicted in a GUI.

Processing happens in this order:

1. The Cinebara UI
2. All ghosts in the loaded session (oldest first)
3. The loaded session's stage tree

{{ for page in content.categories["nodes"].pages ~}}
[!card layout="signal"]({{ page.path }})
{{ end }}