# Entities

!!!warning
The entity system described on this page is planned and not implemented. There are currently no `Entity` or `EntityInstance` types.
!!!

An entity is some separate tree that does not exist in a Stage's tree but is referenced by some node within the Stage's tree. The node that sits in the Stage is called an Entity Instance and exposes a dynamic set of configurable properties that allow data to be shared between the Stage and the Entity.

Events like ticks or inputs being received by an Entity Instance are propagated to their referenced Entity root.
