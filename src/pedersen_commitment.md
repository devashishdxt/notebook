# Pedersen Commitment

A **commitment scheme** is a cryptographic primitive that allows one to commit to a chosen value (or chosen statement) 
while keeping it hidden to others, with the ability to reveal the committed value later. Commitment schemes are designed
so that a party cannot change the value or statement after they have committed to it: that is, commitment schemes are 
_binding_.

Interactions in a commitment scheme take place in two phases:

1. _Commit phase_ during which a value is chosen and specified.
1. _Reveal phase_ during which the value is revealed and checked.
