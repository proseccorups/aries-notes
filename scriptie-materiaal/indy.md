# Hyperledger Indy
One of the more important features of SSI is the fact that when a credential is being verified, there is no need to go 
back to the issuer of the credential to confirm its validity. The validity is instead retrieved from an independent source,
which in the case of SSI, is the ledger. Hyperledger Indy provides the basis for deploying such ledger technology and building
applications that interact with it.

## The Indy blockchain
There are a multitude of advantages that come with using a blockchain. 
- **Decentralization:** There is no single central authority responsible for whatever the goal of your project is, be it some
  supply chain management system, voting system or more relevant to this report: a mechanism for defining and issuing credentials.
  This mitigates risks like fraud, tempering with data and other issues that could stem from centralized corruption.
- **Security**: Transactions are agreed upon using consensus mechanisms and every transaction is recorded permanently on the shared ledger.
  In combination with the decentralized aspect, this also helps in preventing issues like fraud, since if fraudulent activities were to occur, they
  can be tracked down via the ledger.
- **Transparency**: Every transaction on the blockchain is available to all participants, providing transparency that could not be 
  unlike any other digital technology. Transparency goes hand in hand with the points made in security and can also help with verifying
  the truth of information.

The Indy blockchain implementation is slightly different from how other blockchains might operate. Indy ledgers are immutable, so when
data is written it can never be changed.

When building an application using the technology, the blockchain part of Indy is hidden in the background and developers don't have to 
worry about that too much. The developers will focus on the credentials, agents, controllers and relationships between them. 
