## ELECTION VOTER
1. This is just a distributed counter impl for voting.
2. There are multiple clients who can cast a vote and each local system will store the state of the vote which will eventually converge
3. There will be multiple impl of different ways to do this
Concepts to learn:

4. single client based model storing all states
1. crdt
2. implementing gossip protocol at a network layer
3. implementing a gset or admin based 2p et (IYKWIM for voting) 

Propogate the downfall of all client states to group based states and 
1. crdt
2. implementing gossip protocol at a network layer
3. implementing a gset or admin based 2p et (IYKWIM for voting)



understanding blogs readhttps://www.youtube.com/watch?v=77qpCahU3fo&ab_channel=MartinKleppmann
https://learn.microsoft.com/en-us/events/gophercon-2021/using-crdts-to-build-a-highly-available-decentralized-service-with-eventual-consistency-in-go

