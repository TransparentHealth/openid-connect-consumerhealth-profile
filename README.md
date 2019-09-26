# openid-connect-consumerhealth-profile
This is an OpenID Connect Profile outlining additional infomation that should be contained 
in the the `id_token` to facilitate healthcare and related identity logistics.  This Profile is at the inception stage

It profiles the following existing claims:

* `document` - To many types of identifiers with related metadata such as URL. Storing FHIR Patient IDs is part of this profile.
* `address` - To define additional metadata around addresses.
* `gender` - To disamiguate from the definition of `gender_identity` in this OIDC profile.

It extends the following new / emerging claims.

* `aal` - To encode Authenticaotr Assurance Level
* `verified_person_data` - To encode Identity assurace Level (e.g. ID check of license, etc.)
* `membership`   To encode linking a person receiving services with an organization (e.g. A communuity-based-organization or insurance provider.)
* `organizational_agent` - To encode  linking a person who works for (or is an agent of) an organization with said organization.
* `middle_name` - To encode a middle name for aiding with patient linking and matching when no unique identifer (e.g. social security number) is known. (national identity)
* `gender_identity` - To disamiguate from the definition of `gender` in OIDC.
* `emergency_contact` - To encode a person's emergency contacts.



#TODO Add some `id_token` example claims.
