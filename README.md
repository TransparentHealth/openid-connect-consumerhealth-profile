# Consumer Health OpenID Connect Profile(CHOP) - DRAFT

This is an OpenID Connect profile which outlines specific content of the `id_token`. It is designed to address logistical issues surrounding access to health information. The goals of this profile are:

1. To communicate digital identity information in a consistent fashion.
2. To provide a consistent way represent identifiers, which often act as pointers to health information. 
3. To provide a consistent way to model relationships among people and organizations.

This is a draft. Please contribute by using issues feature or make a pull request.

The **CHOP** profile outlines claims (i.e. fields) to be contained within the `id_token`.


**Note**: In the context of identity, the word "claim" is referring to any given field in the `id_token`.  The meaning of "claim" in this context is unrelated to the meaning of the word "claim" in a healthcare context.

Fields / Claims
---------------

This section profile’s fields individually.


Goal 1: Digitial Identity
________________________

* `vot` - To  encode Identity Assurance Level (`1`,`2`, or `3`) and  Authenticator Assurance Level (`1`,`2`, or `3`).  This profile requires that a numerical value for `P` and `C` are set.  (`P0`, `P1`, `P2`, `P3`, `C1`,` C2`, `C3`).  All other `vot` data is optional.

* `vtm` - To reference the  specific set of vector values as defined by NIST 800-63-3.  The value of the `vtm`  claim shall be `https://github.com/TransparentHealth/800-63-3-trustmark/`.

* `verified_claims` - To provide details on the id verification event, if needed. (e.g. Details on a driver's license may be stored here.)

Goal 2: Identifiers
___________________


* `document` - This profile extends the iGov OIDC `doc` claim for documents.https://openid.net/specs/openid-igov-openid-connect-1_0-ID1.html#ClaimsResponse and should help facilitate patient linking and matching. The extension allows additional metadata to be added to fields including codes for `country`, `subdivision` (e.g. state), `url`. The helps better codify state issued documents such as a driver's license. In addition, Patient identifiers in various systems may be stored. For example, a FHIR Patient ID along with the URL to the FHIR server to which it pertains may be stores within the `doc` claim.

Goal 3: Relationships
_____________________

* `agent-to-organization` - For employment relationships. Example: Bob works for ACME Health
* `member-to-organization` - For membership/client/patient relationships. Examples: Bob has insurance through ACME Health. Carol is a client of City Mission. Carlos is patient at Capitol Clinic.  
* `member-to-member` - For family relationships. Examples: Carlos is the spouse of Carol. Frank wants Eve to have access to his records. 
* `agent-to-member` - For Patient/provider relationships. Examples:  Alice, of ACME Health, is the care coordinator for Alice.  Charlie, of City Mission, is the care coordinator for Frank. 

Other Claims:
____________

* `middle_name` - To encode a middle name for aiding with patient linking and matching when no unique identifier (e.g. social security number) is known. (national identity)

* `sex` - A field to indicate biological/birth sex.  Values are `male`, `female`, and `other`.


Example Token
-------------


Below is a sample of content in the `is_token` for James Kirk.  Important information about James Kirk is provided to the replying party , Including:

* James' identity has been verified to IAL2.
* James' middle name is Tiberius. His sex is male. He was both March 22, 2233.
* James' NC state Mediciad ID is 123456789.
* James has an insurance plan with NC Medicaid.
* James is receiving services from ACME Health.
* James has given his spouse, Alice, read access to his medical records.
* James' care coordinator is Carol Capenter, of ACME Health.


Payload of `id_token`:


    {
 	"aud": "sharemyhealth@verifymyidentity",
 	"auth_time": 1573568084.385469,
 	"email": "james@example.com",
 	"exp": 1573571700.0725582,
 	"iat": 1573568100.07256,
 	"iss": "https://oidc.example.com",
 	"nonce": "xc1bl2q8nfHZvxqPBo9C7ThuPTCHw8lEI2CbDWM2kUISaPBYQX57ocJFEznLdX1X",
 	"sub": "130468531371930",
 	"birthdate": "2233-03-22",
 	"email_verified": false,
 	"family_name": "Kirk",
 	"given_name": "James",
 	"middle_name": "Tiberius",
 	"name": "James Kirk",
 	"nickname": "Captian",
 	"phone_number": "+15555555555",
 	"phone_verified": false,
 	"picture": "https://oidc.example.com/media/profile-picture/james-kirk.jpg",
 	"preferred_username": "james",
 	"sex": "male",
 	"vot": "Ab.P2.C2",
 	"vtm": "https://github.com/TransparentHealth/800-63-3-trustmark/",
 	document": [{
        "type": "MEDICAID_ID",
        "num": "123456789",
        "issuer": "dhhs.nc.gov",
        "country": "US",
        "subdivision": "NC",
        "uri": "https://medicaid.ncdhhs.gov/medicaid"
    }],
    "address": [{
 		"formatted": "811 9th St. Suite 120-309\nDurham, NC 27705",
 		"street_address": "811 9th St. Suite 120-309",
 		"locality": "Durham",
 		"region": "NC",
 		"postal_code": "27705",
 		"country": ""
 	}],
 	"member_to_organization": [{
 			"name": "NC Medicaid",
 			"slug": "nc-medicaid",
 			"relationship_type": "Primary Medial Insurance",
 			"sub": "270687240429810",
 			"picture": "https://oidc.example.com/media/org-picture/nc-mediciad.jpg",
 			"website": "https://medicaid.ncdhhs.gov",
 			"phone_number": "+15555559999",
 			"scope": "profile user/*.*"
 		},
 		{
 			"name": "ACME Health",
 			"slug": "acme-health",
 			"relationship_type": "Recipient of services form a community-based organization",
 			"sub": "260687240429810",
 			"picture": "https://oidc.example.com/media/org-picture/acme.jpg",
 			"website": "http://acme.example.com",
 			"phone_number": "+155555555555",
 			"scope": "profile user/*.read"
 		}
 	],
 	"member_to_member": [{
 		"name": "Alice Alders",
 		"sub": "160687240429810",
 		"picture": "https://oidc.example.com/media/profile-picture/alice.jpg",
 		"phone_number": "+155555551234",
 		"relationship": "spouse",
 		"scope": "profile user/*.read"
 	}],
 	"agent_to_member": [{
 		"name": "Carol Capenter",
 		"sub": "190688250429811",
 		"picture": "https://oidc.example.com/media/profile-picture/alice.jpg",
 		"phone_number": "+155555558894",
 		"relationship": "Care coordinator",
 		"scope": "profile user/*.*",
 		"organization": {
 			"name": "ACME Health",
 			"slug": "acme-health",
 			"sub": "260687240429810"
 		}
 	}],
 	"verified_claims": [{
 		"verification": {
 			"trust_framework": "nist_800_63A_ial_2",
 			"time": "2019-11-08 16:50:06.252483+00:00",
 			"evidence": [{
 				"type": "id_document",
 				"method": "pipp",
 				"document": {
 					"type": "idcard",
 					"issuer": {
 						"name": "State of North Carolina",
 						"country": "US",
 						"region": "NC"
 					},
 					"number": "1234567",
 					"date_of_issuance": "2019-11-07",
 					"date_of_expiry": "2029-11-07"
 				}
 			}],
 			"claims": {
 				"given_name": "JAMES",
 				"family_name": "KIRK",
 				"birthdate": "1975-10-12"
 			}
 		}

 	}]
    }
