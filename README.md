# drimpy-consent
A repo for using Drimpy as source of NutsConsentCredentials

# terminology
- citizen: a person that wants to register consent. the citizen is equal to the subject and the grantor of the consent (identified by a bsn)
- subject: the person that the consent is about (identified by a bsn)
- grantor: the person that grants the consent.
- drimpy: organization that registers consent-records and issues NutsConsentCredentials
- custodian: organization that holds source data. the citizen wants the custodian to give acces to data concerning a specific purposeOfUse. this access can be generic (an actor if not specified) of it can be specific (the citizen wants the custodian to give access to a specific actor). custodian is equal to grantee
- grantee: custodian
- actor: organization that is granted will access the data that resides at the custodian

# flow 
The flow consits of 3 major parts:
1. one time onboarding, by vendor Drimpy
2. one time onboarding, by vendors of custodians
3. create consent-record, by citizen

## one-time on-boarding drimpy
Goal: the goal of this part is to register that the vendor Drimpy trusts other vendors for the issuance of NutsOrganizationCredentials. 
Why: This is necessary to be able to look up the did:nuts-identifiers of custodian-organizations and actor-organizations that the citizen wants to give consent to. 
- 1.1: Drimpy needs to trust the other vendors as issuers of NutsOrganizationCredentials. 

The DID's:
- parsek:	did:nuts:DW7R4nk1he5aP7ZRMBUT8yB6RYYTUsKsHBn5eYrgQj6Y
- Interoplab:	did:nuts:GQVCPtXWSStiTFfxNmdX679YGF7rvGFjk3DMZvHMect2
- Firely:	did:nuts:77HfbxNYTx9v9tNow51xXnwMc9io85q6BneP6nKASeiU
- Nexus:	did:nuts:AkPuuhpkbfnmQUFSfycjqrv9nN3L7tkbyGKZG4MfRvtX
- Kiesz:	did:nuts:CkCCGbA7LxsKPYPj9mbHqRQc3382azg2TehXD3coBm7b

## one-time on-boarding vendors of custodians
Goal: the goal of this part is to register that the vendors of the custodians trust the vendor Drimpy for the issuance of NutsConsentCredentials. 
Why: This is necessary to be able to sync NutsConsentCredentials from the Nuts-node of Drimpy to the Nuts nodes of the custodians

# create consent-record
- 3.1: login by user (existing tech)
- 3.2: create consent-record (existing tech)
- 3.3: store consent-record (existing tech)
- 3.4 search did:nuts-identifier of custodian
- 3.6 search did:nuts-identifier of actor(s)
- 3.8 register NutsConsentCredential

# NutsConsentCredential
~~~
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://nuts.nl/credentials/v1",
    "http://schema.org/",
    "https://w3c-ccg.github.io/lds-jws2020/contexts/lds-jws2020-v1.json",
    "https://fhircat.org/fhir-r4/original/contexts/root.context.jsonld"
  ],
  "issuer": "did:nuts:PGOPatientID",
  "type": ["VerifiableCredential", "nuts:NutsConsentCredential"],
  "expirationDate": "2023-04-03T20:34:17.687862+01:00",
  "credentialSubject": {
    "id":"did:nuts:123-CareOrganisation",
    "type":"Organization",
    "member": {
      "type":"fhir:Consent",
      "fhir:subject":"urn:bsn:99998",
      "fhir:decision":"allow",
      "provision":{
        "action":"access",
        "actor":"did:nuts:456-Huisarts",
        "fhir:purpose":["zorginzage"]
      }
    }
  },
  "issuedAt":"2023-04-17T16:05:00",
  "expirationDate":"2024-04-17T16:05:00",
  "proof": {
    "type": "JsonWebSignature2020",
    "verificationMethod": "did:nuts:123456789#key-1",
    "created": "2023-04-03T16:34:17.687862+01:00",
    "jws": "eyJhbGciOiJFUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..hKcboC8m6YnZPi6ReJAYs0J0Ztn5nxcx2EavoXdtrkWxmE1JZmImW89_8IIgjvfI8XtGeDlEnGywAuY2u7y9Bw"
  }
}
~~~

# Build plan
1. Deploy nuts-node in the development-network using this documentation: https://nuts-node.readthedocs.io/en/stable/pages/getting-started/3-configure-your-node.html
2. use Postman for onboarding
3. Add API-calls 3.4, 3.6, 3.8 to Drimpy-app