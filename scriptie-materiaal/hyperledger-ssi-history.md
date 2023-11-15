# Hyperledger SSI history
In total there are four Hyperledger Projects that are relevant to SSI and all have their own set of tasks they accomplish.
Those four projects are Hyperledger Indy, Aries, AnonCreds and Ursa. Below you will find some high level overviews of the 
philosophies behind these technologies and what part they play in enabling Self Sovereign Identity.

## Indy
It all started with Hyperledger Indy. Indy is a distributed ledger software with a focus on identity. It's made up out of tools,
libraries and components for providing digital identities that exist on a blockchain. Indy can be used on combination with other
blockchains or standalone, with the main goal of decentralizing identity.

The code for Indy was contributed by the Sovrin Foundation, which is a nonprofit organization established to manage 
the Sovrin network. It's an independent organization who take responsibility for making sure the Sovrin system is globally
accessible at all times. The Sovrin network is a decentralized public permissioned blockchain, designed to enable self-sovereign
identity. The fact that it's permissioned means that not just anyone can become a node on the Sovrin network, but validators have
to be known and approved by the governing body which is Sovrin themselves.

Over time Indy has evolved into a flexible tool that consists of just the ledger, tools for managing the ledger and client libraries
for interacting with Indy ledgers.

## Ursa
Hyperledger Ursa is a project that naturally evolved out of the Indy project, which is reflected in the timeline. It was created
to save both time and effort because the Hyperledger community realised that if they collaborated on cryptographic code, it would 
be able for different projects to use the same code without problems. 
It came to be in 2018, when the indy-crypto code was migrated into its own repository called Ursa. Cryptographic algorithms are 
quite niche when it comes to software development, which means that only a small amount of experts are familiar with how they work
and only said experts should be programming them. Ursa lets the experts work together to build the cryptographic technologies 
that other developers can use. Ursa is built to be used by both Indy and Aries and other projects that need a solid cryptographic base.

## Aries
The star of the show and the main point of research for this report is Hyperledger Aries. It is the complete package for creating
decentralized identity solutions and online trust. Use it to issue, store and verify credentials with privacy and confidentiality. 
It supports a variety of protocols credential types, ledgers and registries. There are Aries frameworks in development for multiple 
languages to make at as accessible for developers as possible.
Aries was created with the philosophy of being a flexible tool for implementing SSI. Indy and AnonCreds are both great tools, but they
are not the only ones of their kind. Aries is an agent that can use DIDs and Verifiable Credentials from multiple ecosystems and was 
officially accepted as a Hyperledger project in March 2019.
Aries is designed so that no matter how the SSI world evolves over the years, Aries is the tool that you can keep relying on 
for implementing SSI. At it's core, Aries is a set of protocol specifications that let agents interact with each other using interactions
based on DIDs and higher level protocols to accomplish whatever SSI related goal they might have, be it issuing, presenting or verifying 
credentials. Using protocols ensures flexibility, an example being supporting different kinds of credential types within a short timespan.

## AnonCreds
AnonCreds is short for Anonymous Credentials, and is the most commonly used verifiable credential format in the world. Alongside
providing all the assurances that come with verifiable credentials, AnonCreds adds privacy-protecting Zero Knowledge Proof capabilities.
AnonCreds is a more recent addition to the Hyperledger SSI portfolio, and it also came about from Indy into a standalone project. Although
this might insinuate that AnonCreds can only be used with Indy, this is not the case. AnonCreds is the system that allows for the creation
and verification of anonymous credentials and protecting the privacy of the credential holder is paramount.