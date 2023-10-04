# The Aries Administrative API

### What is the Administrative API?
It's an interface that provides administrative functionalities for managing an Aries agent. This API allows developers 
and administrators to interact with and manage the agent's internal operations and resources.

### What can you do with it

- **Agent management**: enables control over an agent's lifecycle, e.g. starting or stopping an agent
- **Connection management**: create, accept or delete connections with other agents
- **Credential management**: issue, request and manage verifiable credentials.
- **Proof presentation**: Allows for creation of proof requests. Review them and confirm authenticity
- **Protocol Management**: Insight into ongoing protocol interactions, their state and messages.
- **Event Notifications**: Webhook features that fire when important events happen. Like new connections being made or credentials issued
- **Configuration/customization**: Allows querying and updating agent's configurations. (setting mediator agents, changing endpoints or updating internal database)

The exact implementation of the Administrative API depends on the specific Aries agent (framework) you are using. But the general principle remains the same.