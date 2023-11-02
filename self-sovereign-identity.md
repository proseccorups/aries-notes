# Self Sovereign Identity

## What are the problems it's trying to solve?

### User ID + Password
We all know the traditional email/password authentication that is being used almost everywhere, and we probably have had
to deal with its flaws as well. 
- There is too many passwords to keep track of
- We use the same password in multiple locations causing all of them to be compromised if one is
- We use passwords that are easy for us to remember, often meaning they are also often easy to guess

### Identity providers
One approach that many people use today is identity providers. Providers such as Google and Facebook can be used to 
log in to smaller sites. As long as we know our account credentials for Facebook and Google we can log in to any of those sites.
The problem with this is that every time we log in or register somewhere, Facebook or Google will know that as well and keep
track of that information. This is causing Identity Providers to be not only be a security concern if your Facebook or Google
account is compromised, but also brings some privacy concerns with it.

### Centralized identifiers
Nearly all of today's identifiers are centralized entities. Could be the government handing us our driving license/id, or a company
id to log into their system. There are some big problems with this:
- If the centralized authority such as a government oppresses its people, it can choose to take away 'power' from them at any given time
- If the centralized authority is compromised a lot of people are affected. 