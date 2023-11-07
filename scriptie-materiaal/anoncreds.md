# Hyperledger AnonCreds

## Features
AnonCreds provides the features that you would expect from a Verifiable Credential, like who issued the credential and making
sure that the credential was not altered between issuance and presentation, but also offers some features on top of that. 
- The holder does not necessarily have to provide the "entire" original verifiable credential
- The holder is not given a unique identifier when proof was presented.
- There is a binding to prove that a presentation comes from the same holder that the credential in question was issued to
- There is a binding to prove that when multiple credentials are requested, they were all issued to the same holder
- A holder can "choose" specific attributes from their credentials to "reveal" to the verifier, allowing privacy of other attributes
- A presentation can contain Zero Knowledge Proof predicates, wherein instead of proving you have a certain attribute value, you can
  present that the value of one or more attributes conform(s) to the predicate put in place by the verifier.