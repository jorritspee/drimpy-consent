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

## create consent-record,


