# PLEASE NOTE
This document is in draft. With feedback from clients, etc.., this API WILL change.
When it is release and is not going to change, then the below will be removed, along with this note

![DRAFT DOCUMENT](/images/DRAFT.png "'This document is in draft'")

# Identity API

This API allows you to:
* the creation of a Person Identity
* The creation of an organisation Identity
* The appropriate person/organisation be added as the UBO to the company/person

---

# Flow

This process flow is intended to work in the following manner. Below an example using a "person" and "company"
identity will be used as the example.

## Assumptions
* that there is only one UBO of the company -> the person in the example -> "Fred Smith"
* the person is a simplified example (e.g. no aliases)
* the company is a limited company with a var (UK) registration
  * the company is 100% owned by Fred Smith
  * And he is the sole director
  * it was incorporated and vat registered on the 2021-12-31
  * the address and phone number are the same as the Fred Smith
* the encryption in transit is "ignored" for this example
* UUID are example ones.
* Data is "example"

## Process

### NOTE ABOUT URL CALLS
Please read the Encryption API. In the below information for the examples of how to interact:
* URLs -> these are in the "encrypted_url"
* JSON for change actions (post) -> these are in the "encrypted_payload". This can be null if GET
* username -> this the the agreed username (e.g. machine@example.com) that will access the API
* method -> GET or POST

Other than the "method" (used for routing), all other data must be encrypted as per the information
in the Encrypted API section

```json
{
	"encrypted_payload": null,
	"encrypted_user": ENCRYPTED(<username>),    
	"encrypted_url": ENCRYPTED("/onboarding/identity/<UUID>"),
	"method": "GET"
}
```

### Diagram
The high-level flow is as such

![high-level](/images/ubo.jpg 'This image is to be done')

### Create the person
First action is to create the person in the identity system. So a post call is made to the endpoint

```json
{
  "external_id": "ClientRefId_43971e26-61b1-420b-9add-c510d44a354f",
  "type": "PERSON",
  "person": {
    "external_id": "ClientPERSONRefId_43971e26-61b1-420b-9add-c510d44a354f",
    "date_of_birth": "1979-12-31",
    "details": {
      "id": "43971e26-61b1-420b-9add-c510d44a354f",
      "title": "Mr",
      "surname": "SMITH",
      "firstname": "FRED",
      "gender": "MALE",
      "married": "YES",
      "dates": {
        "date_from": "1979-12-31"
      },
      "status": "CURRENT"
    },
    "nationality": [
      [
        {
          "country": {
            "country": "England",
            "code": "GB"
          },
          "dates": {
            "date_from": "1979-12-31"
          },
          "status": "CURRENT"
        }
      ]
    ],
    "residency": [
      [
        {
          "country": {
            "country": "England",
            "code": "GB"
          },
          "dates": {
            "date_from": "1979-12-31"
          },
          "status": "CURRENT"
        }
      ]
    ]
  },
  "addresses": [
    {
      "external_id": "ExampleRefId_43971e26-61b1-420b-9add-c510d44a354f",
      "address_line_1": "123 Example House",
      "address_line_2": "Example Road",
      "town": "Example Large Town",
      "state": "Middlesex",
      "postcode": "EX1 1EG",
      "country": {
        "country": "England",
        "code": "GB"
      },
      "type": "PERSONAL",
      "status": "CURRENT",
      "dates": {
        "date_from": "1979-12-31"
      }
    }
  ],
  "telephone": [
    {
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "routing_type": "MOBILE",
      "number_type": "PERSONAL",
      "number": [
        {
          "tel_type": "LOCAL",
          "tel_number": "07117 754764"
        }
      ],
      "country": {
        "country": "England",
        "code": "GB"
      }
    }
  ],
  "email": [
    {
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "email_type": "PERSONAL",
      "email": "example@example.com"
    }
  ],
  "compliance": {
    "screened": "CLIENT",
    "risk_rated": "CLIENT"
  },
  "terms_of_service": {
    "tos_accepted_date": "2023-01-11",
    "tos_accepted": true
  }
}
```
And assuming successful the response is:

(note the Identity Reference (id) is fc843eee-debf-11ed-b5ea-0242ac120002)

```json
{
  "id": "fc843eee-debf-11ed-b5ea-0242ac120002",
  "external_id": "ClientRefId_43971e26-61b1-420b-9add-c510d44a354f",
  "type": "PERSON",
  "person": {
    "id": "43971e26-61b1-420b-9add-c510d44a354f",
    "external_id": "ClientPERSONRefId_43971e26-61b1-420b-9add-c510d44a354f",
    "date_of_birth": "1979-12-31",
    "details": {
      "id": "43971e26-61b1-420b-9add-c510d44a354f",
      "title": "Mr",
      "surname": "SMITH",
      "firstname": "FRED",
      "gender": "MALE",
      "married": "YES",
      "dates": {
        "date_from": "1979-12-31"

      },
      "status": "CURRENT"
    },
    "nationality": [
      [
        {
          "id": "43971e26-61b1-420b-9add-c510d44a354f",
          "country": {
            "country": "England",
            "code": "GB"
          },
          "dates": {
            "date_from": "1979-12-31"

          },
          "status": "CURRENT"
        }
      ]
    ],
    "residency": [
      [
        {
          "id": "43971e26-61b1-420b-9add-c510d44a354f",
          "country": {
            "country": "England",
            "code": "GB"
          },
          "dates": {
            "date_from": "1979-12-31"
          },
          "status": "CURRENT"
        }
      ]
    ],
    "audit_dates": {
      "created": "2023-01-22T13:15:30Z",
      "updated": "2023-01-22T13:15:30Z"
    }
  },
  "addresses": [
    {
      "id": "43971e26-61b1-420b-9add-c510d44a354f",
      "external_id": "ExampleRefId_43971e26-61b1-420b-9add-c510d44a354f",
      "address_line_1": "123 Example House",
      "address_line_2": "Example Road",
      "town": "Example Large Town",
      "state": "Middlesex",
      "postcode": "EX1 1EG",
      "country": {
        "country": "England",
        "code": "GB"
      },
      "type": "PERSONAL",
      "status": "CURRENT",
      "dates": {
        "date_to": "1970-12-31",
        "date_from": "1970-12-31"
      }
    }
  ],
  "telephone": [
    {
      "id": "43971e26-61b1-420b-9add-c510d44a354f",
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "routing_type": "MOBILE",
      "number_type": "PERSONAL",
      "number": [
        {
          "tel_type": "LOCAL",
          "tel_number": "07117 754764"
        }
      ],
      "country": {
        "country": "England",
        "code": "GB"
      }
    }
  ],
  "email": [
    {
      "id": "43971e26-61b1-420b-9add-c510d44a354f",
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "email_type": "PERSONAL",
      "email": "example@example.com"
    }
  ],
  "terms_of_service": {
    "tos_accepted_date": "2023-01-11",
    "tos_accepted": true
  },
  "compliance": {
    "screened": "CLIENT",
    "risk_rated": "CLIENT"
  },
  "audit_dates": {
    "created": "2023-01-22T13:15:30Z",
    "updated": "2023-01-22T13:15:30Z"
  }
}
```
## Create the organisation
From the above identity the ID is used as the UBO id.
There needs to be two -> one for the person as a shareholder, one as the director

```json
{
  "external_id": "ExampleRefId_43971e26-61b1-420b-9add-c510d44a354f",
  "type": "ORGANISATION",
  "organisation": {
    "external_id": "ClientORGRefId_43971e26-61b1-420b-9add-c510d44a354f",
    "company_name": "fredsCompany Limited",
    "company_number": [
      {
        "type": "VAT",
        "value": "1234-123-ab",
        "country_of_number": {
          "country": "England",
          "code": "GB"
        },
        "dates": {
          "date_from": "2021-12-31"
        }
      },
      {
        "type": "COMPANIES_HOUSE",
        "value": "QQ123456",
        "country_of_number": {
          "country": "England",
          "code": "GB"
        },
        "dates": {
          "date_from": "2021-12-31"
        }
      }
    ],
    "type_of_organisation": "LIMITED_COMPANY",
    "facta": false
  },
  "addresses": [
    {
      "external_id": "ExampleRefId_43971e26-61b1-420b-9add-c510d44a354f",
      "address_line_1": "123 Example House",
      "address_line_2": "Example Road",
      "town": "Example Large Town",
      "state": "Middlesex",
      "postcode": "EX1 1EG",
      "country": {
        "country": "England",
        "code": "GB"
      },
      "type": "REGISTERED_OFFICE",
      "status": "CURRENT",
      "dates": {
        "date_from": "2021-12-31"
      }
    }
  ],
  "telephone": [
    {
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "routing_type": "MOBILE",
      "number_type": "PERSONAL",
      "number": [
        {
          "tel_type": "LOCAL",
          "tel_number": "07117 754764"
        }
      ],
      "country": {
        "country": "England",
        "code": "GB"
      }
    }
  ],
  "email": [
    {
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "email_type": "PERSONAL",
      "email": "owners@fredsCompany.com"
    }
  ],
  "ubo": [
    {
      "ubo_identity_id": "fc843eee-debf-11ed-b5ea-0242ac120002",
      "ubo_type": "DIRECTOR",
      "dates": {
        "date_from": "2021-12-31"
      },
      "audit_dates": {
        "created": "2023-01-22T13:15:30Z",
        "updated": "2023-01-22T13:15:30Z"
      }
    },
    {
      "ubo_identity_id": "fc843eee-debf-11ed-b5ea-0242ac120002",
      "ubo_type": "SHAREHOLDER",
      "dates": {
        "date_from": "2021-12-31"
      },
      "audit_dates": {
        "created": "2023-01-22T13:15:30Z",
        "updated": "2023-01-22T13:15:30Z"
      }
    }
  ],
  "compliance": {
    "screened": "CLIENT",
    "risk_rated": "CLIENT"
  },
  "terms_of_service": {
    "tos_accepted_date": "2023-01-11",
    "tos_accepted": true
  },
  "audit_dates": {
    "created": "2023-01-22T13:15:30Z",
    "updated": "2023-01-22T13:15:30Z"
  }
}
```

And the response is

```json
{
  "id": " 6ec9d4ee-dec2-11ed-b5ea-0242ac120002 ",
  "external_id": "ExampleRefId_43971e26-61b1-420b-9add-c510d44a354f",
  "type": "ORGANISATION",
  "organisation": {
    "id": "43971e26-aaaa-420b-9add-c510d44a354f",
    "external_id": "ClientORGRefId_43971e26-61b1-420b-9add-c510d44a354f",
    "company_name": "fredsCompany Limited",
    "company_number": [
      {
        "type": "VAT",
        "value": "1234-123-ab",
        "country_of_number": {
          "country": "England",
          "code": "GB"
        },
        "dates": {
          "date_from": "2021-12-31"
        }
      },
      {
        "type": "COMPANIES_HOUSE",
        "value": "QQ123456",
        "country_of_number": {
          "country": "England",
          "code": "GB"
        },
        "dates": {
          "date_from": "2021-12-31"
        }
      }
    ],
    "type_of_organisation": "LIMITED_COMPANY",
    "facta": false
  },
  "addresses": [
    {
      "id": "43971e26-bbbb-420b-9add-c510d44a354f",
      "external_id": "ExampleRefId_43971e26-61b1-420b-9add-c510d44a354f",
      "address_line_1": "123 Example House",
      "address_line_2": "Example Road",
      "town": "Example Large Town",
      "state": "Middlesex",
      "postcode": "EX1 1EG",
      "country": {
        "country": "England",
        "code": "GB"
      },
      "type": "REGISTERED_OFFICE",
      "status": "CURRENT",
      "dates": {
        "date_from": "2021-12-31"
      }
    }
  ],
  "telephone": [
    {
      "id": "43971e26-cccc-420b-9add-c510d44a354f",
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "routing_type": "MOBILE",
      "number_type": "PERSONAL",
      "number": [
        {
          "tel_type": "LOCAL",
          "tel_number": "07117 754764"
        }
      ],
      "country": {
        "country": "England",
        "code": "GB"
      }
    }
  ],
  "email": [
    {
      "id": "43971e26-dddd-420b-9add-c510d44a354f",
      "valid": true,
      "primary": true,
      "confirmed": true,
      "details_confirmed_by": "CLIENT",
      "email_type": "PERSONAL",
      "email": "owners@fredsCompany.com"
    }
  ],
  "ubo": [
    {
      "id": "43971e26-eeee-420b-888-c510d44a354f",
      "ubo_identity_id": "fc843eee-debf-11ed-b5ea-0242ac120002",
      "ubo_type": "DIRECTOR",
      "dates": {
        "date_from": "2021-12-31"
      },
      "audit_dates": {
        "created": "2023-01-22T13:15:30Z",
        "updated": "2023-01-22T13:15:30Z"
      }
    },
    {
      "id": "43971e26-gggg-420b-888-c510d44a354f",
      "ubo_identity_id": "fc843eee-debf-11ed-b5ea-0242ac120002",
      "ubo_type": "SHAREHOLDER",
      "dates": {
        "date_from": "2021-12-31"
      },
      "audit_dates": {
        "created": "2023-01-22T13:15:30Z",
        "updated": "2023-01-22T13:15:30Z"
      }
    }
  ],
  "compliance": {
    "screened": "CLIENT",
    "risk_rated": "CLIENT"
  },
  "terms_of_service": {
    "tos_accepted_date": "2023-01-11",
    "tos_accepted": true
  },
  "audit_dates": {
    "created": "2023-01-22T13:15:30Z",
    "updated": "2023-01-22T13:15:30Z"
  }
}
```


### Results
In the system you have created:
* Person Identity for Fred Smith
  * ID is fc843eee-debf-11ed-b5ea-0242ac120002
* Company Identity for _"fredsCompany Limited"_
  * ID is 6ec9d4ee-dec2-11ed-b5ea-0242ac120002
* With Fred Smith as a UBO (Director and shareholder) of _"fredsCompany Limited"_ (UBO)

---

# UBOS

## Companies
Below is a table showing the MINIMUM required for each company type
(note ALL shareholdings of 25% or more must be declared as a UBO, and in some cases a company can be a UBO - example holding company)

| Company Type     | DIRECTOR | SHAREHOLDER | OTHER              |
|------------------|----------|-------------|--------------------|
| LIMITED_COMPANY  | 1+       | Normally 1+ | Yes if applicable  |
| SOLE_TRADER      | 1+       | Normally 1  | Yes if applicable  | 
| PARTNERSHIP      | 1+       | Normally 2+ | Yes if applicable  | 
| LLP              | 1+       | Normally 1+ | Yes if applicable  | 
| PLC              | 1+       | 0+          | Yes if applicable  | 
| OTHER            | 1+       | 0+          | Yes if applicable  | 

If a valid Identity ID is NOT provided for the organisation for this roles/combinations, the request will be rejected

## Person

A person can also have a UBO -> these tend to be Guardian, Executor, Court Appointed etc..

---
# Compliance and Terms Of Service

## Terms Of Service (TOS)
For ALL identities you create, as per the terms of service then:
* you must accept that the Terms Of Service have been accepted for this Identity (company or person)
* provide the appropriate date when this occurred

## Compliance
For ALL identities you create, as per the terms of service then you must:
* undertake the appropriate KYC/AML actions
* state, upon creation, that you have undertaken these

## Rejection
If the Terms Of Service is missing, and the Compliance confirmation, then the request to create will be rejected



---
# Minimum Required Values
Currently (release 1.0.x) the following are the required values

| Main Object/value | Sub Values                     | For            | Notes                                                     |
|-------------------|--------------------------------|----------------|-----------------------------------------------------------|
| external_id       |                                | BOTH           |                                                           |
| type              |                                | BOTH           |                                                           |
| organisation      |                                | ORGANISATION   | Do not supply any details here if person                  |
| organisation      | external_id                    | ORGANISATION   |                                                           |
| organisation      | company_name                   | ORGANISATION   |                                                           |
| organisation      | company_number                 | ORGANISATION   | Yes if LTD/PLC etc..                                      |
| organisation      | type_of_organisation           | ORGANISATION   |                                                           |
| organisation      | facta                          | ORGANISATION   |                                                           |
| Person            |                                | PERSON         | Do not supply any details here if organisation            |
| Person            | external_id                    | PERSON         |                                                           |
| Person            | date_of_birth                  | PERSON         |                                                           |
| Person.details    | surname                        | PERSON         |                                                           |
| Person.details    | firstname                      | PERSON         |                                                           |
| Person.details    | dates                          | PERSON         |                                                           |
| Person.details    | dates.date_from                | PERSON         |                                                           |
| Person.details    | status                         | PERSON         |                                                           |
| addresses         |                                | BOTH           | At least one (current)                                    |
| addresses         | external_id                    | BOTH           |                                                           |
| addresses         | address_line_1                 | BOTH           |                                                           |
| addresses         | address_line_2                 | BOTH           |                                                           |
| addresses         | town                           | BOTH           |                                                           |
| addresses         | postcode                       | BOTH           |                                                           |
| addresses         | country                        | BOTH           | all                                                       |
| addresses         | type                           | BOTH           |                                                           |
| addresses         | dates.date_from                | BOTH           |                                                           |
| telephone         |                                | BOTH           | At least one (current)                                    |
| telephone         | telephone.valid                | BOTH           |                                                           |
| telephone         | telephone.confirmed            | BOTH           |                                                           |
| telephone         | telephone.details_confirmed_by | BOTH           |                                                           |
| telephone         | telephone.routing_type         | BOTH           |                                                           |
| telephone         | telephone.number_type          | BOTH           |                                                           |
| telephone         | telephone.number               | BOTH           | LOCAL or Internation version of a number                  |
| telephone         | telephone.country              | BOTH           |                                                           |
| email             |                                | BOTH           | At least one (current)                                    |
| email             | email.valid                    | BOTH           |                                                           |
| email             | email.confirmed                | BOTH           |                                                           |
| email             | email.details_confirmed_by     | BOTH           |                                                           |
| email             | email.email_type               | BOTH           |                                                           |
| email             | email.email                    | BOTH           |                                                           |
| terms_of_service  | all                            | BOTH           | This needs the date AND the fact it has been accepted     |
| compliance        | compliance.screened            | BOTH           | you are confirming you have screened WRT AML the identity |
| compliance        | compliance.risk_rated          | BOTH           | you are confirming you have risk rated the identity       |

---
# Headers

## Host/Date

This information is optional.

## `x-correlation-id`

This is supported -> we can take this information and use it, so it is an optional header.
The api may/may no return the `X-Correlation-ID` on calls. Please do NOT rely on this information to be present or match with yours if there is one. As far as we can see with the testing, if you set the `X-Correlation-ID` it will be returned correctly to yourselves on the response.

Note: _Please use uuid only_

---

# Encryption in transit

Please see the "Encryption API". You CANNOT CALL THIS API DIRECTLY, IT MUST BE WRAPPED IN:

### get  example
(get an identity used as example)
```json
{
	"encrypted_payload": null,
	"encrypted_user": ENCRYPTED(<username>),    
	"encrypted_url": ENCRYPTED("/onboarding/identity/<UUID>"),
	"method": "GET"
}
```
### Post example
(create identity used as example)
```json
{
	"encrypted_payload": ENCRYPTED(<payload>),
	"encrypted_user": ENCRYPTED(<username>),    
	"encrypted_url": ENCRYPTED("/onboarding/identity"),
	"method": "POST"
}
```


---

# Provided Jar for your use

There is a Jar that will allow your system to interact with the Fondy system "as if" it was on the same service. Please see the Additional Documentation



