# The Aries Interop Profile

### What is AIP

The Aries Interop Profile (AIP) in the context of Hyperledger Aries refers to a specific 
set of rules, protocols, and conventions that enable different Aries-based agents and systems 
to interoperate, ensuring they can communicate and interact seamlessly.

Interoperability is crucial in any software component built to run protocols, because you must
ensure that it is able to work with other devices it's supposed to 'interop' with.

Here is a quick list of bullet points what Interop Profiles are about:

- Each AIP has a version number starting with 1.0 (sort of like wi-fi versions)
- Each AIP has a mission, a set of goals that Aries implementation will be able to accomplish if they
  are compliant with that AIP version
- Each AIP defines a set of Aries RFC's that all compliant implementations will support.
- For each included RFC, a link in the AIP goes to a specific version of the RFC or external standard
- An RFC-driven suite of tests enables demonstrating interoperability across Aries Implementations

The biggest change in the AIP 2.0 that was approved in may 2021, is that it offers support for ledgers
other than Indy and verifiable credential formats other than AnonCreds.

### How do AIPs and their versions impact developers

Many of the RFC's in the AIP are not related to protocols and are addressed within the Aries frameworks
themselves. They are not really a concern for those building controllers. The RFC's that are important to learn
for developers are the Aries Messaging Protocols.

As you select a framework to use. You must take the AIP support and plans for future support into consideration.
As of now the newest AIP is 2.0, so that should be the point of focus.

If you want your agent to work with other agents in the ecosystem, you have to take the AIP versions
that are supported by those agents into account. If you build the 'latest and greatest' issuer of credentials,
but there are no actual mobile agents available that are able to receive them. It will be lonely.
Being stuck in 'old tech' is obviously a problem and you should encourage people to move steadily forward

While most of the hard work about supporting an AIP is in the agent framework itself, controllers will
be impacted in the form of changes to the administrative API. Be aware of changes to endpoints you are using.