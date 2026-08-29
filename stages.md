# Stages

A Stage holds the content of a [Session](sessions.md). In the mature workflow, it is the unit that users save when closing a Session, load when starting one, edit, and perform entirely within Cinebara.

!!!warning
The `Stage` container and its root node exist in the current state of the engine. Complete stage persistence and full in-world editing do not. The current serializer writes a tree to data in one direction. It is not yet a complete save and load system.
!!!

A Stage always has at least one [Node](nodes.md) in it which serves as the root of the Stage's [tree](nodes.md#trees).

# Scenes

!!!warning
Scenes are not yet implemented
!!!

A scene is some configuration of a stage. Elements can be added that themselves are not a part of the stage and changes can be made to the stage that are non-destructive All changes, such as deleting nodes, repositioning a prop, or changing the time of day, can be reverted. Changes made to the original stage are not immediately merged into scenes.

!!!question
Should scenes be like branches of the stage? As in, source control... Scenes could derive other scenes. Infact, a stage should maybe be branchable in general. This concept could be extended to entities, quite like Unity's prefab variants. I think it should. - Kufi
!!!

# Snapshots

!!!warning
Snapshots are not yet implemented
!!!

A snapshot allows a scene to be saved up to a certain point such that the performance after that point can be recaptured for alternative takes. Like splitting timelines!
