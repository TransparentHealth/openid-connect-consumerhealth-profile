# openid-connect-consumerhealth-profile(CHP) - DRAFT
This is an OpenID Connect Profile outlining to facilitate healthcare and patient-centered data exhange.

**CHP** profiles new and existing claims to be contained within the `id_token`.  These new claims are broken into two sections; **Required** and **Optional**.


Required
--------

Knowing an individual's level of identyity assurance and authenticator assurance is a key peice systems (relying parties) need in order make informed decisions on which actions are appropriate for a given user.

* `ial` - To encode Identity Assurance  Assurance Level (`1`,`2`, or `3`). https://pages.nist.gov/800-63-3/sp800-63a.html
* `aal` - To encode Authenticator Assurance Level (`1`,`2`, or `3`). https://pages.nist.gov/800-63-3/sp800-63a.html


Optional
--------

* `document` - This profile extends the iGov OIDC `doc` claim for documents.https://openid.net/specs/openid-igov-openid-connect-1_0-ID1.html#ClaimsResponse. The extension allows additional metadata to be added to fields including codes for `country`, `subdivision` (e.g. state), `url`. The helps better codify state issued documents such as a driver's license. In addition Patient identifiers in various systems may be stored. For example a FHIR Patient ID along with the URL to the FHIR server to which it pertains may be stores withjin the `doc` claim.
* `address` - To define additional metadata around addresses.
* `middle_name` - To encode a middle name for aiding with patient linking and matching when no unique identifer (e.g. social security number) is known. (national identity)
* `sex` - A field to indicate biological/birth sex.  Values include `male`, `female`, and `other`.
* `verified_claims` - Optional and as per specification.To encode Identity assurace Level (e.g. ID check of license, etc.)
