# Verifiable Credential

## Words and Terms
- **Claim:** An assertion about the holder of the credential. E.g. Name: niek, age: 25

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

### Cryptographic Signing
Cryptographic signing can be summarized in a high level way as follows: 
- Issuer creates keypair that is mathematically linked. Keeps private key itself
- Issuer runs operation that takes information, and private key as inputs
- Issuer uses that information to produce a signature
- A verifier gets the information, the public key and the signature
- Verifier runs verification process that user signed information, signature and public key
- Process returns verified

Cryptography makes sure that is it extremely unlikely (borderline impossible) to produce a signature
without a private key. It's also nearly impossible to alter any information and still producing
the same signature. Nearly impossible in this context means that it wouldn't happen in billions of attempts and hundreds
of years. 

## What makes VC's so powerful?

### Saving money and time
Instead of manually entering your information you give a presentation provided by 
an authority that is trusted by the verifier. Verifier automatically accepts the presentation
and there is no need for further checks if they trust the issuer. This saves time and thus money

### prevent impersonation
If someone has access to your government identifier, they would still not be able
to impersonate you since the information would not come from a Verifiable Credential
issued by the government to you.

Every place that we still rely on data that is self-asserted and paper documents, verifiable 
credentials probably offer a better, safer, faster and cheaper option

### You are in control
A verifiable credential is issued to you personally and stored in whatever wallet 
that you might be using. This means that you as the holder are in control of when you want
to present the credential and to who you want to show it. This empowers privacy of the individual.

### Presentation is proven without call back to issuer
With a verifiable credential the verifier does not need to confirm the presented
proof with the issuer themselves. A Verifiable Credential serves as sufficient proof. The holder
is the one to present the data from the issuer and the cryptographic material is used to 
verify that the data is authentic. This prevents a lot of direct connections between verifiers and issuers
that would otherwise have had to be made. 

### Not just identification
Verifiable credentials can basically be used to replace any verification process that still
involves physical proof. Take for example the Dutch VOG (Verklaring Omtrent Gedrag). This is still
a physical document that is sent to you personally by the government institute responsible for 
issuing them. If you replace this with a verifiable credential, it would save time by not having 
to use a delivery service to get it to your doorstep, and it's less easy to be tampered with because
of the digital and cryptographic nature of credentials.
