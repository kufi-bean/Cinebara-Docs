# Sessions

!!!warning
The Session abstraction and its lifetime, master, replication, and election model are planned and not implemented. The current state of the engine keeps the main and UI stages on the `Cinebara` singleton and stores Ghosts on `Stage`.
!!!

A session holds a loaded instance of a [Stage](stages.md) and may be networked. Fundamentally, a session exists to provide access to a Stage.

A session can contain many trees that serve different purposes. 
One specific tree that the session holds is the Stage, which is the primary tree you interact with.

!!!warning 
Networking is not yet implemented
!!!

# The Master
The master of a session is the user that serves as the source of truth for network events and replication order. All reliable packets are sent through the master and redistributed to other users. 

Users may establish direct connections with eachother for unreliable data streams. This is useful for decreasing latency as much as possible to make acting with someone more natural/realtime.

In the event that the master is lost, perhaps due to a crash, a user is chosen to assume the role of master.

---

!!!question
- How do you create a session?
- Can a session host multiple stages?
- Is this where Entities are collaboratively edited?
- How do we choose a new master when the old one is lost?
!!!
