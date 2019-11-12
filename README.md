# openid-connect-consumerhealth-profile(CHP) - DRAFT

This is an OpenID Connect Profile outlining to facilitate healthcare and patient-centered data exchange.

**CHP** profile outlines claims (i.e. fields) to be contained within the `id_token`.  Claims are broken into two sections; **Required** and **Optional**.


Required
--------

Knowing an individual's level of identyity assurance and authenticator assurance is a key peice systems (relying parties) need in order make informed decisions on which actions are appropriate for a given user.

* `vot` - To  encode Identity Assurance  Assurance Level (`1`,`2`, or `3`) and  Authenticator Assurance Level (`1`,`2`, or `3`).  This profile requires that a numerical value for `P` and `C` are set.  (`P0`, `P1`, `P2`, `P3`, `C1`,` C2`, `C3`).  All other `vot` data is optional.

The details for the NIST 800-63-3 to `vot` mapping can be found here: https://github.com/TransparentHealth/800-63-3/blob/nist-pages/sp800-63d/vot-mapping-consumer-health.md



Optional
--------

* `document` - This profile extends the iGov OIDC `doc` claim for documents.https://openid.net/specs/openid-igov-openid-connect-1_0-ID1.html#ClaimsResponse and should help facilitate patient linking and matching. The extension allows additional metadata to be added to fields including codes for `country`, `subdivision` (e.g. state), `url`. The helps better codify state issued documents such as a driver's license. In addition, Patient identifiers in various systems may be stored. For example, a FHIR Patient ID along with the URL to the FHIR server to which it pertains may be stores within the `doc` claim.

* `verified_claims` - Optional and as per specification. To encode Identity assurance Level (e.g. ID check of license, etc.)

*`middle_name` - To encode a middle name for aiding with patient linking and matching when no unique identifier (e.g. social security number) is known. (national identity)

* `sex` - A field to indicate biological/birth sex.  Values are `male`, `female`, and `other`.


Example Token
-------------


Below is a sample of content in the `is_token`'s payload.


    {
    "aud": "sharemyhealth@verifymyidentity",
    "auth_time": 1573568084.385469,
    "email": "james@example.com",
    "exp": 1573571700.0725582,
    "iat": 1573568100.07256,
    "iss": "http://verifymyidentity:8000",
    "nonce": "xc1bl2q8nfHZvxqPBo9C7ThuPTCHw8lEI2CbDWM2kUISaPBYQX56ocJFEznLdX1X",
    "sub": "130468531371930",
    "birthdate": "1975-10-12",
    "email_verified": false,
    "family_name": "Kirk",
    "given_name": "James",
    "middle_name": "",
    "name": "James Kirk",
    "nickname": "CAPTIAN",
    "phone_number": "+13046853137",
    "phone_verified": false,
    "picture": "https://example.com/media/profile-picture/alan_IMGIEON.jpg",
    "preferred_username": "james",
    "sex": "male",
    "vot": "Ab.P2.C2",
    "website": "",
    "address": [
        {
            "formatted": "811 9th St. Suite 120-309\nDurham, NC 27705",
            "street_address": "811 9th St. Suite 120-309",
            "locality": "Durham",
            "region": "NC",
            "postal_code": "27705",
            "country": ""
        }
    ],

    "memberships": [ ],
    "verified_claims": [
        {
            "verification": {
                "trust_framework": "nist_800_63A_ial_2",
                "time": "2019-11-08 16:50:06.252483+00:00",
                "evidence": [
                    {
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
                    }
                ],
                "claims": {
                    "given_name": "JAMES",
                    "family_name": "KIRK",
                    "birthdate": "1975-10-12"
                }
            }
        }
        }
    ]
    }
