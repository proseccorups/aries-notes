# Protocols with JSON-LD

### What is JSON-LD


### Credentials

With JSON-LD you do *not* create a schema or credential definition. Those are only required for indy credentials.

The recommended approach to defining credentials is to define a credential-specific vocabulary 
(or make use of existing ones). (Note that these can include references to https://schema.org, 
you just shouldn't use this directly in your credential.)

A better example is to use the W3C citizenship context to issue a PermanentResident credential. It 
looks like this:

some attributes to take note of: 
- Connection_id: The id of the connection that should already be established with the other agent
- @context: links to what kind of format (context) you are using to construct your credential
- issuer: The DID of the agent that is sending the credential
- credentialsubject/id: The DID of the agent that is to receive the credential
- attributes: Every other value in the credentialSubject block are the attributes
- prooftype: The type of signature used. E.G. "Ed25519Signature2018" or "BbsBlsSignature2020"


```
{
    "connection_id": "41acd909-9f45-4c69-8641-8146e0444a57",
    "filter": {
        "ld_proof": {
            "credential": {
                "@context": [
                    "https://www.w3.org/2018/credentials/v1",
                    "https://w3id.org/citizenship/v1"
                ],
                "type": [
                    "VerifiableCredential",
                    "PermanentResident"
                ],
                "id": "https://credential.example.com/residents/1234567890",
                "issuer": "did:key:zUC7Dus47jW5Avcne8LLsUvJSdwspmErgehxMWqZZy8eSSNoHZ4x8wgs77sAmQtCADED5RQP1WWhvt7KFNm6GGMxdSGpKu3PX6R9a61G9VoVsiFoRf1yoK6pzhq9jtFP3e2SmU9",
                "issuanceDate": "2020-01-01T12:00:00Z",
                "credentialSubject": {
                    "type": [
                        "PermanentResident"
                    ],
                    "id": "did:key:zUC7CXi82AXbkv4SvhxDxoufrLwQSAo79qbKiw7omCQ3c4TyciDdb9s3GTCbMvsDruSLZX6HNsjGxAr2SMLCNCCBRN5scukiZ4JV9FDPg5gccdqE9nfCU2zUcdyqRiUVnn9ZH83",
                    "givenName": "ALICE",
                    "familyName": "SMITH",
                    "gender": "Female",
                    "birthCountry": "Bahamas",
                    "birthDate": "1958-07-17"
                }
            },
            "options": {
                "proofType": "BbsBlsSignature2020"
            }
        }
    }
}
```

Another example of a possible credential using the **W3C Vaccination Schema**:

```
{
  "connection_id": "ad35a4d8-c84b-4a4f-a83f-1afbf134b8b9",
  "filter": {
    "ld_proof": {
      "credential": {
        "@context": [
          "https://www.w3.org/2018/credentials/v1",
          "https://w3id.org/vaccination/v1"
        ],
        "type": ["VerifiableCredential", "VaccinationCertificate"],
        "issuer": "did:key:zUC71pj2gpDLfcZ9DE1bMtjZGWCSLhkQsUCaKjqXtCftGkz27894pEX9VvGNiFsaV67gqv2TEPQ2aDaDDdTDNp42LfDdK1LaWSBCfzsQEyaiR1zjZm1RtoRu1ZM6v6vz4TiqDgU",
        "issuanceDate": "2020-01-01T12:00:00Z",
        "credentialSubject": {
            "id": "did:key:aksdkajshdkajhsdkjahsdkjahsdj",
            "type": "VaccinationEvent",
            "batchNumber": "1183738569",
            "administeringCentre": "MoH",
            "healthProfessional": "MoH",
            "countryOfVaccination": "NZ",
            "recipient": {
              "type": "VaccineRecipient",
              "givenName": "JOHN",
              "familyName": "SMITH",
              "gender": "Male",
              "birthDate": "1958-07-17"
            },
            "vaccine": {
              "type": "Vaccine",
              "disease": "COVID-19",
              "atcCode": "J07BX03",
              "medicinalProductName": "COVID-19 Vaccine Moderna",
              "marketingAuthorizationHolder": "Moderna Biotech"
            }
        }
      },
      "options": {
        "proofType": "BbsBlsSignature2020"
      }
    }
  }
}
``` 

