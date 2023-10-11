# Mobile Production Challenges

The biggest challenge with mobile wallets is: **agent distribution**. 
- Dealing with app store release policies (getting your app through the gates of Apple and Google)
- Getting users to upgrade to the latest version to drop support for deprecated features.

Normal web services like a website often have simply one deployment, and you control the version yourself. Mobile
apps could run on millions of devices, and getting all of them to upgrade is an unsurmountable task.

## Community upgrade process

For Aries this problem can be even more significant, because these wallets also need to integrate with a range
of other agents. Agents need to align AIP versions and need to be tested for interoperability. When the community
agrees that a certain update really needs to happen, the upgrade mechanism 
[RFC 0345](https://github.com/hyperledger/aries-rfcs/tree/main/concepts/0345-community-coordinated-update) 
can be used.

## Deploying a Mediator (or not)

Besides deploying a mobile wallet to the app store, each mobile wallet will need a mediator that connects it and 
receives messages for it at its endpoint. Beyond that minimum of routing messages, it's up to the mobile wallet
provider to decide what else you want your mediator to do.

### Third party mediator

With the coming of mediation protocols, a simple solution for using a mediator is using a third party mediator.
This is a mediator that is managed by someone else. Anyone can set up a mediator that uses those mediation protocols,
to serve as a mobile wallet mediator that support those protocols.

One example of a public mediator is this: [Indicio Mediator](https://indicio-tech.github.io/mediator/)

### Aries Mediator Service

Another possibility is deploying an instance of the [Aries Mediator Service](https://github.com/hyperledger/aries-mediator-service).
A mediator service ready to deploy in your own environment. Under the hood it's just Aries Cloudagent Python with
some configuration settings for it to act as a mediator. You can deploy an instance as is, or add more features
depending on the needs of your mobile wallets (or other applications that might use the mediator).

###  Write your own

Another option is to write your own mediator agent. Using an Aries framework as a base might not be that usefull,
since a mediator doesn't do a lot of "agent-like" things. It makes more sense to make your own component.