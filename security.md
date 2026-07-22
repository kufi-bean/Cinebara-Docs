---
description: Promises, contracts, and disclaimers that curious users may be interested to know about.
---

# Security

While Cinebara has no need for security features right now, in anticipation of a day where it becomes more widespread and people can freely move between [Sessions](sessions.md), considerations are made for what someone (potentially a bad actor) may have access to.

This concerns span from internal management of refences that could be exploited through the in-world editing system, to the in-world permission system itself, where a session host may have authority over what other users may do.

---

# Promises

Before we get to the real security stuff, let's lay out some promises. A "promise" is more of a conceptual thing, It's a pinky promise that we will try our hardest to maintain. Most of these are less technical and more user-facing.

### Sources will be readable

The plan for how Cinebara will be open-sourced is under discussion, but so far everyone agrees that the source should be public facing.

### Modders are allowed to mod

We can not account for absolutely everyone's use case. Custom clients are expected regardless of if we "allow" them. Pushing the VR film industry forward is the goal of Cinebara and choking innovation by disallowing mods would be counter to that goal.

---

# Contracts

A "Contract" is an absolute rule arbitrarily defined for Cinebara's operational safety. They are in place to avoid security footguns or to improve general usability and stability. Typically, a contract has the goal of limiting access to something but some contracts may specifically aim to permit access as to avoid ambiguity.

### Transparent Relationships {#transparent-relationships}
Requesting a Node's children or parent must report an accurate result for the request. Never should a Node pretend it has no Children, or hide its Parent.

Such responses could result in a Node's intentions becoming unclear. If a Node intends to send an event to all of its children then the User should be sure that it does that. This concept extends to parents.

The consequence of this is that an entire Tree is readable if you have a reference to just one Node in that Tree.

### Hidden Ghosts {#hidden-ghost}
Nodes that are a part of a [Ghost's](nodes/nodes.md#ghosts) tree must not be discoverable by any other tree.

Modification of a Ghost could be a malicious attack vector. A Ghost must be a safe object for the User and so a User must remain completely in control of it.

*Personal Characters may also be in this Tree, but this is under discussion.*

### Undiscoverable Trees {#undiscoverable-trees}
A tree must never be discoverable from nothing. 

You can reference foreign trees as long as the foreign tree was either in the same tree at some point before, or a daisy chain of references lead to it. This is important to keep Ghosts from being discovered from nothing which would violate [Hidden Ghosts](#hidden-ghosts)

---

# Disclaimers

Finally, a "Disclaimer" is everything we would like to promise, but realistically can't. All of these are things we will try to avoid but if the result is a benefit for Cinebara then we may well do it.

### Breaking Changes

Cinebara's primary goal is to push the industry forward. The best way to afford that is to be flexible with development. We're a small team and our reasoning is not perfect. If it turns out that changing something would benefit the engine as a whole, it is likely we will make that change.

*Note: We will try to write upgrade mechanisms to smooth out these situations, but matching behaviour is not guaranteed.*

### Engine Instability

Especially during the early development, you can expect crashes and unexpected behaviour. We encourage you to communicate your struggles to us and we can promise to work towards a more stable future, but for now... make frequent backups.

---

# Roles

!!!warning
The permission system & roles are not yet implemented
!!!

As with most permission systems, users are given roles that afford them abilities.

---

# Open Concerns

!!!question Modified Clients
If a user has a modified client, how can we protect other users from having their input events scrubbed?

Can we protect users from having their assets stolen easily this way? Encryption of some kind? I find it unlikely.
Maybe we can protect against the same content being uploaded twice? Not if the assets are decentralized, though.

I believe it is fine to allow modified clients in some cases but not others. If a User knows all of the people they will be interacting with, then trying to protect them might be a bit of an overstep. Some Sessions could be made to allow modified clients, while others, perhaps the public sessions, do not?

How do you even check for a modified client? A checksum can just be spoofed. 

Perhaps you can only connect to Sessions if you have an account and we use moderation. A user who mods for convenience should not be punished as though they were malicious. But you can't really detect if malicious activity is happening.
!!!

!!!question Licensed Assets
How should we hide access to licensed assets? If a user imports something they own, can we protect it? I think the answer is no, generally, but we can make it inconvenient. And from the perspective of a "good" actor, the ability to save the item to a known location on disc should not be present. Maybe the locally cached version should be encrypted or obfuscated, even.

I believe we fundamentally can not protect someone's assets, no matter what. No app can.
!!!