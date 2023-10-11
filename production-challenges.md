# Production Challenges

## Sandbox vs Production-secure Storage Handling

When developing your first proof of concept using a sandbox ledger, you might not necessarily concern yourself 
managing ledgers and your agent's secure storage. If things aren't working you can just reset everything.
During development ledgers and agent storage often unintentionally get out of sync, and you can just reset everything.
In production this is **NOT OK**.

Some production ledgers have a fee for writing to them, and you don't want to pay more than you have to. Even more
crucial is when you are an issuer of credentials, and you base whether you are going to issue one or not on objects
stored on the ledger, you won't be able to if you lose access to secure storage.
Remember that once you are in production, storage is basically a production database, and it must be handled as 
such. Make back-ups and make it secure. A production database is the last thing you would want compromised.

## Agent Storage Back-Up

While backup and  restore of agent secure storage is less important for mobile wallets (users do not write to
a public ledger), on enterprise agents it's crucial from day one.

It's a good thing that backup and restore for enterprise use cases is a well understood problem. Enterprise 
agent storage should be done in an enterprise database such as PostgreSQL, and all of the tools available 
to it. The secure storage on an enterprise agent shouldn't be any different compared to a normal enterprise database.
That's why for both of them, the following points apply:
- Backup regularly
- Run tests to verify the integrity of backups
- Define and (sometimes) execute a agent disaster recovery plan
- Make sure backup are stored in a secure location. Protect both database and encryption keys.

## Indy ledger writing: Legal and Technical complications

Indy ledgers can be easily written to using an API, but there are a couple of added governance related 
complications that need to be covered in most production and some test ledgers.

### Indy Transaction Author Agreement (TAA)

TAA is an optional agreement between someone writing to an Indy instance and the operators of said instance.
If the ledger is configured to use TAA, every call made to that instance needs to include you agreeing to the
TAA. Taking a write transaction as an example, three fields are added to write transactions that the ledger will
check:
- Time of acceptance for the TAA
- Hash of the current TAA
- Enumerated value that shows how the TAA was accepted.


Legally, an organisation must retrieve, review and accept the TAA put in place by the ledger operator before using
it.

Technically an agent writing to a ledger that has a non-empty TAA, needs to get the hash of the current TAA
from the ledger and a list of configured values for how to accept the TAA. This information is stored on the 
ledger in the TXN_AUTHOR_AGREEMENT_AML configuration transaction. (E.G. on Sovrin MainNet: [Sovrin Example](https://indyscan.io/tx/SOVRIN_MAINNET/config/9362))
AML stands for Acceptance Mechanism List. In steps the process would look like this. an Agent must:
- Get AML transaction from ledger
- Have the controller select a method from the AML to use to accept the TAA
- Include the method, a hash from the AML data, and the current timestamp in any ledger write transaction.

Most Aries framework make this process easy. ACA-Py has an Admin API call to read AML data and another one 
**/ledger/taa/accept** that lets you decide how you accept the TAA from the list of options. ACA-Py will, after execution,
automatically add the TAA data to every write. If you add that call to the controller initialization code, you
no longer have to worry about the TAA in code.

This is only the technical side tho, it's still an agreement and like a contract it should be carefully read.