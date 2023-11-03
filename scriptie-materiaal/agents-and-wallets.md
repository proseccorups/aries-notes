# Agents and Wallets
As one might imagine, all interactions involving DIDs and Verifiable Credentials happen digitally, so there need to be some
entities that perform those interactions. Hyperledger Aries and other hyperledger project use the term **agent** for the 
piece of software that is doing that. An individual person might have a mobile wallet **agent** while an organisation might
be running one or more agents on enterprise servers or in the cloud.

### Storage
In a Hyperledger SSI setup, agents have secure storage to store identity information such as DIDs and verifiable credentials
and maybe a list of trusted issuers