# Mobile Wallets
Aries Mobile Wallets offer all the functionalites that have already been talked about. They are an Agent like any other.
They can establish connections, exchange credentials etc. Since wallets are more focused towards 
people, the typical use case for them would be to be a credential holder. That would mean the main functionalities
will be receiving credentials, requesting and presenting proofs.

## Core Capabilities of Aries Mobile Wallets   
- Some kind of toturial to help the user get used to the functionalities of the wallet.
- Mediator connection is established (automatically or with some user input)
- If the wallet is secured with biometrics, this is done entirely on the device. Biometric is not accessible to anyone.
- Big button with option to scan QR-code, which is the favored method to establish a connection.
- Once connection is established, messages and presentation requests etc can be sent.
- Once the connection is made it won't have to be re-established

## Credentials and Connection Lists
There is an ongoing debate of whether the main focus of apps should be to show **Credential/connection** 
lists or not. The internal framework already knows which connection is asking for something and users
dont have to scroll trough their contacts themselves. When a request for proof is received, the internal
framework also looks through the available credentials automatically, finds the credentials and asks
the user for confirmation for sending the proof.

The current focus for **Credential and Connection** lists is to just get a **history** of both. The user will
be able to see **when** a connection was established and what interactions occurred with it. When a **credential** was
received, **when** it has been used and **what** it has been used for.

**Scanning QR-codes** is the **main** focus, **credential and connection** list information comes **second**.

## Credential Types and Ledgers
To this point, all Aries mobile wallets use AnonCreds credentials and a Hyperledger Indy ledger. This is mainly because of the
following reasons:
- Aries' roots lie in Indy.
- Those technologies offer a lot of privacy preserving features.
- AnonCreds are easier to use from a business and developer perspective.

AnonCreds are easy to use because compared to other credentials, AnonCreds make a lot of decisions
about how issuers, holders and verifiers interact that would otherwise have to be implemented manually.

For wallets working with Indy, wallet deployments will need to decide what Indy ledgers to support. The most 
common approach is to just support some **test ledgers** that developers are most likely to use and **production ledgers**
that are most likely to be used by customers.