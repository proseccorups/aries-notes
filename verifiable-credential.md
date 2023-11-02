# Verifiable Credential

## The old way of doing things
The concept of using some form of a credential for identification/authentication is not something unique to Hyperledger and SSI, and 
it's not even a new concept to begin with. We have been giving out 'paper' credentials for a long time now. An authority would 
give you some sort of document to you as holder, which you can then use to present some kind of proof.

### How verifiers can mitigate risk with paper credentials
- Build the cost of the risks associated with document forgery into the cost of their business. Basically raise prices to cover 
  losses induced by false information.
- Manually inspect the documents to see if they look fake. It's easy to see that this is not very reliable
- Motivate the holder to really present valid information by making the consequences for not doing so more grave. For example having the 
  presenting of a fake driver's licence result in not being able to receive a license for a certain period of time, along with a criminal record.

Those techniques all come with a cost, and it would obviously be best to try to avoid that as much as possible. Luckily Verifiable Credentials offer
solutions to these problems.

## What is a credential
A credential is a proof of having certain qualifications, being competent and/or having some sort of authority. A credential can not only
be given out to individuals, but also to organisations. Some examples of credentials being given out today are:
- Driver's license
- ID card
- School diploma/certificate
- A dutch VOG (Verklaring Omtrent Gedrag)
- and many more...

A credential is often used in the case where there is an issuer, holder and a verifier. The issuer will be the one to give out the
credential itself. The holder is the one the credential is being given to, and the verifier is the one that will need you to prove
something with that credential. 
Take for example an academic certificate like a bachelor's degree. In this case the issuer would be the school the courses were taken at,
the holder would be the student receiving the degree, and the verifier could be any company the student will apply for a job at.
The company will be able to confirm that the necessary requirements are met without them seeing any unnecessary data. The holder 
is in charge of the data and can decide if they want to share it or not. This is called the paper credential model.

### What does a credential prove?
A credential should prove who issued the credential, who holds the credential and that the claims that are being made in the 
credential are authentic and unaltered.

### Trust the issuer
Trusting the issuer remains a problem. If the issuer of a credential can not be trusted, the credential itself can not be trusted.
Trust the holder gets a lot easier with digital credentials but trusting the issuer remains a challenge.

## Cryptographic Signing