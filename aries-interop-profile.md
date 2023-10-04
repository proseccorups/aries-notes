# The Aries Interop Profile
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