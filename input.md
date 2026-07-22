# Input

Raw inputs are transformed into Actions via a series of Action Generators. An Action Generator can be though of as a keybind, something that turns a raw input concept (Like pressing the W key) into an Action with a purpose (Like "move forward").

At the start of a tick, raw inputs are turned into a list of actions. The actions are processed through the session following the process order defined above. Nodes can then listen for a certain Action and read it before optionally consuming it (implying other nodes should not use it again).

# Ownership
!!!warning
Action ownership is not yet implemented
!!!

Some nodes may intend to use inputs from a specific user while ignoring inputs from other users. For this, Actions have an owner which can be used as a filter by Nodes.

## Input sources
The same action may be provided by different sources. Think of a laser in VR and a mouse cursor both sending out "click" events. Different sources may be owned by the same device, like the left hand laser and the right hand laser.

These sources are provided to actions in the form of a list. The list is composed of all sources that contributed to the generation of an action.

## Action consumption
Consuming an action marks all of the used inputs as being used and no further actions should be accessible that also use those actions. Some raw inputs may want to be used by multiple actions in the same tick, such as holding a modifier key like ctrl to alter the behaviour of movement keys.

!!!question
How do we differentiate between actions that can be shared and those that can not?
!!!