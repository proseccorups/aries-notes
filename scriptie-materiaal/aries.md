# Hyperledger Aries

## Why Aries?
Aries is a project that solves a number of challenges that arise when creating a fully functional SSI ecosystem. Such a
system require a network of agents that interact with other agents and a ledger. Those agents are operated by either individuals
or organizations and are built using open source technology, commercial tools or proprietary built solutions. To make all of this
work together seamlessly is quite the challenge. How do they reach each other, how do they exchange credentials, how do they interact
when having different origins? Hyperledger Aries is the project built to solve all these problems. 

Aries is built with collaboration in mind. Aries allows those who want to set up an SSI architecture to define common protocols
that will be used, common agent architecture and tests to ensure that the agents are able to work together properly. As mentioned previously,
Aries originated from Hyperledger Indy and AnonCreds, though it still supports said technologies, it can also be used with different ledgers
and credential formats. 

## Protocols
There are various degrees of complexity at which interaction can happen between Aries agents. The simples exchange is just 
sending and receiving messages. One agent sends some data and the other agent understands and processes it. Adding some complexity
will bring you to a sequence of messages that happen in a set order. Both the single message and the sequence of messages are protocols.
A protocol is simply the set of rules or procedures for how interactions between agents should happen, making sure that the 
interaction is secure, reliable and every involved party understands how interactions should happen.
As protocols are used by many involved parties, one person can not just implement and use a new protocol. They need to be 
carefully specified, implemented and tested by multiple stakeholders to eventually be accepted as the new norm. The various 
protocols and in use right now can be found in the Aries RFC repository (link in sources).

One example of a protocol used in the context of Aries is issuing a credential. The process always starts with an offer from
the issuer to the holder. The holder will confirm this offer by sending a request for the credential and the protocol ends
with the issuer issuing the credential itself.
Another example is the DIDComm protocol that is involved with most Aries interactions. DIDComm uses DIDs and its involved data to 
enable peer to peer messaging that is private and secure.

## Making interactions secure with DIDComm