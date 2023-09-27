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


https://learn.microsoft.com/en-us/events/gophercon-2021/using-crdts-to-build-a-highly-available-decentralized-service-with-eventual-consistency-in-go



Gossip protocol:
Ways to broadcast mesasge
1. Eager reliable broadcast:
   1. everyone broadcast all the messages they recieve
   2. but the problem with the approach is that its expensive
   3. order of messages is m^2  messages
2. Optimisation for this is called gossip protocol
   1. when  a message is recieved by a node it will forward to 3 or X more nodes at random.
   2. when the message goes to a node which have already broadcasted it will ignore it - eventually it reaches all nodes

Ordering in gossip protocol:
if we want to ensure fifo broadcast(all of the messages by same sender are recieved in the right order):

1. each node maintains 3 variables
   1. seqNumber -> number showing the messages that is sent by the current node
   2. delivered -> [int] -> how many messages by each particular sender we have delivered
   3. buffer - queue of messsges and then delivered
2. On request to broad cast message m for node n1
   1. for all i:
      1. send(i,seqNumber, m)
      2. seqNumber + 1 
3. On request to recieve:
   1. add to buffer
   2. look at buffer
   3. check the message is the next message.
   4. if the message is not in sequence put it back to buffer

if we want to ensure causal broadcast(all of the messages by same sender are recieved in the right order):

1. each node maintains 4 variables
    1. seqNumber -> number showing the messages that is sent by the current node
    2. delivered -> [int] -> how many messages by each particular sender we have delivered
    3. buffer - queue of messsges and then delivered
   4. dep = [int] -> when a node sends a messsage it will increment its dependency 
2. On request to broad cast message m for node n1
    1. for all i:
       2. dep[i] = seqnumber 
       1. send(i,dep, m)
       2. seqNumber + 1
3. On request to recieve: (TODO)
    1. add to buffer
    2. look at buffer
    3. check the message is the next message.
    4. if the message is not in sequence put it back to buffer


Total order broadcast is hard:
1. one way is for a leader to be present which will sequence the message and the leader will be doing the fifo broad cast
2. other opton s