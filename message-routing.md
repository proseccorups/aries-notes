# Message Routing in Hyperledger Aries

## What is message routing?

### Why routing?
Based on the knowledge I've gathered so far, it's easy to form a mental image of how messages are 
being passes around between Hyperledger Aries agents. While messaging agents appear to be connected
directly. They ofter are **not**. Mediator and Relay agents are often necessary for messages to be
securely delivered.

The reasons for this are as follows:
- Mobile wallets do not have an endpoint. So other agents can not *directly* send messages to them.
- Entities might want to minimize correlation of their messages, so instead of having a unique endpoint, many agents
  might share the same endpoint. This way their messages are *hidden in the crowd.*
- Entities might not want inbound and outbound messages to be correlated. Therefore they might use different pahts for the two.
- An enterprise might want to have a gateway agent which is responsible for talking to the *big bad internet*. The other agents
  from that organisation will just talk to the gateway.

Only the *first* option in the list above is an actual requirement/fact. The rest are options available to the entities managing agents.

![img.png](assets/images/multiple-mediators-example.png)

### Intermediaries/mediators
In the above example the Faber agent might decide to always send messages trough agent 2. Alice might
instruct other agents that they always want their messages to be sent trough agents 3 and 4. So in the end you
would need 5 agents in total to send a message from one agent to the other.

### Privacy
Faber and Alice probably want to keep their data private and will therefore encrypt the messages, with
only just enough information available for the intermediaries to know how to get the message to its destination.

### An analogy
You could imagine the routing agents as a sort of postal service. They get the message wrapped in multiple letters (encryption)
which are then sent to the receiver without them knowing the contents.

## DIDComm Mediators and Relays

### Mediator
In DIDComm, the **mediator** is an agent that the receiver has instructed the sender to use when sending them a message.
For each mediator that is being added to the *path*, another layer of encryption is added. Alice will
have a *list of agents*, that is actually just a **list of encryption keys** for Faber to use.

### Relay
In DIDComm, the term **relay** means that the message is being routed trough one or multiple agents, without knowledge of the sender.
Important difference with Mediators, is that the sender *must* know about those and explicitly add an extra *envelope* of encryption,
whereas for relays, they don't care. An analogy for a relay might be an assistant distributing letters in an organisation that have already been received securely.

### Mediators and Relays are agents too!
An important takeaway here is that both Mediators and Relays are agents of their own with all the functionalities that come with it.
It's just that their activities are different. They have a peer-to-peer relationship with the agents with which they communicate, and 
they use that channel to do **routing** on their behalf.

[Here you can see the RFC and more details on mediators and relays](https://github.com/hyperledger/aries-rfcs/blob/main/concepts/0046-mediators-and-relays/README.md)

## Encryption Handling
DIDComm encryption is performed within the Aries frameworks, and not something a developer building applications
that use an agent has to worry about. Within an Aries agent, there are libraries present responsible for encryption. And there is a big chance
that they eventually call some dependencies from **Hyperledger Ursa**.

To encrypt a message. The sender agent code will call something like a ```pack()``` function to encrypt a message. And to decrypt a message,
the code of the receiving agent will call something like an ```unpack()``` function.

The *encryption envelopes* described in the following RFC's 
([RFC 0019](https://github.com/hyperledger/aries-rfcs/blob/main/features/0019-encryption-envelope/README.md) for AIP 1.0) 
([RFC 0587](https://github.com/hyperledger/aries-rfcs/tree/main/features/0587-encryption-envelope-v2) for AIP 2.0)
define the different variations for sender authenticated and anonymous encryption. 

### Authenticated messages
Both the keys for the sender and the recipient are used for encryption. The recipient will know exactly who sent a message.

### Anonymous encryption
With **anonymous encryption**, the sender will only use the public key of the recipient for encryption. Anyone who knows that key can send a message.

In DIDComm, the general way to go would be **Authenticated** messages, and it's generally used for all messaging that involves a sender and recipient.
**Anonymous encryption** is often used for messages to and from **Mediators** and **Relays**

## Mediators, Relays and Privacy

It should be obvious that when sending messages trough other agents, some privacy aspects need to be taken into consideration. It's tempting 
so keep sending and handling messages as simple as possible, but for privacy reasons that might no be a very good idea. Below you'll find some notes on how **DIDComm** can **mitigate** privacy risks

### Recording Metadata
Even tho mediators and relays can not see the contents of the messages they are routing. They do know a lot of other information, such as:
- The fact that the message was sent.
- From where it was received.
- How big it is.
- When it was sent.
- Where it will go next.

Collecting all this **metadata** could eventually still be a breach of privacy. The contents remain private, but it's still possible to collect information about the
senders' and receivers' social and business relationships. It could be compared to Google knowing about your interests by tracking logins to websites, while not 
knowing about the details of your interactions with the website.

### DIDComm addressing privacy concerns
With DIDComm, one of the goals was to address this concern of too much metadata being exposed to intermediaries.
Encrypting every wrapper and minimal inclusion of information in the *envelope*, limits what metadata can be gathered.
Using multiple hops in the sequence of getting a message across. Could also help preventing the intermediaries from knowing what the earlier and later steps are.

If you take the earlier picture as an example, let's consider what privacy and security risks exist.

- Every agent in the flow could try to decrypt inner messages which they are not supposed to access. With proper encryption this would fail.
- Agent 2 (The one trough which faber sends outbound messages), can see the physical messages going to agent 3.
- As long as other agents are also using agent 3 as an endpoint, agent 2 doesn't know who the end recipient is. (This concept is called
  **lost in the crowd**, many messages are received at common endpoints and senders don't learn anything about the final destination)
- Agent 3 can see the physical address of where the message came from (agent 2), but can't see where agent 2 got it from. As long as not only Faber messages go trough
  Agent 2, it can't know it came from Faber.
- Since agent 3 routes messages trough agent 4, agent 3 does not know Faber's message is for Alice.
- Agent 4 is aware of every time Alice receives a message.
- Agent 4 does not know from whom the messages were received, since they all go trough the agent 3. Since Agent 4 is only used for Alice's inbound messages,
  it doesn't know anything about Alice's outbound messages.
- For mobile wallets, data sent between mediator and mobile wallet flows trough the Internet Service Provider. The ISP can know where all the messages
  are flowing, but can not decrypt their contents.
- The recipient can ofcourse see all the plaintext data from the message, because they need to display it to an end user or something along the lines of that.
  This needs to be taken into consideration for security as well. Can you trust the recipient to not share the data with non-trusted parties.
