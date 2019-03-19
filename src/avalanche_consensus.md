# Avalanche Consensus Algorithm (WIP)

Avalanche is a new family of consensus protocols inspired by gossip algorithms. The protocol is based 
on random sampling and meta-stable decision, and provide a strong probabilistic safety guarantee.

This protocol family achieves its properties by humbly cheating in three different ways:

1. Adopting a safety guarantee that is probabilistic.
2. Establishing only partial order between dependent transactions.
3. No liveliness guarantee for misbehaving clients.

## Guarantees

Avalanche protocol provides the following guarantees with high probability:
- **Safety:** No two correct nodes will accept conflicting transactions.
- **Liveliness:** Any transaction issued by a correct client will eventually be accepted by every correct
node.

## Assumptions

Avalanche protocol makes following assumptions:
- A synchronous network.
- All members of a network are not known to all participants.
- A safe bootstrapping system that enables a node to connect with sufficiently many correct nodes.

## Approach
