# Handling Credential Revocations

Revocation in software systems is surprisingly difficult. Revocation is often decided by just one entity (issuer),
but everyone involved (holder, verifier) need to be informed in a timely matter. Revocation of AnonCreds is also
tricky, but frameworks like **Aries Cloudagent Python** do most of the work for you. It will at most take the Aries
developer some extra configuration steps.

Some activities of an issuer of revocable AnonCreds credentials are the following:
- Setup for issuing credentials by publishing AnonCreds objects to the ledger and a tails file.
- Issue credentials and create additional revocation registries if needed.
- Track credentials pending revocation.
- Revoke pending credentials by publishing impacted revocation registries to the ledger.

### Complications

This creates some complications for the issuer.

A **tails file** must be published by the issuer such that every credential holder can retrieve it. In order for 
it to also be retrievable by mobile wallets, it needs to be accessible on a SSL certificate protected server (https:).
The BC Gov team has implemented a [Tails Server](https://github.com/bcgov/indy-tails-server) open source reporitory that you
can deploy yourself.

Another complication is that AnonCreds revocation registries are **rather small**, so the number of credentials that
you can issue per revocation registry is also rather small. If the number of credentials you have issues exceeds
that capacity of the revocation registry, you will have to create **another one**.

And another complication is the fact that every time you revoke credentials, you have to **write to the ledger**.
If credentials needs to be revoked in **different registries**, that would mean **multiple writes**.

### ACA-Py to the rescue

Aries Cloudagent Python minimizes the complexity around revocation registries for you, making sure the issuer
won't have a hard time.

If your code indicates that revocation will be used, ACA-Py creates **two revocation registries**. This is to make sure
that when one registry is **full**, there is always **another one ready to go**. As soon as one is full it switches to the next
and a new registry is **generated behind the scenes**.

Here's what AnonCreds revocations looks like from the issuers controller perspective in ACA-Py:
- Deploy, or use a public tails server.
- When starting, pass the tails server as a command line option. ACA-Py will publish tails file for each revocation registry created.
- When creating a credential definition, indicate with a flag that revocation is to be supported. And include the
  size of the revocation registry. Size will be a tradeoff between number of registries needed and tails file size.
- When issuing a credential, save the ID, so it can be used later for revoking the credential if necessary.
- If required, mark a credential as pending revocation using the saved ID, this marks the credential for revocation,
  but does not publish that information.
- Trigger the publishing of revoked credentials. This can be done together with revoking another credential, or periodically.

All these complications **rest on the shoulders of the issuers**. A holder's job is simpler. As long as the ledger
and the path to the tails file is accessible, revocation is handled by AnonCreds so there isn't much for the holder's
agent code to do. One thing could be **checking to see if a credential has been revoked** before sending it as a **presentation proof**.

### Publishing revocations frequency

How often should you publish revocations to the ledger? There is a cost associated with publishing so you want 
to avoid excess publishing, but on the other hand your verifiers may want to know about revocations asap. Revocations 
could be published **"on demand"**, or periodically. An organisation could do a daily write of all revocations, and 
maybe define a separate category of **"emergency"** revocations that need to happen immediately. This would result
in considerably less writes to the ledger compared to just doing everything on demand.