# Aries Protocol Notes

## Aries Protocol Messages

- **@id** is a unique identifier for the message, generated from a globally unique ID (GUID) library.
- **@type **is the type of the message. It is made up of the following parts:
  - **namespace**: *https://didcomm.org* is the place where protocols are defined by the Aries Working Group
  - **protocol:** The name of the protocol to which the message type belongs
  - **version:** the version of the message defined with the semver versioning system
  - **type:** The actual name of the message
- **sent_time**: When the message was sent, as defined by the sender
- **content**: The text of the message!

## Message Decorators

- Message decorators are standardized message elements that define cross-cutting behaviour.
- They are cross-cutting, which means that the bevaviour of that element is the same when used in different protocols
- the ~l10n decorator in the message below is an example. It is used to provide information to enable localization of the message.
- Decorators all have their own RFC's (Request For Comment). In this case, the localization decorator is specified in **RFC 0043**
- Most common decorator is **~thread** (RFC 0008) which is used to link messages in a protocol instance
- As messages go back and forth between agents to complete an instance of a protocol (for example, issuing a credential), **~thread** decorator data lets the agents know to which protocol instance the message belongs and the ordering of the message in the overall flow.
- The ** first** message of a protocol instance will not have a **~thread** decorator. When a recipient responds to the message, the **@ID** of the first message is taken and made the **thid** (thread ID) of the **~thread** decorator

## Special Message Types: Ack and Problem Report

two message types that deserve special attention:

- ack (acknowledge): Explains how one party can send acknowledgement messages to confirm receipt and clarify the status of complex processes. ([RFC 0015](https://github.com/hyperledger/aries-rfcs/tree/main/features/0015-acks))
- problem_report: Describes how to report errors and warnings in a powerfull, interoperable way. All implementations of SSi agent or hub technology SHOULD implement this RFC. ([RFC 0035](https://github.com/hyperledger/aries-rfcs/tree/main/features/0035-report-problem))

When a protocol **'adopts'** these messages, it means that there is a message type of **ack and/or problem_report** in the protocol, even though there is not a formal definition of the message type in the specification.

**DIDComm** messages are asynchronous. A use case for problem_report in that regard could be: If an agent sends a message, and it doesn't get a response within a timeframe it deems appropriate, it can send a **problem_report** asking if the message was received.

## Protocols and Messages: The Controller's Perspective

As an aries developer, it's important to know what protocols do and how to use them when coding, but you don't have to know all 
the nitty gritty details. Each aries framework exposes a way to use the protocols that minimize what the controller has to do.

Instead of constructing a complext message yourself, what the controller does is call an endpoint 
like:/didexchange/{conn_id}/accept-invitation using the ID of the connection. A framework like ACA-py takes care of the rest.

## Aries Protocols: Receiving a Response

Let's say Alice sends a request for a credential about her degree at Faber college. The agent framework processes the message as follows:

- **Agent Framework Code:** Uses the **~thread** information to find the message's corresponding protocol state object and retrieves it from storage. Could be the state object
  of the initial message that was sent between the two agents.
- **Agent Framework Code:** Processes other **generic decorators**, ones not meant to be processed by the message type handler, such as: '~tracing'
- **Agent Framework Code:** Hands the message and the protocol state object to the appropriate **message type handler**. In this case, the credential request handler 
  that is part of the issue credential protocol is invoked
- **Message Type Handler:** processes the message, updates the **protocol state object** appropriately and sends an HTTP request to the controller 
  (**webhook**) to provide info to the **protocol state object**.
- **Controller:** receives the information via the event **webhook**.
- **The agent framework code**: Doesn't know how long it will take for the controller to respond, so it persists the protocol state object and does other 
  things in the meantime.
- **Controller:** Uses the information from the protocol state to know how to respond. In this case it would check Alice's data in the 
  Student Information System to decide if it is going to issue the credential.
- **Controller:** issues another call to the **Aries administration API** with info on how to respond to the previous message. It passes all the
  same types of information as the first message with the content including the **claims** to be put into Alice's **verifiable credential**. It also
  passes a reference to the **protocol state object**
- **Agent Framework Code:** Receives the request, retrieves **protocol state object**, prepares and sends the message to Alice and 
  upates and saves **protocol state object**

There is a lot going on in the process of receiving a response from an agent, but this sequence is basically the same for almost every request/response transaction and it looks a lot like the 
processing of traditional web servers.