# Networking

The structure of a networked stage hierarchy is implicitly replicated between peers. Properties on Nodes within the
hierarchy are implcitly replicated during editing but explicitly replicated during play mode. They must be intentionally
set up for networking or be backed by networked.

When replicating data, one user acts as an authority for the NetworkID. They do NOT own the data, they just help agree
upon a unique ID.

## The master

The master relays all reliable packets to all other users. They also decide on newly connecting users IDs.

## NetworkIDs

Anything that must be uniquely identified over the network uses a NetworkId, a polymorphic identifier type. An id may refer to a Node or a ValueInterface, both of which are owned by a stage in some way.

A Network Id may then be used to find properties, since properties live directly on Nodes or ValueInterfaces. Identifying a property is done using the NetworkId of the thing holding the property followed by the property's string identifier.

NetworkIDs are the preferred way of referencing a Node, but it is not the only way. When a user first creates a Node,
and it is replicated to the master, the node lacks an agreed upon NetworkID. For this reason it is given a temporary ID
that is composed of the User's ID and a NetworkID as decided by the author of the Node. This is more data but avoids
collisions when multiple users associate the same ID to different Nodes without knowing.

Both IDs are associated to any node created locally or that was replicated to the master.

Sending ordered data to peers for a newly created object follows this protocol:
There are 3 connected peers; Alice, Bob, and Marc who is also the "master"

1. Alice creates Banana and associates a temporary ID "AliceBanana".
2. Alice tells Marc about Banana.
3. Marc associates a new, more compact, known-to-be-unique ID "Banan".
4. Marc tells Alice about the new id.
5. Marc tells Bob about the creation event, already associating it only with the new NetworkId.
6. All peers now exchange changes to Banana using the compact "Banan" id.

**Considerations**

> **Conflicting changes**
>
> The master chooses the most recent change based on latency adjusted ticks and informs the resolved value to the peer
> who had lost the conflict battle.
