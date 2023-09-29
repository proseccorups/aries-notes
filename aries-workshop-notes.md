# Hyperledger Aries Workshop Notes

## What is Hyperledger Aries
- Anonimity is a double edged sword. Sometimes we need to know someone's identity.
- It's easy to also pretend to be someone you're not.
- Identity can be something ( a datapoint ) that can be anything as long as both parties involved agree that it has some kind of value to them.

## Why a decentralized model
- You hold on to your own digital identity without it being shared around for you.

## Trust in data
- **Authenticity**: Being able to identify the source of the data
- **Integrity**: Knowing if data is "real" or has arrived as it was originally "issued"
- **Usefullness**: Once provenance is assured, how well do I know the originator of the data.

## Trust model
- **Philosophical trust**: I'll give you the key to the car if you have a real divers license
- **Cryptographic trust**: based on credentials. If you have a valid key, you are trusted.

## Identity Agents
- They act on behalf of a single identity owner
- Holds and uses cryptographic keys to securely perform their responsibilities
- Interacts with other agents trough DID Communication Protocols
- An agent receives messages over HTTP