# Youverify Documentation
## Welcome! This is Youverify's documentation page

The Youverify API is a RESTful web service for developers to programmatically interact with Youverify’s data and functionality.
Every bit of data exchanged between clients and the API is JSON over HTTPS.

## Environments

We offer both Staging and Production environments. You may leverage our Staging environment to test your integration in a number of scenarios. The Staging and Production environments function similarly, with the difference that sample data can only be used in the staging environment.

-   The base URL for the Youverify staging API is <https://api.staging.youverify.co> 
- The live API endpoint is <https://api.youverify.co>
-   All endpoints should be prefix with v1 e.g <https://api.staging.youverify.co/v1> for staging and while live is <https://api.youverify.co/v1>
-   All sample requests in this documentation are formatted for cURL.
-   All parameters, where relevant, are required unless otherwise specified.
-   If you have questions about using the API, want to share some feedback, or have come across a bug you'd like to report, write us an email at [developer@youverify.co](mailto:developer@youverify.co)
-   Youverify API uses key based authentication method. You can get a key from settings(<https://developer.youverify.co>).

## Identity Verification API's

The Identity Verification API allows you to validate an individual's identity information by utilizing their personal information and ID number from one of our supported ID Types. This API will return a comprehensive information available about the individual.

### Request Values

Name | Type | Description
---------|----------|---------
 report_type | String | Specific youverify service type.
 type | String | Specific identity type.
 reference | String | Required identification number.
last_name | String| Candidate's last name.
first_name | String| Candidate's first name.
dob | String | Candidate's date of birth.
subject_constent |Boolean| Candidate consent to the verification.

### Nigerian International Passport (NIP)

This endpoint lets you verify a passport ID.

Request Sample.

```json http
{
  "method": "POST",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"report_type\": \"identity\", \n \"type\": \"passport\", \n \"reference\": \"Axxxxxxxx\", [required][alphanumeric]\n \"last_name\": \"John\", [ required ] \n \"first_name\": \"Doe\", [ optional ] \n \"dob\": \"2000-01-01\", [ optional ] \n \"subject_consent\": true [required] [Boolean] \n}"
}
```

Successful response:

```json
 { 
  "data": 
  { 
   "id": "reports_7e9b2a5e-1c58-4cc9-a544-371d95d39a12", 
   "reference_id": "5d890625e8841", 
   "response": { 
   "first_name": "JOHN", 
   "last_name": "DOE", 
   "middle_name": "", 
   "dob": "2000-01-01", 
   "mobile": null, 
   "photo": "/9j/4AAQSkZJRgABAgEAYABgAAD//+xIdoMMG+J4NL65A33mbth9RutNh+MYdi //9k=", 
   "gender": "Male", 
   "issued_at": "ALAUSA, LAGOS", 
   "issued_date": "2018-10-30", 
   "expiry_date": "2023-10-29", 
   "reference_id": "Axxxxxxxx" 
   }, 
    "type": "passport",
    "task_created_by": "Inc Youverify" 
    }, 
"message": "Successful", 
"status_code": 200 
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

#### NIP Test Data

ID Number: A11111111

DOB: 1988-04-04

FN: Sarah

MN: Jane

LN: Doe

### Permanent Voters Card (PVC)

This endpoint allows you to verify a PVC ID.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{\n  \"report_type\": \"identity\",\n  \"type\": \"inec\",\n  \"reference\": \"00A0A0A000000000000\",[required][alphanumeric]\n  \"first_name\": \"John\",[optional]\n  \"last_name\": \"Doe\",[optional]\n  \"dob\": \"04-04-1988\" [optional]\n}"
}
```

Successful response:

```json
{
    "data": {
        "id": "reports_08a2e83a-4ca5-4f5d-b006-b16e48e66f41",
        "reference_id": "5f2e90ca155ab",
        "response": {
            "first_name": "John",
            "last_name": "Doe",
            "middle_name": "",
            "dob": "1990-04-04",
            "mobile": null,
            "gender": "Male",
            "reference_id": "00a0a0a000000000000"
        },
        "type": "inec",
        "task_created_by": "Chinook Devops"
    },
    "message": "Successful",
    "status_code": 200
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

#### PVC Test Data

ID Number: 00A0A0A000000000000

FN: John

LN: Doe

DOB: 04-04-1988

### Bank Verification Number with Image (IBVN)

This endpoints allows you to verify the BVN Identity with Images.
 

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"report_type\": \"identity\", \n \"type\": \"ibvn\", \n \"reference\": \"xxxxxxxxxxx\", [required][String]\n \"last_name\": \"John\", [ optional ] \n \"first_name\": \"Doe\", [ optional ] \n \"dob\": \"2000-01-01\", [ optional ] \n \"subject_consent\": true [required] [Boolean] \n}"
}
```

Successful response:

```json
{ 
"data": { 
"id": "reports_65376e11-387e-4e54-b2d9-7511bba9080d", 
"reference_id": "5d89e45394fc1", 
"response": { 
"first_name": "JOHN", 
"middle_name": "", 
"mobile": "xxxxxxxxxx", 
"last_name": "DOE", 
"dob": "01-Jan-00",
"photo": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL//MTgVFKBtDLt3Z71dhXYjx/IDnis6fAJAqe4unAA4xWfJMMHNc87XNVqhCcimA4PvTTIAOtMD/NVwMqmxd0BGgvUUcbvMc59Cf8AHFdnC4K4PNcdoIY3FxOxz0QZ/M/9k=" 
}, 
"type": "ibvn", 
"task_created_by": "Inc Youverify" 
}, 
"message": "Successful", 
"status_code": 200 
}
```

Failed response:

```json


{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

#### BVN Test Data

ID Number: 11111111111 

DOB: 1988-04-04 

FN: John 

MN: 

LN: Doe


### Bank Verification Number (BVN) without Image

This endpoints allows you to verify the BVN Identity without Images.
 

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"report_type\": \"identity\", \n \"type\": \"bvn\", \n \"reference\": \"xxxxxxxxxxx\", [required][String]\n \"last_name\": \"John\", [ optional ] \n \"first_name\": \"Doe\", [ optional ] \n \"dob\": \"2000-01-01\", [ optional ] \n \"subject_consent\": true [required] [Boolean] \n}"
}
```

Successful response:

```json
{ 
"data": { 
"id": "reports_65376e11-387e-4e54-b2d9-7511bba9080d", 
"reference_id": "5d89e45394fc1", 
"response": { 
"first_name": "JOHN", 
"middle_name": "", 
"mobile": "xxxxxxxxxx", 
"last_name": "DOE", 
"dob": "01-Jan-00", 
"type": "ibvn", 
"task_created_by": "Inc Youverify" 
}, 
"message": "Successful", 
"status_code": 200 
}
```

Failed response:

```json


{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

#### BVN Test Data

ID Number: 11111111111 

DOB: 1988-04-04 

FN: John 

MN: 

LN: Doe


### Nigerian Driver's License (NDL)

This endpoint allows you to verify driver's license number.

Request Sample

**NB**: first_name and last_name does not affect the result but are needed by the API – The default can be left as is, just change the "reference" to the NDL number and also the DOB.

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"report_type\": \"identity\", \n \"type\": \"frsc\", \n \"reference\": \"xxxxxxxxxxxxx\", [required][alphanumeric] \n \"last_name\": \"John\", [optional] \n \"first_name\": \"Doe\", [optional] \n \"dob\": \"2000-01-01\", [optional] \n \"subject_consent\": true [required] [Boolean] \n}"
}
```

Successful response:

```json
 { 
"data": { 
"id": "reports_8c4088b0-b04c-4966-9c60-d235db186071",
"reference_id": "5d89e628ded9a", 
"response": { 
"residence_address_line1": "xxxxxxxxxx", 
"residence_town": "xxxxxxxxxx ", 
"residence_lga": "xxxxxxxxxx ", 
"residence_state": "Lagos", 
"application_first_issued_date": "2010-02-26", 
"dob": "2000-01-01”, 
"disability": "No", 
"facial_mark": "N", 
"first_state_of_issuance": "Lagos ", 
"first_name": "JOHN", 
"gender": "M", 
"glasses": "N", 
"height": null, 
"self_origin_lga": "xxxxxxxxxx", 
"license": { 
"class": "D", 
"description": "Motor vehicle other than motor cycle, taxi, stage carriage, an articulated vehicle or vehicle drawing a trailer. " 
}, 
"mobile": " xxxxxxxxxx ", 
"maiden_name": " xxxxxxxxxx ", 
"birth_country": "Nigeria ", 
"next_of_kin_phone_number": "xxxxxxxxxx ", 
"middle_name": "", 
"previous_dl_number": "xxxxxxxxxx ", 
"birth_state": "RIvers",
"last_name": "DOE", 
"reference_id": null 
}, 
"type": "frsc", 
"task_created_by": "Inc Youverify" 
}, 
"message": "Successful", 
"status_code": 200 
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ],
        "dob": [
            "The dob field is required."
        ],
        "first_name": [
            "The first name field is required."
        ],
        "last_name": [
            "The last name field is required."
        ]
    },
    "status_code": 422
}
```

#### NDL Test Data

ID Number: AAA00000AA00

DOB: 1988-04-04

FN: John

MN: Michael

LN: Doe

### National Identity Number (NIN)

This endpoint verifies a National identity number.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"report_type\": \"identity\", \n \"type\": \"nin\", \n \"reference\": \"xxxxxxxxxxxxx\", [required][numeric] \n \"last_name\": \"John\", [ optional ] \n \"first_name\": \"Doe\", [ optional ] \n \"dob\": \"2000-01-01\", [ optional ] \n \"subject_consent\": true [required] [Boolean] \n}"
}
```

Successful response

```json
{ 
"data": { 
"id": "reports_31a5e789-b426-496d-979d-a57f88cf3741", 
"reference_id": "5d89e958c31b1", 
"response": { 
"first_name": "JOHN", 
"last_name": "DOE", 
"middle_name": "", 
"dob": "01-01-2000", 
"mobile": "xxxxxxxxxxx", 
"reference_id": "xxxxxxxxxxx ", 
"batch_id": null, 
"birth_country": "nigeria", 
"birth_lga": "xxxxxxxxxxx", 
"birth_state": "Edo", 
"card_status": null, 
"central_id": "xxxxxx", 
"document_no": null, 
"educational_level": "tertiary", 
"employment_status": null, 
"gender": "m", 
"height": null, 
"maiden_name": null,
"marital_status": "single", 
"nok_address1": "****", 
"nok_address2": "", 
"nok_firstname": "****", 
"nok_lga": "****", 
"nok_state": "Niger", 
"nok_surname": "****", 
"nok_town": "****", 
"nspokenlang": "****", 
"ospokenlang": "****", 
"photo": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0a\nHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/ \nODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTl /\nDXiJbi1NvM+ycIU5GS248n64FaUnrqElpod1ara+ /2Q==", 
"profession": "STUDENT", 
"religion": "christianity", 
"residence_adress_line1": null, 
"residence_town": null, 
"residence_lga": "xxxxxxxx", 
"residence_state": "Niger", 
"residence_status": "birth", 
"self_origin_lga": "****", 
"self_origin_place": "****", 
"self_origin_state": "****",
"signature": "/9j/4AAQSkZJRgABAQEAlgCWAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0a\nHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIy\ +iii\ngDx/4Qf8lD+J3/YVH/o24rhL+w1r48fEHUX06+jh0HT /9k=", 
"title": "mr", 
"tracking_id": "xxxxxxxxxxxxxxxxxxxxxx" 
}, 
"type": "nin", 
"task_created_by": "Inc Youverify" 
}, 
"message": "Successful", 
"status_code": 200
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

#### NIN Test Data

ID Number: 11111111111

DOB: 1988-04-04

FN: Sarah

MN: Jane

LN: Doe

### Bank Verification Number with Facial Match (BVN Facial)

This endpoint allows you to verify a BVN ID with a Facial match.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"report_type\": \"identity\", \n \"type\": \"bvn_facial\", \n \"reference\": \"xxxxxxxxxxx\", [required][string] \n \"last_name\": \"John\", [ optional ] \n \"first_name\": \"Doe\", [ optional ] \n \"dob\": \"2000-01-01\", [ optional ] \n \"image\": \"{Base64 string less than 1MB}\", [required] – Image to be\n  compared with BVN image \n \"subject_consent\": true [required] [Boolean] \n}"
}
```

Successful response:

```json
{ 
 "data": { 
  "id": "reports_65376e11-387e-4e54-b2d9-7511bba9080a", 
  "reference_id": "5d89e45394fc2", 
  "response": 
   { 
    "first_name": "JOHN", 
    "middle_name": "", 
    "mobile": "xxxxxxxxxx", 
    "last_name": "DOE", 
    "dob": "01-Jan-00", 
    "photo": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL//MTgVFKBDLt3Z71dhXYjx/IDnis6fAJAqe4unAA4xWfJMMHNc87XNVqhCcimA4PvTTIAOtMD/NVwMqmxd0BGgvUUcbvMc59Cf8AHFdnC4K4PNcdoIY3FxOxz0QZ/M/9k=", 
    "face_details": 
    { 
     "confidence": 38.72, 
     "threshold": 70,
     "request_image": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL//MTgVFBtDLt3Z71dhXYjx/IDnis6fAJAqe4unAA4xWfJMMHNc87XNVqhCcimA4PvTTIAOtMD/NVwMqmxd0BGgvUUcbvMc59Cf8AHFdnC4K4PNcdoIY3FxOxz0QZ/M/9k=" 
    } 
   }, 
  "type": "bvn_facial", 
  "task_created_by": "Inc Youverify" 
 }, 
"message": "Successful", 
"status_code": 200 
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ],
        "image": [
            "The image field is required."
        ]
    },
    "status_code": 422
}
```

#### BVN Test Data

ID Number: 11111111111 

DOB: 1988-04-04 

FN: John 

MN: 

LN: Doe

### National Identity Number with Facial Match (NIN Facial)

This endpoint allows you to verify a NIN ID with a Facial match.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": {
    "report_type": "identity",
    "type": "nin_facial",
    "reference": "xxxxxxxxxx",
    "image": "{{base64 image}}",
    "subject_consent": true
  }
}
```

Successful response:

```json
{
    "data": {
        "id": "reports_d5185a8d-5c17-474a-ab5f-ee74c61b499b",
        "reference_id": "5fb26a019a504",
        "response": {
            "first_name": "John",
            "last_name": "Doe",
            "middle_name": "Michael",
            "dob": "01-01-1990",
            "mobile": "08111111111",
            "reference_id": "00000000279",
            "batch_id": null,
            "birth_country": "nigeria",
            "birth_lga": "Ikorodu",
            "birth_state": "Lagos",
            "card_status": null,
            "central_id": "8817188",
            "document_no": null,
            "educational_level": "secondary",
            "employment_status": null,
            "gender": "m",
            "height": null,
            "maiden_name": null,
            "marital_status": "single",
            "nok_address1": "****",
            "nok_address2": "",
            "nok_firstname": "****",
            "nok_lga": "****",
            "nok_state": "****",
            "nok_surname": "****",
            "nok_town": "****",
            "nspokenlang": "YORUBA",
            "ospokenlang": "****",
            "photo": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0a\nHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIy\nMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAHSAV4DASIA\nAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQA\nAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3\nODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4e",
            "face_details": {
                "confidence": 89.78,
                "threshold": 70,
                "request_image": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wgARCAQ4AyoDASIAAhEBAxEB/8QAGgABAQEBAQEBAAAAAAAAAAAAAAECAwQFBv/EABgBAQEBAQEAAAAAAAAAAAAAAAABAgME/9oADAMBAAIQAxAAAAL7dlyAAAAAAAAAAAQKlAAAAAAAAAAAAAAAAAAACCoKliWBQELAFIB8/wCh86X4/Lpm3N6w5dufZfodc+znfEFzZokEmNyvsU6cwAAAAAAAAABCgAAAAAAAAAAAAAAAAAAAJSWAIWACikIAAAnzfpfOl+Hnvm3LVOXo5+iX6Xt8nrw8EVrFlICET7I68wAAAAAAAAEsAFAAAAAAAAAgWUAAAAAJQCUBIWAAABYLLAABKEonzvo+HN+e+2r4t+1D4z7Xhl37PJ0zfLJWoDKiS5k+zY687FoQqUAAAEKQqBYAFgoAAAAABCoKQVCgAAAEKgqCogAAAAABYAAAAJ4fd8/N9ossKvg9/gzrd5ZxsWs2UiUkQ+yOnKwooIKCAoIoiwLAILKKABCoKgqCkLFIsLCAAAALLKsIAFIAAAAsAFgsAAAACfP+h8/N9osKqeD3+DOrcTO1zoysICA+wOnKoCyllAIolAQCAAAKloA"
            },
            "profession": "STUDENT",
            "religion": "christianity",
            "residence_adress_line1": null,
            "residence_town": null,
            "residence_lga": "Ibadan South West",
            "residence_state": "Oyo",
            "residence_status": "birth",
            "self_origin_lga": "Ikorodu",
            "self_origin_place": "****",
            "self_origin_state": "Lagos",
            "signature": "/9j/4AAQSkZJRgABAQEAlgkWAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0a\nHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIy\nMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCADIAPoDASIA\nAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQA\nAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3\nODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWm\np6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEA\nAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSEx\nBhJBUQdhcRMiMoEIF",
            "title": "mr",
            "tracking_id": "S7K0OG3150014AZ"
        },
        "type": "nin_facial",
        "task_created_by": "Chinook Devops"
    },
    "message": "Successful",
    "status_code": 200
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

#### NIN Test Data

ID Number: 11111111111

DOB: 1988-04-04

FN: Sarah

MN: Jane

LN: Doe

### Nigerian International Passport with Facial Match (Passport Facial)

This endpoint allows you to verify a Passport ID with a Facial match.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": {
    "report_type": "identity",
    "type": "passport_facial",
    "reference": "Axxxxxxxxx",
    "image": "{{base64 image}}",
    "subject_consent": true
  }
}
```

Successful response:

```json
{
    "data": {
        "id": "reports_55c130dc-62a5-4603-849b-15fad5095ea8",
        "reference_id": "6051334d658d1",
        "response": {
            "first_name": "JOHN",
            "last_name": "DOE",
            "middle_name": "MICHAEL",
            "dob": "1994-10-11",
            "mobile": null,
            "photo": "/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAIBAQIBAQICAgICAgICAwUDAwMDAwYEBAMFBwYHBwcGBwcICQsJCAgKCAcHCg0KCgsMDAwMBwkODw0MDgsMDAz/2wBDAQICAgMDAwYDAwYMCAcIDAw//Z",
            "face_details": {
                "confidence": 97.39,
                "threshold": 70,
                "request_image": "/9j/4AAQSkZJRgABAQEAkACQAAD/4QDARXhpZgAASUkqAAgAAAAFABoBBQABAAAASgAAABsBBQABAAAAUgAAACgBAwABAAAAAgAAADEBAgALAAAAWgAAAGmHBAABAAAAZgAAAAAAAACQAAAAAQAAAJAAAAABAAAAUGhvdG9TY2FwZQAABACGkgcAHAAAAJwAAAABoAMAA//Z"
            },
            "gender": "Male",
            "issued_at": "ABUJA",
            "issued_date": "2020-04-02",
            "expiry_date": "2025-03-02",
            "reference_id": "Axxxxxxxx"
        },
        "type": "passport_facial",
        "task_created_by": "Chinook Devops"
    },
    "message": "Successful",
    "status_code": 200
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ],
        "image": [
            "The image field is required."
        ]
    },
    "status_code": 422
}
```

#### NIP Test Data

ID Number: A11111111

DOB: 1988-04-04

FN: Sarah

MN: Jane

LN: Doe

### Tax Identification Number (TIN)

This endpoint allows you to verify a Tax dentification number

Request sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/candidates/check",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": {
    "report_type": "identity",
    "type": "tin",
    "reference": "00000000-0001",
    "subject_consent": true
  }
}
```

Successful response:

```json
{
    "data": {
        "id": "reports_1d63b3ce-38f7-4eb4-8759-539292f2ca7d",
        "reference_id": "xxxxxxxxxx",
        "response": {
            "full_name": "xxxxxxxxxxxxxxxxxxxxx",
            "tax_identification_number": "00000000-0001",
            "verified": true
        },
        "type": "tin",
        "task_created_by": "Chinook Devops"
    },
    "message": "Successful",
    "status_code": 200
}
```

Failed response:

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "reference": [
            "The reference field is required."
        ]
    },
    "status_code": 422
}
```

### Bank Account Verification

This endpoint allows you verify a bank account.

To generate the list of Banks.

Request sample

```json http
{
  "method": "get",
  "url": "https://api.staging.youverify.co/v1/identities/banks",
  "headers": {
    "Token": "{{token}}"
  }
}
```

To verify bank account.

Request sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/identities/banks/verify_account",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": {
    "account_number": "0111101011",
    "bank_code": "058",
    "subject_consent": true
  }
}
```

Successful response:

```json
{
    "data": {
        "id": "reports_efd61da7-94cd-b1e7-ea3585a6158a",
        "reference_id": "5fb17b1d00083",
        "subject_consent": true,
        "candidate": {
            "id": "0da849a9-e6b3-9c19-25e8c0d7a878",
            "reference_id": "YV5fb17b1d092492817",
            "full_name": "John Michael Doe",
            "bank_name": "xxxxxx Bank",
            "account_number": "xxxxxxxxx",
            "bank_code": "058"
        },
        "status": "completed",
        "identity_status": "VERIFIED",
        "identity_number": "xxxxxxxxx",
        "package": "identity",
        "package_name": "Identity",
        "type": "bank_account_verification",
        "business": "Youcheck Online Services Limited",
        "task_created_by": "Inc Youverify",
        "end_time": "2020-11-15",
        "created_at": "2020-11-15 20:01:49",
        "images": {
            "data": []
        }
    },
    "message": "Successful",
    "status_code": 200
}
```

Failed response

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "account_number": [
            "The account number must be 10 digits."
        ]
    },
    "status_code": 422
}
```

## Company Search (CAC)

This endpoint allows you to search for registered companies.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/backgrounds/cac",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": {
	"company_name":"Youcheck Online Services Ltd"
}
}
```

Successful response:

```json
{
    "data": {
        "id": "reports_7918e7f5-6015-41f0-b34c-a57055fbe98b",
        "reference_id": "60280583a4f12",
        "start_time": "2021-04-27",
        "end_time": "2021-04-27",
        "execution_date": "",
        "submitted_at": "",
        "status": "completed",
        "task_status": "PENDING",
        "reason": "",
        "task_created_by": "xxxxxxxxxxxxxxx",
        "package": "company_check",
        "download_url": "http://127.0.0.1:8000/v1/reports/reports_7918e7f5-6015-41a0-b34c-a58055ebe08b/download/pdf",
        "description": "",
        "package_name": "Company Verification",
        "details": {
            "id": 30,
            "uuid": "background-745b42fd-5975-4863-9f12-e0090c7fe773",
            "background_type": "cac",
            "background_id": 42,
            "search_id": "RC 1418005",
            "user_id": "35",
            "model_id": "1",
            "model_type": "partners",
            "status": "completed",
            "reason_for_fail": null,
            "deleted_at": null,
            "created_at": "2021-04-27 13:37:23",
            "updated_at": "2021-04-27 13:37:23",
            "background_model": {
                "uuid": "cac-eff922ca-061d-4cc7-956f-ec5d6b03b406",
                "task_id": "60880583b126ce1c8acbea62",
                "search_type": "manual",
                "status": "VERIFIED",
                "name_of_company": "YOUCHECK ONLINE SERVICES LTD",
                "data": {
                    "message": "Success",
                    "data": {
                        "_id": "60880583b126ce1c8acbea62",
                        "name": "YOUCHECK ONLINE SERVICES LTD",
                        "status": "Unknown",
                        "activity": "Information service activities",
                        "registrationNumber": "RC 1418005",
                        "registrationDate": "09 Jun 2017",
                        "address": "13B BISHOP STREET,  OFF COKER ROAD,  ILUPEJU,  LAGOS STATE",
                        "state": "LAGOS",
                        "lga": "KOSOFE",
                        "city": "LAGOS",
                        "phoneNumber": "",
                        "websiteEmail": "xxxxxxxxxxxxxxxxxx",
                        "branchAddress": "",
                        "headOfficeAddress": "",
                        "objectives": "",
                        "createdAt": "2021-04-27T12:37:23.447Z",
                        "updatedAt": "2021-04-27T12:37:23.447Z",
                        "__v": 0
                    }
                },
                "registration_number": "RC 1418005",
                "found_company_name": null,
                "date_of_change_of_name": null,
                "memorandum_of_association_url": null,
                "additional_comments": null,
                "deleted_at": null,
                "created_at": "2021-04-27 13:37:23",
                "updated_at": "2021-04-27 13:37:23"
            }
        },
        "has_address": false,
        "reportable_id": "background-735b42fd-5975-4863-9f12-e0095c7fe773",
        "last_updated_at": "2021-04-27 13:37:23",
        "can_view_report": true,
        "business": "Youverify Chinook",
        "created_at": "2021-04-27 13:37:23",
        "images": {
            "data": []
        }
    },
    "message": "Successful",
    "status_code": 200
}
```

Failed response:

```json
{
    "message": "No result found",
    "code": 404,
    "status_code": 400
}
```


## Address Verification API's

There are three types of address verification; 

1.  Individual Address verification - Individual Address check 
2.  Reference Address Verification - Individual Guarantor's Address Check 
3.  Business Address Verification

Steps to request for an address verification:

### 1. Create Candidate

This endpoint creates a candidate.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/candidates",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"first_name\": \"\" [required], \n \"middle_name\": \"\"[optional] , \n \"last_name\": \"\" [required], \n \"gender\": \"\" [optional], \n \"dob\": \"\" [optional], \n \"email\": \"\" [required if mobile is not set], \n \"mobile\": \"\" [required if email is not set], \n \"country\": \"Nigeria\", \n \"mothers_maiden_name\": \"\",[optional] \n \"previous_last_name\": \"\",[optional] \n \"nationality\": \"\",[optional] \n \"country_of_birth\": \"\",[optional] \n \"town_of_birth\": \"\"[optional] \n}"
}
```

**Note**: All optional keys should not be sent if they are not filled

Response

```json
{ 
"data": { 
"id": "bad42b9e-84f3-4274-b790-7960d532ccaa", 
"reference_id": "YV5d7b6f05bc3e8", 
"name": "Femi Akeem", 
"first_name": "Akeem", 
"middle_name": "", 
"last_name": "Femi", 
"gender": "male", 
"dob": "1995-09-09", 
"mobile": "08012345678", 
"email": "email@gmail.com", 
"country": "Nigeria", 
"has_live_photo": false, 
"live_photo_path": null, 
"mothers_maiden_name": "Ifeoluwa", 
"previous_last_name": "", 
"nationality": "Nigeria", 
"country_of_birth": "Nigeria", 
"town_of_birth": "Ilorin", 
"href": "/candidates/bad42b9e-84f3-4274-b790-7960d532ccaa", 
"has_reports": false, 
"id_numbers": [], 
"created_at": "2019-09-13 11:27:17" 
}, 
"message": "Successful", 
"status_code": 200 
}
```

### 2. Request for Address Verification using the candidate_id

#### A. Individual Address Verification - Individual Address Check

This endpoint initiates an address verification.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/candidates/{candidate_id}/live_photo",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"description\": \"Address Description\", [optional] \n \"address\": \n { \n  \"flat_number\": \" \", [optional] \n  \"building_name\": \" \", [optional] \n  \"building_number\": \" \", [required] \n  \"street\": \" \",[required] \n  \"sub_street\": \" \", [optional] \n  \"landmark\": \" \", [required] \n  \"state\":\" \", [required] \n  \"city\": \" \", [required] \n  \"postcode\": \" \", [optional] \n  \"country\": \"Nigeria\" [required] \n  }, \n \"images\": [\"base64 encoded image/logo or url of image/logo\"][required] \n}"
}
```

Response

```json
{ 
    "data": { 
    "id": "reports_f313d22a-4c39-4015-aa00-30e55c54296b", 
    "reference_id": "5d7b7dd40b39c", 
    "candidate": { 
    "id": "b54b401f-5487-49d7-ad1c-7fdd50786fc7", 
    "reference_id": "YV5d7b7da4e5b57", 
    "name": "Femi Akeem", 
    "first_name": "Akeem", 
    "last_name": "Femi", 
    "middle_name": "", 
    "email": "email@gmail.com", 
    "mobile": "08012345678", 
    "has_live_photo": true, 
    "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2019-09-13/photo_5d7b7dd35b1895416.jpeg" 
    }, 
    "start_time": "2019-09-13", 
    "end_time": "2019-09-13", 
    "execution_date": "", 
    "submitted_at": "", 
    "completed_at": null, 
    "accepted_at": null, 
    "revalidation_date": "2019-12-13", 
    "status": "unassigned", 
    "task_status": "PENDING", 
    "reason": null, 
    "task_created_by": "Chinook Devops", 
    "package": "live_photo", 
    "download_url": null, 
    "description": "", 
    "package_name": "Live Photo Address Verification",
    "details": 
    { 
        "uuid": "95aed5b5-b208-499b-8acf-234eb9320ffd", 
        "address_id": 3674, 
        "candidate_id": 5551, 
        "photo_url": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2019-09-13/photo_5d7b7dd35b1895416.jpeg", 
        "status": "PENDING", 
        "reason_for_fail": null, 
        "deleted_at": null, 
        "created_at": "2019-09-13 12:30:27", 
        "updated_at": "2019-09-13 12:30:27", 
        "images": [ 
        { 
            "id": 3308, 
            "uuid": "273c1410-8fb4-4872-a88f-65ed8f5aff9d", 
            "live_photo_id": 3307, 
            "candidate_id": 5551, 
            "image_type": "image/jpeg", 
            "image_extension": "jpeg", 
            "path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2019-09-13/photo_5d7b7dd35b1895416.jpeg", 
            "image_name": "photo_5d7b7dd35808b1132.jpeg", 
            "deleted_at": null, 
            "created_at": "2019-09-13 12:30:27", 
            "updated_at": "2019-09-13 12:30:27", 
            "image_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2019-09-13/photo_5d7b7dd35b1895416.jpeg" 
            } 
                }, 
                "address": { 
                "uuid": "377058b1-ed06-47e5-9d5e-ee3ac094f50b",
                "user_id": 1, 
                "user_type": "user", 
                "candidate_id": 5551, 
                "flat_number": "5", 
                "building_name": "White Building", 
                "building_number": "13", 
                "sub_street": "Bishop", 
                "street": "Bishop Street", 
                "landmark": "Opposit Ilupeju Police station", 
                "state": "Lagos", 
                "city": "Ilupeju", 
                "post_code": null, 
                "country": "Nigeria", 
                "longitude": "3.359873", 
                "latitude": "6.5524201", 
                "what3words": "LAMH-42998", 
                "what3words_map": "https://address.gov.ng/Home/address/LAMH-42998", 
                "agent_geo": null, 
                "start_date": "", 
                "end_date": "", 
                "status": "PENDING", 
                "reason_for_fail": null, 
                "item_id": "0", 
                "item_type": "live_photo",
                "created_at": "2019-09-13 12:30:27", 
                "updated_at": "2019-09-13 12:30:27", 
                "formatted": "Flat Number 5, White Building, 13, Sub Streetbishop, Bishop Street, Ilupeju, Lagos, Nigeria, ", 
                "map_format": "13 Bishop Street, Ilupeju , Lagos, Nigeria", 
                "map_address_url": null, 
                "map_geolocation_url": null 
                ], 
                    "live_photos": { 
                    "photo_url": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2019-09-13/photo_5d7b7dd35b1895416.jpeg" 
                    } 
                }, 
                "has_address": true, 
                "notes": [], 
                "signature": [], 
                "is_flagged": 0, 
                "reportable_id": "95aed5b5-b208-499b-8acf-234eb9320ffd", 
                "created_at": "2019-09-13 12:30:28", 
                "last_updated_at": "2019-09-13 12:30:52", 
                "what3words": null, 
                "what3words_map_link": null, 
                "digital_address_code": null, 
                "digital_address_url": null, 
                "map_address_url": null, 
                "map_geolocation_url": null, 
                "report_geolocation_url": null, 
                "report_longitude": null, 
                "report_latitude": null, 
                "can_view_report": true, 
                "business": "Youverify", 
                "reasons_for_failure": [ 
                "Address does not exist", 
                "Address not accessible", 
                "Candidate does not live there" 
                ], 
            "submission_distance_in_meters": 0, 
            "images": { 
            "data": [] 
        } 
    }, 
    "message": "Successful", 
    "status_code": 200 
}
```

#### B. Reference Address Verification - Guarantors Address Check

This endpoint initiates a Guarantors address verification.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/candidates/{candidate_id}/references",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{ \n \"notes\":\"\", \n \"reference\": { \"first_name\": \"\", [required] \n \"last_name\": \"\", [required] \"email\": \"\", [required] \n \"mobile\": \"\", [required] \n \"image\": [\"base64 encoded image/logo or url of image/logo\"] [required] \n }, \n \"address\": { \"flat_number\": \"\", [optional] \n \"building_name\": \"\", [optional] \n \"building_number\": \"\", [required] \n \"street\": \"\",[required] \n \"sub_street\": \"\", [optional] \n \"landmark\": \"\", [required] \n \"state\":\"\", [required] \n \"city\": \"\", [required] \n \"postcode\": \"\", [optional] \n \"country\": \"Nigeria\" [required] \n }, \n}"
}
```

Respond

```json
{
"data": {
"id": "reports_08ef00ba-38c9-4666-bd53-d440d48530c5",
"reference_id": "5d7b7f8bf3803",
"candidate": {
"id": "b54b401f-5487-49d7-ad1c-7fdd50786fc7",
"reference_id": "YV5d7b7da4e5b57",
"name": "Femi Akeem",
"first_name": "Akeem",
"last_name": "Femi",
"middle_name": "",
"email": "email@gmail.com",
"mobile": "07035038922",
"has_live_photo": true,
"live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2019-09-13/photo_5d7b7dd35b1895416.jpeg"
},
"start_time": "2019-09-13",
"end_time": "2019-09-13",
"execution_date": "",
"submitted_at": "",
"completed_at": null,
"accepted_at": null,
"revalidation_date": "2019-12-13",
"status": "unassigned",
"task_status": "PENDING",
"reason": null,
"task_created_by": "Chinook Devops",
"package": "reference_check",
"download_url": null,
"description": "",
"package_name": "Reference Check Address Verification",
"details": {
"uuid": "1aa44e38-6126-4906-9d37-553a10004012",
"address_id": 3678,
"first_name": "Tobi",
"last_name": "Adeyemi",
"email": "email@gmail.com",
"mobile": "",
"photo_url": null,
"status": "PENDING",
"reason_for_fail": null,
"created_at": "2019-09-13 12:37:47",
"updated_at": "2019-09-13 12:37:47",
"name": "Adeyemi Tobi",
"address": {
"uuid": "927d593b-f63e-4ec4-8cb9-68b88ca962c3",
"user_id": 1,
"user_type": "user",
"candidate_id": 5551,
"flat_number": "5",
"building_name": "White Building",
"building_number": "3",
"sub_street": "Bishop",
"street": "13B Bishop Street",
"landmark": "Opposit Ilupeju Police station",
"state": "Lagos",
"city": "Ilupeju",
"post_code": null,
"country": "Nigeria",
"longitude": "3.359796",
"latitude": "6.552381",
"what3words": "LAMH-42998",
"what3words_map": "https://address.gov.ng/Home/address/LAMH-42998",
"agent_geo": null,
"start_date": "2017-10-05",
"end_date": "2017-10-09",
"status": "PENDING",
"reason_for_fail": null,
"item_id": "0",
"item_type": "reference",
"created_at": "2019-09-13 12:37:46",
"updated_at": "2019-09-13 12:37:46",
"formatted": "Flat Number 5, White Building, 3, Sub Streetbishop, 13b Bishop Street, Ilupeju, Lagos, Nigeria, ",
"map_format": "3 13b Bishop Street, Ilupeju , Lagos, Nigeria",
"map_address_url": null,
"map_geolocation_url": null
},
"guarantor_image": "https://api.staging.youverify.co/uploads/tasks/livephoto/2019-09-13/photo5d7b7f8b25ddf2041.jpeg"
},
"has_address": true,
"notes": [],
"signature": [],
"is_flagged": 0,
"reportable_id": "1aa44e38-6126-4906-9d37-553a10004012",
"created_at": "2019-09-13 12:37:48",
"last_updated_at": "2019-09-13 12:38:05",
"what3words": null,
"what3words_map_link": null,
"digital_address_code": null,
"digital_address_url": null,
"map_address_url": null,
"map_geolocation_url": null,
"report_geolocation_url": null,
"report_longitude": null,
"report_latitude": null,
"can_view_report": true,
"business": "Youverify",
"reasons_for_failure": [
"Address does not exist",
"Address not accessible",
"Candidate does not live there"
],
"submission_distance_in_meters": 0,
"images": {
"data": []
}
},
"message": "Successful",
"status_code": 200
} 
```

#### C. Business Address Verification

This endpoint initiates a Business Address verification.

Request Sample

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/candidates/{candidate_id}/merchants",
  "headers": {
    "Content-Type": "application/json",
    "Token": "{{token}}"
  },
  "body": "{\n  \"merchant\": {\n    \"name\": \"Anthony\",\n    \"registration_number\": \"1530-03089-0393993\",\n    \"email\": \"anthony@gm.com\",\n    \"mobile\": \"09123449908\"\n  },\n  \"address\": {\n    \"flat_number\": \"\",\n    \"building_name\": \"\",\n    \"building_number\": \"13b\",[required]\n    \"landmark\": \"Ilupeju Police Station\",[required]\n    \"street\": \"Bishop street\",[required]\n    \"sub_street\": \"\",\n    \"digital_address_code\": \"\",\n    \"nipost_address\": \"\",\n    \"state\": \"Lagos\",[required]\n    \"city\": \"Ilupeju\",[required]\n    \"postcode\": \"\",\n    \"country\": \"Nigeria\"[required]\n  }\n}"
}
```

Response

```json
{
    "data": {
        "id": "reports_aaa5cfcf-bcd6-490b-994d-cf5936d4dee4",
        "reference_id": "5ed6f030c5409",
        "subject_consent": true,
        "candidate": {
            "id": "fb064007-7a8e-45c8-81c3-269b399740e9",
            "reference_id": "YV5ed65254796b68637",
            "name": "Doe John",
            "first_name": "John",
            "last_name": "Doe",
            "middle_name": "",
            "email": "john@email.com",
            "mobile": "07012312345",
            "has_live_photo": false,
            "live_photo_path": null
        },
        "start_time": "2020-06-03",
        "end_time": "2020-06-03",
        "execution_date": "",
        "submitted_at": "",
        "completed_at": null,
        "accepted_at": null,
        "revalidation_date": "2020-09-03",
        "status": "unassigned",
        "task_status": "PENDING",
        "reason": null,
        "task_created_by": "Chinook Devops",
        "package": "merchant_verification",
        "download_url": null,
        "description": "",
        "package_name": "Merchant Verification",
        "details": {
            "id": 49,
            "uuid": "2ec200a2-f66e-4ed5-b921-10f96a7cef49",
            "address_id": 4092,
            "candidate_id": 7025,
            "status": "PENDING",
            "registration_number": "1530-03089-0393993",
            "name": "Anthony",
            "email": "anthony@gm.com",
            "mobile": "09123449908",
            "telephone": "",
            "deleted_at": null,
            "created_at": "2020-06-03 01:34:56",
            "updated_at": "2020-06-03 01:34:56",
            "address": {
                "uuid": "efa06cd1-6c8d-4304-8f0f-a25d1186a9ee",
                "user_id": 1,
                "user_type": "user",
                "candidate_id": 7025,
                "flat_number": "",
                "building_name": "",
                "building_number": "13b",
                "sub_street": "",
                "street": "Bishop street",
                "landmark": "Ilupeju Police Station",
                "state": "lagos",
                "city": "Ilupeju",
                "post_code": null,
                "country": "Nigeria",
                "longitude": "3.3595358",
                "latitude": "6.5457033",
                "what3words": "LAMH-70950",
                "what3words_map": "https://address.gov.ng/Home/address/LAMH-70950",
                "agent_geo": null,
                "start_date": null,
                "end_date": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "item_id": "0",
                "item_type": "merchant_verification",
                "created_at": "2020-06-03 01:34:56",
                "updated_at": "2020-06-03 01:34:56",
                "formatted": "13b, Bishop  Street, Ilupeju Police Station, Ilupeju, Lagos, Nigeria, ",
                "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                "map_address_url": null,
                "map_geolocation_url": null
            }
        },
        "has_address": true,
        "notes": [],
        "signature": [],
        "is_flagged": 0,
        "awaiting_qa": false,
        "reportable_id": "2ec200a2-f66e-4ed5-b921-10f96a7cef49",
        "created_at": "2020-06-03 01:34:56",
        "last_updated_at": "2020-06-03 01:35:08",
        "what3words": null,
        "what3words_map_link": null,
        "digital_address_code": null,
        "digital_address_url": null,
        "map_address_url": null,
        "map_geolocation_url": null,
        "report_geolocation_url": null,
        "report_longitude": null,
        "report_latitude": null,
        "can_view_report": true,
        "business": "Youverify",
        "reasons_for_failure": [
            "Address does not exist",
            "Address not accessible",
            "Candidate does not live there"
        ],
        "submission_distance_in_meters": 0,
        "images": {
            "data": []
        }
    },
    "message": "Successful",
    "status_code": 200
}
```

## Reports

This endpoint gets all reports.

```json http
{
  "method": "get",
  "url": "https://api.staging.youverify.co/v1/reports",
  "headers": {
    "Token": "{{token}}"
  }
}
```

Response

```json
{
    "data": [
        {
            "id": "c9a75233-00ef-49ed-85fa-3ab6003e12b7",
            "reference_id": "5a0d94274096d",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-23",
            "end_time": "2018-03-26",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-26",
            "status": "completed",
            "task_status": "VERIFIED",
            "reason": null,
            "task_created_by": "",
            "package": "live_photo",
            "download_url": "https://api.staging.youverify.co/v1/reports/c9a75233-00ef-49ed-85fa-3ab6003e12b7/download/pdf",
            "description": null,
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "894654cc-a373-4ef5-b3b4-8a030fefac67",
                "address_id": 1,
                "candidate_id": 1,
                "photo_url": null,
                "status": "VERIFIED",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2017-11-16 14:35:34",
                "updated_at": "2017-11-16 14:50:59",
                "images": [
                    {
                        "id": 1,
                        "uuid": "a6b83226-3fd3-497c-9d2c-44f8a9db215b",
                        "live_photo_id": 1,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a0d94266d7a87447.jpeg",
                        "deleted_at": null,
                        "created_at": "2017-11-16 14:35:35",
                        "updated_at": "2017-11-16 14:35:35",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a0d94266d7a87447.jpeg"
                    }
                ],
                "address": {
                    "uuid": "f2a77feb-a500-42f5-aa64-124257cce3ce",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "1",
                    "building_name": "",
                    "building_number": "18",
                    "sub_street": "",
                    "street": "Ogati",
                    "landmark": "Fadeyi bus stop",
                    "state": "Lagos",
                    "city": "Somolu",
                    "post_code": "234001",
                    "country": "Nigeria",
                    "longitude": "3.369765",
                    "latitude": "6.5258024",
                    "what3words": "speeds.divided.book",
                    "what3words_map": "http://w3w.co/speeds.divided.book",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2017-11-16 14:35:34",
                    "updated_at": "2017-11-16 14:35:34",
                    "formatted": "Flat Number 1, 18, Ogati Street, Fadeyi Bus Stop, Somolu, Lagos, Nigeria, ",
                    "map_format": "18 Ogati, Somolu , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 1,
                        "uuid": "a6b83226-3fd3-497c-9d2c-44f8a9db215b",
                        "live_photo_id": 1,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a0d94266d7a87447.jpeg",
                        "deleted_at": null,
                        "created_at": "2017-11-16 14:35:35",
                        "updated_at": "2017-11-16 14:35:35",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a0d94266d7a87447.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [
                {
                    "id": 1,
                    "report_id": 1000,
                    "agent_id": 2,
                    "note": "Testing the report pdf",
                    "created_at": "2017-11-16 14:49:41",
                    "updated_at": "2017-11-16 14:49:41",
                    "formatted_time": "16 Nov, 2017 02:49:pm"
                },
                {
                    "id": 5,
                    "report_id": 1000,
                    "agent_id": 2,
                    "note": "This should be deleted have edited this note from partner portal",
                    "created_at": "2017-11-23 16:02:11",
                    "updated_at": "2017-11-23 16:02:46",
                    "formatted_time": "23 Nov, 2017 04:02:pm"
                },
                {
                    "id": 6,
                    "report_id": 1000,
                    "agent_id": 2,
                    "note": "Note for candidate",
                    "created_at": "2017-12-04 17:06:20",
                    "updated_at": "2017-12-04 17:06:20",
                    "formatted_time": "04 Dec, 2017 05:06:pm"
                },
                {
                    "id": 7,
                    "report_id": 1000,
                    "agent_id": 2,
                    "note": "This is a note.",
                    "created_at": "2017-12-04 17:08:05",
                    "updated_at": "2017-12-04 17:08:05",
                    "formatted_time": "04 Dec, 2017 05:08:pm"
                }
            ],
            "signature": [
                "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"
            ],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "894654cc-a373-4ef5-b3b4-8a030fefac67",
            "created_at": "2017-11-16 14:35:35",
            "last_updated_at": "2019-04-02 12:35:39",
            "what3words": "vibe.winters.gives",
            "what3words_map_link": "http://w3w.co/vibe.winters.gives",
            "digital_address_code": "vibe.winters.gives",
            "digital_address_url": "http://w3w.co/vibe.winters.gives",
            "map_address_url": "https://www.google.com/maps/search/?api=1&query=18+Ogati%2C+Somolu+%2C+Lagos%2C+Nigeria",
            "map_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524521, 3.3598646",
            "report_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524521, 3.3598646",
            "report_longitude": "3.3598646",
            "report_latitude": "6.5524521",
            "can_view_report": true,
            "business": null,
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 3158,
            "images": {
                "data": [
                    {
                        "id": 4,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1510847173905_98228.jpg",
                        "file_size": "13807",
                        "file_path": "uploads/reports/images/2017-11-16/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/original/1510847173905_98228.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/resize/1510847173905_98228.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/original/1510847173905_98228.jpg",
                        "h": 359,
                        "w": 640,
                        "resize_height": 224,
                        "resize_width": 400
                    },
                    {
                        "id": 6,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1510847376671_93652.jpg",
                        "file_size": "13390",
                        "file_path": "uploads/reports/images/2017-11-16/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/original/1510847376671_93652.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/resize/1510847376671_93652.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/original/1510847376671_93652.jpg",
                        "h": 359,
                        "w": 640,
                        "resize_height": 224,
                        "resize_width": 400
                    },
                    {
                        "id": 7,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1510849612249_91455.jpg",
                        "file_size": "46724",
                        "file_path": "uploads/reports/images/2017-11-16/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/original/1510849612249_91455.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/resize/1510849612249_91455.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-11-16/original/1510849612249_91455.jpg",
                        "h": 1138,
                        "w": 640,
                        "resize_height": 711,
                        "resize_width": 400
                    },
                    {
                        "id": 14,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1511447449149_80411.jpg",
                        "file_size": "46405",
                        "file_path": "uploads/reports/images/2017-11-23/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-23/original/1511447449149_80411.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-23/resize/1511447449149_80411.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-11-23/original/1511447449149_80411.jpg",
                        "h": 1138,
                        "w": 640,
                        "resize_height": 711,
                        "resize_width": 400
                    },
                    {
                        "id": 18,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1512403764578_12971.jpg",
                        "file_size": "14165",
                        "file_path": "uploads/reports/images/2017-12-04/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-12-04/original/1512403764578_12971.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-12-04/resize/1512403764578_12971.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-12-04/original/1512403764578_12971.jpg",
                        "h": 235,
                        "w": 360,
                        "resize_height": 261,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "c4b80a27-91d9-4c14-9e11-ebc9a4ee2410",
            "reference_id": "5a0efb99d3476",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "VERIFIED",
            "reason": null,
            "task_created_by": "",
            "package": "merchant_verification",
            "download_url": null,
            "description": null,
            "package_name": "Merchant Verification",
            "details": {
                "id": 1,
                "uuid": "0634947f-f06d-466d-86a7-e77c627a145c",
                "address_id": 3,
                "candidate_id": 1,
                "status": "VERIFIED",
                "registration_number": "12332234567",
                "name": "Safi.Ng",
                "email": null,
                "mobile": null,
                "telephone": null,
                "deleted_at": null,
                "created_at": "2017-11-17 16:09:13",
                "updated_at": "2017-11-17 16:48:51",
                "address": {
                    "uuid": "c61551f1-b9bd-4367-af95-c4479bd228be",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.3598313",
                    "latitude": "6.551594499999999",
                    "what3words": "outdone.sprain.times",
                    "what3words_map": "http://w3w.co/outdone.sprain.times",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "merchant_verification",
                    "created_at": "2017-11-17 16:09:13",
                    "updated_at": "2017-11-17 16:09:13",
                    "formatted": "13b, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                }
            },
            "has_address": true,
            "notes": [
                {
                    "id": 3,
                    "report_id": 1002,
                    "agent_id": 2,
                    "note": "Working on business verification",
                    "created_at": "2017-11-17 16:47:42",
                    "updated_at": "2017-11-17 16:47:42",
                    "formatted_time": "17 Nov, 2017 04:47:pm"
                }
            ],
            "signature": [
                "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"
            ],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "0634947f-f06d-466d-86a7-e77c627a145c",
            "created_at": "2017-11-17 16:09:13",
            "last_updated_at": "2019-04-04 10:25:03",
            "what3words": "vibe.winters.gives",
            "what3words_map_link": "http://w3w.co/vibe.winters.gives",
            "digital_address_code": "vibe.winters.gives",
            "digital_address_url": "http://w3w.co/vibe.winters.gives",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": "3.3598589",
            "report_latitude": "6.5524545",
            "can_view_report": true,
            "business": null,
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 95,
            "images": {
                "data": [
                    {
                        "id": 12,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1510933700268_79580.jpg",
                        "file_size": "33665",
                        "file_path": "uploads/reports/images/2017-11-17/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-17/original/1510933700268_79580.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-17/resize/1510933700268_79580.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-11-17/original/1510933700268_79580.jpg",
                        "h": 852,
                        "w": 640,
                        "resize_height": 533,
                        "resize_width": 400
                    },
                    {
                        "id": 13,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1510933722625_89696.jpg",
                        "file_size": "20964",
                        "file_path": "uploads/reports/images/2017-11-17/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-17/original/1510933722625_89696.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2017-11-17/resize/1510933722625_89696.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2017-11-17/original/1510933722625_89696.jpg",
                        "h": 359,
                        "w": 640,
                        "resize_height": 224,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "4196e38b-8b83-4394-8143-9907fe718cf5",
            "reference_id": "5a3ad34cba34c",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "merchant_verification",
            "download_url": null,
            "description": "",
            "package_name": "Merchant Verification",
            "details": {
                "id": 2,
                "uuid": "87421dd5-7e74-4c95-a011-c60a8e725731",
                "address_id": 70,
                "candidate_id": 1,
                "status": "PENDING",
                "registration_number": "121223343221",
                "name": "Safi",
                "email": null,
                "mobile": null,
                "telephone": null,
                "deleted_at": null,
                "created_at": "2017-12-20 22:17:00",
                "updated_at": "2017-12-20 22:17:00",
                "address": {
                    "uuid": "0b97cfaa-54cf-47f5-8101-9f41fd5d42dc",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "18",
                    "sub_street": "",
                    "street": "Ogati street",
                    "landmark": "",
                    "state": "Lagos",
                    "city": "Somolu",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.3700493",
                    "latitude": "6.5260282",
                    "what3words": "weep.nursery.boarded",
                    "what3words_map": "http://w3w.co/weep.nursery.boarded",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "merchant_verification",
                    "created_at": "2017-12-20 22:17:00",
                    "updated_at": "2017-12-20 22:17:00",
                    "formatted": "18, Ogati  Street, Somolu, Lagos, Nigeria, ",
                    "map_format": "18 Ogati Street, Somolu , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                }
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "87421dd5-7e74-4c95-a011-c60a8e725731",
            "created_at": "2017-12-20 22:17:00",
            "last_updated_at": "2019-04-12 06:00:18",
            "what3words": "NULL",
            "what3words_map_link": "NULL",
            "digital_address_code": "NULL",
            "digital_address_url": "NULL",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "8585a00e-eb33-41b5-96a5-7d86b53c81be",
            "reference_id": "5a69cca63790e",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-23",
            "end_time": "2018-03-26",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-26",
            "status": "completed",
            "task_status": "VERIFIED",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "merchant_verification",
            "download_url": "https://api.staging.youverify.co/v1/reports/8585a00e-eb33-41b5-96a5-7d86b53c81be/download/pdf",
            "description": "Pls verify Jumia before next tomorrow",
            "package_name": "Merchant Verification",
            "details": {
                "id": 3,
                "uuid": "52ddebbe-b896-41ea-a044-d098ef936752",
                "address_id": 71,
                "candidate_id": 1,
                "status": "VERIFIED",
                "registration_number": "12121224893765",
                "name": "Jumia Nig Ltd",
                "email": null,
                "mobile": null,
                "telephone": null,
                "deleted_at": null,
                "created_at": "2018-01-25 13:25:10",
                "updated_at": "2018-01-25 13:27:24",
                "address": {
                    "uuid": "1a488f8b-85a7-43ff-a168-d517d20bfe6b",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "Police station",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.359796",
                    "latitude": "6.552381",
                    "what3words": "skewed.rigid.craters",
                    "what3words_map": "http://w3w.co/skewed.rigid.craters",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "merchant_verification",
                    "created_at": "2018-01-25 13:25:10",
                    "updated_at": "2018-01-25 13:25:10",
                    "formatted": "13b, Bishop  Street, Police Station, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                }
            },
            "has_address": true,
            "notes": [
                {
                    "id": 8,
                    "report_id": 1058,
                    "agent_id": 2,
                    "note": "Jumia exists",
                    "created_at": "2018-01-25 13:26:05",
                    "updated_at": "2018-01-25 13:26:05",
                    "formatted_time": "25 Jan, 2018 01:26:pm"
                },
                {
                    "id": 9,
                    "report_id": 1058,
                    "agent_id": 2,
                    "note": "Also testing notes",
                    "created_at": "2018-01-25 13:26:14",
                    "updated_at": "2018-01-25 13:26:14",
                    "formatted_time": "25 Jan, 2018 01:26:pm"
                }
            ],
            "signature": [
                "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"
            ],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "52ddebbe-b896-41ea-a044-d098ef936752",
            "created_at": "2018-01-25 13:25:10",
            "last_updated_at": "2019-04-02 12:35:47",
            "what3words": "divides.canine.button",
            "what3words_map_link": "http://w3w.co/divides.canine.button",
            "digital_address_code": "divides.canine.button",
            "digital_address_url": "http://w3w.co/divides.canine.button",
            "map_address_url": "https://www.google.com/maps/search/?api=1&query=13b+Bishop+Street%2C+Ilupeju+%2C+Lagos%2C+Nigeria",
            "map_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524406, 3.3598398",
            "report_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524406, 3.3598398",
            "report_longitude": "3.3598398",
            "report_latitude": "6.5524406",
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 8,
            "images": {
                "data": [
                    {
                        "id": 20,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1516883225281_49369.jpg",
                        "file_size": "47963",
                        "file_path": "uploads/reports/images/2018-01-25/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-01-25/original/1516883225281_49369.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-01-25/resize/1516883225281_49369.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-01-25/original/1516883225281_49369.jpg",
                        "h": 1137,
                        "w": 640,
                        "resize_height": 711,
                        "resize_width": 400
                    },
                    {
                        "id": 21,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1516883237647_87842.jpg",
                        "file_size": "13213",
                        "file_path": "uploads/reports/images/2018-01-25/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-01-25/original/1516883237647_87842.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-01-25/resize/1516883237647_87842.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-01-25/original/1516883237647_87842.jpg",
                        "h": 360,
                        "w": 640,
                        "resize_height": 225,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "b084448d-0cdd-4059-8c3a-f0bf3ad2d37d",
            "reference_id": "5a79ba9823e31",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "6e9fc223-9ea4-472a-8d56-2e18248f3330",
                "address_id": 72,
                "candidate_id": 1,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-06 15:24:24",
                "updated_at": "2018-02-06 15:24:24",
                "images": [
                    {
                        "id": 30,
                        "uuid": "677b52b7-875f-4eeb-b7bc-9817fde8fcfd",
                        "live_photo_id": 32,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79ba980ec302885.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 15:24:24",
                        "updated_at": "2018-02-06 15:24:24",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79ba980ec302885.jpeg"
                    }
                ],
                "address": {
                    "uuid": "92cc5c9d-ec88-4abb-af56-f8b1d9e4d846",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13b",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "Police station",
                    "state": "Lago",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "",
                    "longitude": "3.359693",
                    "latitude": "6.551221399999999",
                    "what3words": "weeded.bucket.likes",
                    "what3words_map": "http://w3w.co/weeded.bucket.likes",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-06 15:24:24",
                    "updated_at": "2018-02-06 15:24:24",
                    "formatted": "13b, Bishop  Street, Police Station, Ilupeju, Lago, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lago, ",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 30,
                        "uuid": "677b52b7-875f-4eeb-b7bc-9817fde8fcfd",
                        "live_photo_id": 32,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79ba980ec302885.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 15:24:24",
                        "updated_at": "2018-02-06 15:24:24",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79ba980ec302885.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "6e9fc223-9ea4-472a-8d56-2e18248f3330",
            "created_at": "2018-02-06 15:24:24",
            "last_updated_at": "2019-04-12 06:00:19",
            "what3words": "NULL",
            "what3words_map_link": "NULL",
            "digital_address_code": "NULL",
            "digital_address_url": "NULL",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": "3.3702266",
            "report_latitude": "6.5256041",
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 3077,
            "images": {
                "data": []
            }
        },
        {
            "id": "7fbf8e7a-ea16-4243-8520-547ea0dd058a",
            "reference_id": "5a79baf8b37be",
            "subject_consent": true,
            "candidate": {
                "id": "6d3760b3-be8d-4238-8473-aa6304f5d55f",
                "reference_id": "YV5a79baf481109",
                "name": "Olumide Naomi",
                "first_name": "Naomi",
                "last_name": "Olumide",
                "middle_name": "",
                "email": "olumide@naomi.com",
                "mobile": "09087654678",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79baf8980f32052.jpeg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "completed",
            "task_status": "VERIFIED",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": "https://api.staging.youverify.co/v1/reports/7fbf8e7a-ea16-4243-8520-547ea0dd058a/download/pdf",
            "description": "",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "45c74c68-d562-4153-9e6b-51dff9598002",
                "address_id": 73,
                "candidate_id": 16,
                "photo_url": null,
                "status": "VERIFIED",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-06 15:26:00",
                "updated_at": "2018-02-06 16:37:36",
                "images": [
                    {
                        "id": 31,
                        "uuid": "261e3e33-57fc-4a39-b5f2-9cfe43ac9043",
                        "live_photo_id": 33,
                        "candidate_id": 16,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79baf8980f32052.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 15:26:00",
                        "updated_at": "2018-02-06 15:26:00",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79baf8980f32052.jpeg"
                    }
                ],
                "address": {
                    "uuid": "45d4397b-42ed-4449-aec5-54783b24a34c",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 16,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "Police station",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.359796",
                    "latitude": "6.552381",
                    "what3words": "skewed.rigid.craters",
                    "what3words_map": "http://w3w.co/skewed.rigid.craters",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-06 15:26:00",
                    "updated_at": "2018-02-06 15:26:00",
                    "formatted": "13b, Bishop  Street, Police Station, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 31,
                        "uuid": "261e3e33-57fc-4a39-b5f2-9cfe43ac9043",
                        "live_photo_id": 33,
                        "candidate_id": 16,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79baf8980f32052.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 15:26:00",
                        "updated_at": "2018-02-06 15:26:00",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79baf8980f32052.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [
                {
                    "id": 10,
                    "report_id": 1060,
                    "agent_id": 2,
                    "note": "Am testing before presenting",
                    "created_at": "2018-02-06 16:34:22",
                    "updated_at": "2018-02-06 16:34:22",
                    "formatted_time": "06 Feb, 2018 04:34:pm"
                },
                {
                    "id": 11,
                    "report_id": 1060,
                    "agent_id": 2,
                    "note": "Did a great work",
                    "created_at": "2018-02-06 16:34:52",
                    "updated_at": "2018-02-06 16:34:52",
                    "formatted_time": "06 Feb, 2018 04:34:pm"
                },
                {
                    "id": 12,
                    "report_id": 1060,
                    "agent_id": 2,
                    "note": "Last note here",
                    "created_at": "2018-02-06 16:35:05",
                    "updated_at": "2018-02-06 16:35:05",
                    "formatted_time": "06 Feb, 2018 04:35:pm"
                }
            ],
            "signature": [
                "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"
            ],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "45c74c68-d562-4153-9e6b-51dff9598002",
            "created_at": "2018-02-06 15:26:00",
            "last_updated_at": "2019-04-02 12:35:48",
            "what3words": "torched.inkjet.securing",
            "what3words_map_link": "http://w3w.co/torched.inkjet.securing",
            "digital_address_code": "torched.inkjet.securing",
            "digital_address_url": "http://w3w.co/torched.inkjet.securing",
            "map_address_url": "https://www.google.com/maps/search/?api=1&query=13b+Bishop+Street%2C+Ilupeju+%2C+Lagos%2C+Nigeria",
            "map_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524035, 3.3599051",
            "report_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524035, 3.3599051",
            "report_longitude": "3.3599051",
            "report_latitude": "6.5524035",
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 12,
            "images": {
                "data": [
                    {
                        "id": 22,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1517931375532_82975.jpg",
                        "file_size": "29217",
                        "file_path": "uploads/reports/images/2018-02-06/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-06/original/1517931375532_82975.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-06/resize/1517931375532_82975.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-02-06/original/1517931375532_82975.jpg",
                        "h": 1137,
                        "w": 640,
                        "resize_height": 711,
                        "resize_width": 400
                    },
                    {
                        "id": 23,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1517931395542_64886.jpg",
                        "file_size": "19601",
                        "file_path": "uploads/reports/images/2018-02-06/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-06/original/1517931395542_64886.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-06/resize/1517931395542_64886.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-02-06/original/1517931395542_64886.jpg",
                        "h": 1137,
                        "w": 640,
                        "resize_height": 711,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "f92d75b1-6d62-4d6f-a578-5197dae71c88",
            "reference_id": "5a79e62b02eec",
            "subject_consent": true,
            "candidate": {
                "id": "9e9f9b7f-89b1-49b0-9bdf-4412cda1f66b",
                "reference_id": "YV5a79e6289cc9b",
                "name": "Muhammadu Gana Abdullahi",
                "first_name": "ABDULLAHI",
                "last_name": "MUHAMMADU",
                "middle_name": "GANA",
                "email": "defenders@nscdc.gov.ng",
                "mobile": "080992299281",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79e62ae90b48804.jpeg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "Civil defense task",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "586f76a3-824b-4150-b510-71be6333d7c4",
                "address_id": 74,
                "candidate_id": 17,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-06 18:30:18",
                "updated_at": "2018-02-06 18:30:18",
                "images": [
                    {
                        "id": 32,
                        "uuid": "ead5479a-ad3f-47a7-a9b9-d817bdc1d88e",
                        "live_photo_id": 34,
                        "candidate_id": 17,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79e62ae90b48804.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 18:30:19",
                        "updated_at": "2018-02-06 18:30:19",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79e62ae90b48804.jpeg"
                    }
                ],
                "address": {
                    "uuid": "7a1c38a8-3494-4d8a-a31d-72178b6475b9",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 17,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "Plot 420",
                    "sub_street": "Off Aguiyi Ironsi Street",
                    "street": "Tigris Crescent",
                    "landmark": "",
                    "state": "ABuja",
                    "city": "Maitama",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "7.493583699999999",
                    "latitude": "9.0818094",
                    "what3words": "privately.commitments.switchboards",
                    "what3words_map": "http://w3w.co/privately.commitments.switchboards",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-06 18:30:18",
                    "updated_at": "2018-02-06 18:30:18",
                    "formatted": "Plot 420, Sub Street Off Aguiyi Ironsi Street, Tigris Crescent Street, Maitama, Abuja, Nigeria, ",
                    "map_format": "Plot 420 Tigris Crescent, Maitama , Abuja, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 32,
                        "uuid": "ead5479a-ad3f-47a7-a9b9-d817bdc1d88e",
                        "live_photo_id": 34,
                        "candidate_id": 17,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79e62ae90b48804.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 18:30:19",
                        "updated_at": "2018-02-06 18:30:19",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79e62ae90b48804.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [
                {
                    "id": 13,
                    "report_id": 1061,
                    "agent_id": 4,
                    "note": "Yes , he lives there. \nHis name is mr Bakari",
                    "created_at": "2018-02-07 12:48:33",
                    "updated_at": "2018-02-07 12:48:33",
                    "formatted_time": "07 Feb, 2018 12:48:pm"
                }
            ],
            "signature": [
                "iVBORw0KGgoAAAANSUhEUgAAASwAAAFsCAYAAAB2JYQZAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAgAElEQVR4nO3deVgT1/4/8A/KoiCLFveKUvcNsa6oaItoXXptr2253uvWVlvtYhe1frXFtvS6W7Fiq6XWx61qrV1cuRYtbbEX3KuiuIBWEBQERCCQEJKc3x/+mJvJJCHLJOHA+/U8eZ7MZObMSWTenpmcnOPGGGMEAMCBBq6uAACApRBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHADgQUA3EBgAQA3EFgAwA0EFgBwA4EFANxAYAEANxBYAMANBBYAcAOBBQDcQGABADcQWADADQQWAHAD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"
            ],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "586f76a3-824b-4150-b510-71be6333d7c4",
            "created_at": "2018-02-06 18:30:19",
            "last_updated_at": "2019-04-12 06:00:20",
            "what3words": "NULL",
            "what3words_map_link": "NULL",
            "digital_address_code": "NULL",
            "digital_address_url": "NULL",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": [
                    {
                        "id": 25,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1518004026238_61237.jpg",
                        "file_size": "613161",
                        "file_path": "uploads/reports/images/2018-02-07/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-07/original/1518004026238_61237.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-07/resize/1518004026238_61237.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-02-07/original/1518004026238_61237.jpg",
                        "h": 3264,
                        "w": 2448,
                        "resize_height": 533,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "99cb85e1-1fe1-4aad-a41d-6b0a69996d64",
            "reference_id": "5a79e9b5350d9",
            "subject_consent": true,
            "candidate": {
                "id": "f09b0524-6cda-4421-bd51-cb630350b921",
                "reference_id": "YV5a79e9b2e17bf",
                "name": "Mohammed Abdul Hakeem",
                "first_name": "HAKEEM",
                "last_name": "MOHAMMED",
                "middle_name": "ABDUL",
                "email": "cservice@cac.gov.ng",
                "mobile": "080111123458",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79e9b52b86e2592.jpeg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "CaC task",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "cfdab22e-bad4-4d42-8428-727eb745c544",
                "address_id": 75,
                "candidate_id": 18,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-06 18:45:25",
                "updated_at": "2018-02-06 18:45:25",
                "images": [
                    {
                        "id": 33,
                        "uuid": "cc541650-1aff-4425-8497-93414e2eac50",
                        "live_photo_id": 35,
                        "candidate_id": 18,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79e9b52b86e2592.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 18:45:25",
                        "updated_at": "2018-02-06 18:45:25",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79e9b52b86e2592.jpeg"
                    }
                ],
                "address": {
                    "uuid": "d1379da5-08dd-4036-9b83-18b8c6d86252",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 18,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "Plot 666",
                    "sub_street": "ff Aguiyi Ironsi Street,",
                    "street": "Tigris Crescent,",
                    "landmark": "CAC Building",
                    "state": "Abuja",
                    "city": "Maitama",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "7.4926056",
                    "latitude": "9.0822529",
                    "what3words": "idiomatic.thinning.slant",
                    "what3words_map": "http://w3w.co/idiomatic.thinning.slant",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-06 18:45:25",
                    "updated_at": "2018-02-06 18:45:25",
                    "formatted": "Plot 666, Sub Street Ff Aguiyi Ironsi Street,, Tigris Crescent, Street, Cac Building, Maitama, Abuja, Nigeria, ",
                    "map_format": "Plot 666 Tigris Crescent,, Maitama , Abuja, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 33,
                        "uuid": "cc541650-1aff-4425-8497-93414e2eac50",
                        "live_photo_id": 35,
                        "candidate_id": 18,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a79e9b52b86e2592.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-06 18:45:25",
                        "updated_at": "2018-02-06 18:45:25",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a79e9b52b86e2592.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "cfdab22e-bad4-4d42-8428-727eb745c544",
            "created_at": "2018-02-06 18:45:25",
            "last_updated_at": "2019-04-12 06:00:21",
            "what3words": "NULL",
            "what3words_map_link": "NULL",
            "digital_address_code": "NULL",
            "digital_address_url": "NULL",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "fcf9051e-01ba-46a5-9859-4fc89c5b1a39",
            "reference_id": "5a7d77e5aa042",
            "subject_consent": true,
            "candidate": {
                "id": "cb9e3e62-573e-43d3-85e2-455bfe1c87a0",
                "reference_id": "YV5a7d77da9ea01",
                "name": "Haruna Hassan Bakuri",
                "first_name": "Bakuri",
                "last_name": "Haruna",
                "middle_name": "Hassan",
                "email": "nbakuri@cac.gov.ng",
                "mobile": "08077913345",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a7d77e4b404c8082.jpeg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "Plot 420, Tigris Crescent,\r\nOff Aguiyi Ironsi Street,\r\nMaitama, Abuja.\r\nNigeria.",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "7f482b43-0e62-4ae6-8728-37d54423fec2",
                "address_id": 76,
                "candidate_id": 19,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-09 11:28:52",
                "updated_at": "2018-02-09 11:28:52",
                "images": [
                    {
                        "id": 34,
                        "uuid": "966414dc-1a2b-43ab-ae54-776ccce1cf8b",
                        "live_photo_id": 36,
                        "candidate_id": 19,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a7d77e4b404c8082.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-09 11:28:53",
                        "updated_at": "2018-02-09 11:28:53",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a7d77e4b404c8082.jpeg"
                    }
                ],
                "address": {
                    "uuid": "e4a35a7d-b8cc-45ac-9aa0-bcef00fc4772",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 19,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "Plot 420",
                    "sub_street": "Off Aguiyi Ironsi Street",
                    "street": "Tigris Crescent",
                    "landmark": "",
                    "state": "Abuja",
                    "city": "Maitama",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "7.493583699999999",
                    "latitude": "9.0818094",
                    "what3words": "privately.commitments.switchboards",
                    "what3words_map": "http://w3w.co/privately.commitments.switchboards",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-09 11:28:52",
                    "updated_at": "2018-02-09 11:28:52",
                    "formatted": "Plot 420, Sub Street Off Aguiyi Ironsi Street, Tigris Crescent Street, Maitama, Abuja, Nigeria, ",
                    "map_format": "Plot 420 Tigris Crescent, Maitama , Abuja, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 34,
                        "uuid": "966414dc-1a2b-43ab-ae54-776ccce1cf8b",
                        "live_photo_id": 36,
                        "candidate_id": 19,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a7d77e4b404c8082.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-09 11:28:53",
                        "updated_at": "2018-02-09 11:28:53",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a7d77e4b404c8082.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "7f482b43-0e62-4ae6-8728-37d54423fec2",
            "created_at": "2018-02-09 11:28:53",
            "last_updated_at": "2019-04-12 06:00:22",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "1b3943bb-3358-4cee-9d34-c756b69572bf",
            "reference_id": "5a7d9d355d406",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "reference_check",
            "download_url": null,
            "description": "",
            "package_name": "Reference Check Address Verification",
            "details": {
                "uuid": "0faa4572-fe4f-4662-b51d-6e46fa7c90fa",
                "address_id": 77,
                "first_name": "Tobi",
                "last_name": "Adeyemi",
                "email": "tobiadeyemi91@gmail.com",
                "mobile": "",
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "created_at": "2018-02-09 14:08:05",
                "updated_at": "2018-02-09 14:08:05",
                "name": "Adeyemi Tobi",
                "address": {
                    "uuid": "5116bfbe-3e52-4a59-9075-20662de6620a",
                    "user_id": 1,
                    "user_type": "user",
                    "candidate_id": 1,
                    "flat_number": "5",
                    "building_name": "White Building",
                    "building_number": "3",
                    "sub_street": "Bishop",
                    "street": "13B Bishop Street",
                    "landmark": "",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.359796",
                    "latitude": "6.552381",
                    "what3words": "skewed.rigid.craters",
                    "what3words_map": "http://w3w.co/skewed.rigid.craters",
                    "agent_geo": "",
                    "start_date": "2017-10-05",
                    "end_date": "2017-10-09",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "reference",
                    "created_at": "2018-02-09 14:08:05",
                    "updated_at": "2018-02-09 14:08:05",
                    "formatted": "Flat Number 5, White Building, 3, Sub Street Bishop, 13b Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "3 13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "guarantor_image": null
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "0faa4572-fe4f-4662-b51d-6e46fa7c90fa",
            "created_at": "2018-02-09 14:08:05",
            "last_updated_at": "2019-04-12 06:00:23",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "a9dd81da-e068-40fa-b7a0-356fd9bf18db",
            "reference_id": "5a7dad1bc360a",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "f4e65144-2905-41b9-8ea3-c593bc8700b3",
                "address_id": 78,
                "candidate_id": 1,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-09 15:15:55",
                "updated_at": "2018-02-09 15:15:55",
                "images": [
                    {
                        "id": 35,
                        "uuid": "2356c46d-2815-4d6c-b8a7-6be20b1e8fb4",
                        "live_photo_id": 37,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5a7dad1b9296a2886.png",
                        "deleted_at": null,
                        "created_at": "2018-02-09 15:15:55",
                        "updated_at": "2018-02-09 15:15:55",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a7dad1b9296a2886.png"
                    }
                ],
                "address": {
                    "uuid": "9ad636fc-10fe-4971-a036-685c61d8d130",
                    "user_id": 1,
                    "user_type": "user",
                    "candidate_id": 1,
                    "flat_number": "5",
                    "building_name": "White Building",
                    "building_number": "13",
                    "sub_street": "Bishop",
                    "street": "Bishop Street",
                    "landmark": "",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.360025",
                    "latitude": "6.5521614",
                    "what3words": "spreads.includes.kept",
                    "what3words_map": "http://w3w.co/spreads.includes.kept",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-09 15:15:55",
                    "updated_at": "2018-02-09 15:15:55",
                    "formatted": "Flat Number 5, White Building, 13, Sub Street Bishop, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13 Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 35,
                        "uuid": "2356c46d-2815-4d6c-b8a7-6be20b1e8fb4",
                        "live_photo_id": 37,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5a7dad1b9296a2886.png",
                        "deleted_at": null,
                        "created_at": "2018-02-09 15:15:55",
                        "updated_at": "2018-02-09 15:15:55",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a7dad1b9296a2886.png"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "f4e65144-2905-41b9-8ea3-c593bc8700b3",
            "created_at": "2018-02-09 15:15:55",
            "last_updated_at": "2019-04-12 06:00:24",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "850f902c-f455-4d0c-8d7e-6a634065c79a",
            "reference_id": "5a82f17bce82c",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-03-06",
            "end_time": "2018-03-08",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-08",
            "status": "completed",
            "task_status": "VERIFIED",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": "https://api.staging.youverify.co/v1/reports/850f902c-f455-4d0c-8d7e-6a634065c79a/download/pdf",
            "description": "",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "ca404451-bec6-4161-9d9b-fba1951a0d1f",
                "address_id": 82,
                "candidate_id": 1,
                "photo_url": null,
                "status": "VERIFIED",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-02-13 15:08:58",
                "updated_at": "2018-02-13 15:37:54",
                "images": [
                    {
                        "id": 36,
                        "uuid": "5f4ef135-2145-46aa-a5d0-55a0ab5db18e",
                        "live_photo_id": 38,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a82f17a75e495909.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-13 15:08:59",
                        "updated_at": "2018-02-13 15:08:59",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a82f17a75e495909.jpeg"
                    }
                ],
                "address": {
                    "uuid": "b6759ad6-0f55-408a-a962-b1006aa883db",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "Police station",
                    "state": "lagos",
                    "city": "ilupeju",
                    "post_code": "234001",
                    "country": "Nigeria",
                    "longitude": "3.359796",
                    "latitude": "6.552381",
                    "what3words": "skewed.rigid.craters",
                    "what3words_map": "http://w3w.co/skewed.rigid.craters",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-02-13 15:08:58",
                    "updated_at": "2018-02-13 15:08:58",
                    "formatted": "13b, Bishop  Street, Police Station, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 36,
                        "uuid": "5f4ef135-2145-46aa-a5d0-55a0ab5db18e",
                        "live_photo_id": 38,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5a82f17a75e495909.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-02-13 15:08:59",
                        "updated_at": "2018-02-13 15:08:59",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5a82f17a75e495909.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [
                {
                    "id": 14,
                    "report_id": 1069,
                    "agent_id": 5,
                    "note": "Testing second note",
                    "created_at": "2018-02-13 15:33:36",
                    "updated_at": "2018-02-13 15:33:36",
                    "formatted_time": "13 Feb, 2018 03:33:pm"
                },
                {
                    "id": 15,
                    "report_id": 1069,
                    "agent_id": 5,
                    "note": "Second note",
                    "created_at": "2018-02-13 15:35:46",
                    "updated_at": "2018-02-13 15:35:46",
                    "formatted_time": "13 Feb, 2018 03:35:pm"
                },
                {
                    "id": 16,
                    "report_id": 1069,
                    "agent_id": 5,
                    "note": "Second note",
                    "created_at": "2018-02-13 15:37:52",
                    "updated_at": "2018-02-13 15:37:52",
                    "formatted_time": "13 Feb, 2018 03:37:pm"
                }
            ],
            "signature": [
                "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"
            ],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "ca404451-bec6-4161-9d9b-fba1951a0d1f",
            "created_at": "2018-02-13 15:08:59",
            "last_updated_at": "2019-04-02 12:35:49",
            "what3words": "warbler.caged.dreamer",
            "what3words_map_link": "http://w3w.co/warbler.caged.dreamer",
            "digital_address_code": "warbler.caged.dreamer",
            "digital_address_url": "http://w3w.co/warbler.caged.dreamer",
            "map_address_url": "https://www.google.com/maps/search/?api=1&query=13b+Bishop+Street%2C+Ilupeju+%2C+Lagos%2C+Nigeria",
            "map_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.552452975890182, 3.359806425872594",
            "report_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.552452975890182, 3.359806425872594",
            "report_longitude": "3.359806425872594",
            "report_latitude": "6.552452975890182",
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 8,
            "images": {
                "data": [
                    {
                        "id": 28,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1518532664294_42074.jpg",
                        "file_size": "76177",
                        "file_path": "uploads/reports/images/2018-02-13/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-13/original/1518532664294_42074.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-02-13/resize/1518532664294_42074.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-02-13/original/1518532664294_42074.jpg",
                        "h": 1280,
                        "w": 960,
                        "resize_height": 533,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "2b403606-036c-48c1-a563-1894e560a4ef",
            "reference_id": "5a9d313ac483b",
            "subject_consent": true,
            "candidate": {
                "id": "228d1138-f34d-4157-9c62-8083a4edfc66",
                "reference_id": "YV5a9d3138dc562",
                "name": "Famous Prior Ehichioya",
                "first_name": "Ehichioya",
                "last_name": "Famous",
                "middle_name": "Prior",
                "email": "f.ehichioya@gmail.com",
                "mobile": "08036208553",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5cd0386a976102779.jpeg"
            },
            "start_time": "2018-03-05",
            "end_time": "2018-03-07",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-07",
            "status": "completed",
            "task_status": "VERIFIED",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "address_verification",
            "download_url": "https://api.staging.youverify.co/v1/reports/2b403606-036c-48c1-a563-1894e560a4ef/download/pdf",
            "description": null,
            "package_name": "Address Verification",
            "details": {
                "uuid": "8efb4294-cc6d-4a1f-a253-1ce1c5d220ce",
                "user_id": 1,
                "user_type": "partner",
                "candidate_id": 21,
                "flat_number": "",
                "building_name": "",
                "building_number": "13B",
                "sub_street": "",
                "street": "Bishop Street",
                "landmark": "",
                "state": "Lagos",
                "city": "Ilupeju",
                "post_code": "",
                "country": "Nigeria",
                "longitude": "3.359796",
                "latitude": "6.552381",
                "what3words": "skewed.rigid.craters",
                "what3words_map": "http://w3w.co/skewed.rigid.craters",
                "agent_geo": "",
                "start_date": "",
                "end_date": "",
                "status": "VERIFIED",
                "reason_for_fail": null,
                "item_id": "0",
                "item_type": "address",
                "created_at": "2018-03-05 12:59:54",
                "updated_at": "2018-03-05 13:21:06",
                "formatted": "13b, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                "map_address_url": null,
                "map_geolocation_url": null
            },
            "has_address": true,
            "notes": [
                {
                    "id": 21,
                    "report_id": 1077,
                    "agent_id": 2,
                    "note": "Testing note for address verification",
                    "created_at": "2018-03-05 13:18:26",
                    "updated_at": "2018-03-05 13:18:26",
                    "formatted_time": "05 Mar, 2018 01:18:pm"
                },
                {
                    "id": 22,
                    "report_id": 1077,
                    "agent_id": 2,
                    "note": "Testing note 2",
                    "created_at": "2018-03-05 13:18:45",
                    "updated_at": "2018-03-05 13:18:45",
                    "formatted_time": "05 Mar, 2018 01:18:pm"
                }
            ],
            "signature": [
                "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"
            ],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "8efb4294-cc6d-4a1f-a253-1ce1c5d220ce",
            "created_at": "2018-03-05 12:59:54",
            "last_updated_at": "2019-04-02 12:35:51",
            "what3words": "divides.canine.button",
            "what3words_map_link": "http://w3w.co/divides.canine.button",
            "digital_address_code": "divides.canine.button",
            "digital_address_url": "http://w3w.co/divides.canine.button",
            "map_address_url": "https://www.google.com/maps/search/?api=1&query=13b+Bishop+Street%2C+Ilupeju+%2C+Lagos%2C+Nigeria",
            "map_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524357, 3.3598399",
            "report_geolocation_url": "https://www.google.com/maps/search/?api=1&query=6.5524357, 3.3598399",
            "report_longitude": "3.3598399",
            "report_latitude": "6.5524357",
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 7,
            "images": {
                "data": [
                    {
                        "id": 41,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1520252417326_32747.jpg",
                        "file_size": "11283",
                        "file_path": "uploads/reports/images/2018-03-05/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-03-05/original/1520252417326_32747.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-03-05/resize/1520252417326_32747.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-03-05/original/1520252417326_32747.jpg",
                        "h": 360,
                        "w": 640,
                        "resize_height": 225,
                        "resize_width": 400
                    },
                    {
                        "id": 42,
                        "file_type": "image/jpeg",
                        "file_extension": "jpg",
                        "file_name": "1520252444877_96400.jpg",
                        "file_size": "8032",
                        "file_path": "uploads/reports/images/2018-03-05/",
                        "report_file_type": "report_image",
                        "original_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-03-05/original/1520252444877_96400.jpg",
                        "resize_file_path": "https://api.staging.youverify.co/uploads/reports/images/2018-03-05/resize/1520252444877_96400.jpg",
                        "src": "https://api.staging.youverify.co/uploads/reports/images/2018-03-05/original/1520252444877_96400.jpg",
                        "h": 360,
                        "w": 640,
                        "resize_height": 225,
                        "resize_width": 400
                    }
                ]
            }
        },
        {
            "id": "e09862d8-969a-4784-9bb1-8c8a053f0b41",
            "reference_id": "5a9d33bb1506d",
            "subject_consent": true,
            "candidate": {
                "id": "228d1138-f34d-4157-9c62-8083a4edfc66",
                "reference_id": "YV5a9d3138dc562",
                "name": "Famous Prior Ehichioya",
                "first_name": "Ehichioya",
                "last_name": "Famous",
                "middle_name": "Prior",
                "email": "f.ehichioya@gmail.com",
                "mobile": "08036208553",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5cd0386a976102779.jpeg"
            },
            "start_time": "2018-03-05",
            "end_time": "2018-03-07",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-07",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "address_verification",
            "download_url": null,
            "description": "",
            "package_name": "Address Verification",
            "details": {
                "uuid": "6355e33f-621e-4a1e-8f8b-dc455d03db6a",
                "user_id": 1,
                "user_type": "partner",
                "candidate_id": 21,
                "flat_number": "",
                "building_name": "",
                "building_number": "13B",
                "sub_street": "",
                "street": "Bishop Street",
                "landmark": "",
                "state": "Lagos",
                "city": "Ilupeju",
                "post_code": "",
                "country": "Nigeria",
                "longitude": "3.359796",
                "latitude": "6.552381",
                "what3words": "skewed.rigid.craters",
                "what3words_map": "http://w3w.co/skewed.rigid.craters",
                "agent_geo": "",
                "start_date": "",
                "end_date": "",
                "status": "PENDING",
                "reason_for_fail": null,
                "item_id": "0",
                "item_type": "address",
                "created_at": "2018-03-05 13:10:35",
                "updated_at": "2018-03-05 13:10:35",
                "formatted": "13b, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                "map_address_url": null,
                "map_geolocation_url": null
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "6355e33f-621e-4a1e-8f8b-dc455d03db6a",
            "created_at": "2018-03-05 13:10:35",
            "last_updated_at": "2019-04-12 06:00:33",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "2327c2b3-6b8b-41e7-b332-a9e45156f672",
            "reference_id": "5aa6a3f5b8389",
            "subject_consent": true,
            "candidate": {
                "id": "228d1138-f34d-4157-9c62-8083a4edfc66",
                "reference_id": "YV5a9d3138dc562",
                "name": "Famous Prior Ehichioya",
                "first_name": "Ehichioya",
                "last_name": "Famous",
                "middle_name": "Prior",
                "email": "f.ehichioya@gmail.com",
                "mobile": "08036208553",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5cd0386a976102779.jpeg"
            },
            "start_time": "2018-03-16",
            "end_time": "2018-03-20",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-20",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": null,
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "05811b03-5378-4b8b-a9d6-3cd55113940c",
                "address_id": 99,
                "candidate_id": 21,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-03-12 16:59:49",
                "updated_at": "2018-03-12 16:59:49",
                "images": [
                    {
                        "id": 42,
                        "uuid": "f9226f05-d555-426f-9c03-c8b37f16e55b",
                        "live_photo_id": 44,
                        "candidate_id": 21,
                        "image_type": "image/png",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5aa6a3f55c6a67623.png",
                        "deleted_at": null,
                        "created_at": "2018-03-12 16:59:49",
                        "updated_at": "2018-03-12 16:59:49",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5aa6a3f55c6a67623.png"
                    }
                ],
                "address": {
                    "uuid": "5ca01d16-d623-4e3c-be80-8a347ffd6e7d",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 21,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "Police Station",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.359796",
                    "latitude": "6.552381",
                    "what3words": "skewed.rigid.craters",
                    "what3words_map": "http://w3w.co/skewed.rigid.craters",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-03-12 16:59:49",
                    "updated_at": "2018-03-12 16:59:49",
                    "formatted": "13b, Bishop  Street, Police Station, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 42,
                        "uuid": "f9226f05-d555-426f-9c03-c8b37f16e55b",
                        "live_photo_id": 44,
                        "candidate_id": 21,
                        "image_type": "image/png",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5aa6a3f55c6a67623.png",
                        "deleted_at": null,
                        "created_at": "2018-03-12 16:59:49",
                        "updated_at": "2018-03-12 16:59:49",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5aa6a3f55c6a67623.png"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "05811b03-5378-4b8b-a9d6-3cd55113940c",
            "created_at": "2018-03-12 16:59:49",
            "last_updated_at": "2019-04-12 06:00:34",
            "what3words": "NULL",
            "what3words_map_link": "NULL",
            "digital_address_code": "NULL",
            "digital_address_url": "NULL",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "421a84df-3788-4091-9489-d06f588dc2f4",
            "reference_id": "5aabc17650781",
            "subject_consent": true,
            "candidate": {
                "id": "228d1138-f34d-4157-9c62-8083a4edfc66",
                "reference_id": "YV5a9d3138dc562",
                "name": "Famous Prior Ehichioya",
                "first_name": "Ehichioya",
                "last_name": "Famous",
                "middle_name": "Prior",
                "email": "f.ehichioya@gmail.com",
                "mobile": "08036208553",
                "has_live_photo": true,
                "live_photo_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5cd0386a976102779.jpeg"
            },
            "start_time": "2018-03-12",
            "end_time": "2018-03-14",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-06-14",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": null,
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "05811b03-5378-4b8b-a9d6-3cd55113940c",
                "address_id": 99,
                "candidate_id": 21,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-03-12 16:59:49",
                "updated_at": "2018-03-12 16:59:49",
                "images": [
                    {
                        "id": 42,
                        "uuid": "f9226f05-d555-426f-9c03-c8b37f16e55b",
                        "live_photo_id": 44,
                        "candidate_id": 21,
                        "image_type": "image/png",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5aa6a3f55c6a67623.png",
                        "deleted_at": null,
                        "created_at": "2018-03-12 16:59:49",
                        "updated_at": "2018-03-12 16:59:49",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5aa6a3f55c6a67623.png"
                    }
                ],
                "address": {
                    "uuid": "5ca01d16-d623-4e3c-be80-8a347ffd6e7d",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 21,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop street",
                    "landmark": "Police Station",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.359796",
                    "latitude": "6.552381",
                    "what3words": "skewed.rigid.craters",
                    "what3words_map": "http://w3w.co/skewed.rigid.craters",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-03-12 16:59:49",
                    "updated_at": "2018-03-12 16:59:49",
                    "formatted": "13b, Bishop  Street, Police Station, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 42,
                        "uuid": "f9226f05-d555-426f-9c03-c8b37f16e55b",
                        "live_photo_id": 44,
                        "candidate_id": 21,
                        "image_type": "image/png",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5aa6a3f55c6a67623.png",
                        "deleted_at": null,
                        "created_at": "2018-03-12 16:59:49",
                        "updated_at": "2018-03-12 16:59:49",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5aa6a3f55c6a67623.png"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "05811b03-5378-4b8b-a9d6-3cd55113940c",
            "created_at": "2018-03-16 14:07:02",
            "last_updated_at": "2019-04-12 06:00:35",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "23857b3d-773c-402c-99d7-576ed73b3117",
            "reference_id": "5ace329055470",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-04-11",
            "end_time": "2018-04-11",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-07-11",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "0f08bdd1-d9fc-4037-917d-1c407fdaf548",
                "address_id": 109,
                "candidate_id": 1,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-04-11 17:06:40",
                "updated_at": "2018-04-11 17:06:40",
                "images": [
                    {
                        "id": 52,
                        "uuid": "fbb3b2ca-000f-476e-9325-65a2caaad672",
                        "live_photo_id": 54,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5ace32902800d2906.png",
                        "deleted_at": null,
                        "created_at": "2018-04-11 17:06:40",
                        "updated_at": "2018-04-11 17:06:40",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5ace32902800d2906.png"
                    }
                ],
                "address": {
                    "uuid": "2fb23923-4519-4008-b934-777e02fa3114",
                    "user_id": 1,
                    "user_type": "user",
                    "candidate_id": 1,
                    "flat_number": "5",
                    "building_name": "White Building",
                    "building_number": "13",
                    "sub_street": "Bishop",
                    "street": "Bishop Street",
                    "landmark": "",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.3599767",
                    "latitude": "6.552178199999999",
                    "what3words": "cobbled.able.bearings",
                    "what3words_map": "http://w3w.co/cobbled.able.bearings",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-04-11 17:06:40",
                    "updated_at": "2018-04-11 17:06:40",
                    "formatted": "Flat Number 5, White Building, 13, Sub Street Bishop, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13 Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 52,
                        "uuid": "fbb3b2ca-000f-476e-9325-65a2caaad672",
                        "live_photo_id": 54,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5ace32902800d2906.png",
                        "deleted_at": null,
                        "created_at": "2018-04-11 17:06:40",
                        "updated_at": "2018-04-11 17:06:40",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5ace32902800d2906.png"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "0f08bdd1-d9fc-4037-917d-1c407fdaf548",
            "created_at": "2018-04-11 17:06:40",
            "last_updated_at": "2019-04-12 06:00:36",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "ffc06f3d-03b2-4ddb-80ad-7dde50fd251e",
            "reference_id": "5ace334c2216a",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-04-11",
            "end_time": "2018-04-11",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-07-11",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "ded11830-ec5a-4114-bba5-204b42eb5763",
                "address_id": 110,
                "candidate_id": 1,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-04-11 17:09:47",
                "updated_at": "2018-04-11 17:09:47",
                "images": [
                    {
                        "id": 53,
                        "uuid": "8735c699-2951-422b-932a-aaf3ccf5b2a8",
                        "live_photo_id": 55,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5ace334bb90b23420.png",
                        "deleted_at": null,
                        "created_at": "2018-04-11 17:09:48",
                        "updated_at": "2018-04-11 17:09:48",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5ace334bb90b23420.png"
                    }
                ],
                "address": {
                    "uuid": "5dea1335-4bd0-4f90-b12d-3f44fbc37d23",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "5",
                    "building_name": "White Building",
                    "building_number": "13",
                    "sub_street": "Bishop",
                    "street": "Bishop Street",
                    "landmark": "",
                    "state": "Lagos",
                    "city": "Ilupeju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "3.3599767",
                    "latitude": "6.552178199999999",
                    "what3words": "cobbled.able.bearings",
                    "what3words_map": "http://w3w.co/cobbled.able.bearings",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-04-11 17:09:47",
                    "updated_at": "2018-04-11 17:09:47",
                    "formatted": "Flat Number 5, White Building, 13, Sub Street Bishop, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
                    "map_format": "13 Bishop Street, Ilupeju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 53,
                        "uuid": "8735c699-2951-422b-932a-aaf3ccf5b2a8",
                        "live_photo_id": 55,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "png",
                        "path": "/",
                        "image_name": "photo5ace334bb90b23420.png",
                        "deleted_at": null,
                        "created_at": "2018-04-11 17:09:48",
                        "updated_at": "2018-04-11 17:09:48",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5ace334bb90b23420.png"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 0,
            "awaiting_qa": false,
            "reportable_id": "ded11830-ec5a-4114-bba5-204b42eb5763",
            "created_at": "2018-04-11 17:09:48",
            "last_updated_at": "2019-04-12 06:00:37",
            "what3words": null,
            "what3words_map_link": null,
            "digital_address_code": null,
            "digital_address_url": null,
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "d1b202f4-0380-4f80-86b6-1e6e3eaaf92b",
            "reference_id": "5ace34d28974a",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": "07035038924",
                "has_live_photo": true,
                "live_photo_path": "https://youverify-api-bucket.nyc3.digitaloceanspaces.com/reports/live_photos/2020-07-30/photo_5f22b04e5b9ca4391.jpg"
            },
            "start_time": "2018-04-11",
            "end_time": "2018-04-13",
            "execution_date": "",
            "submitted_at": "",
            "completed_at": null,
            "accepted_at": null,
            "revalidation_date": "2018-07-13",
            "status": "canceled",
            "task_status": "PENDING",
            "reason": null,
            "task_created_by": "Chinook Devops",
            "package": "live_photo",
            "download_url": null,
            "description": "Verify Tosin",
            "package_name": "Live Photo Address Verification",
            "details": {
                "uuid": "584d6da3-946b-4748-a7da-515b5a5165f4",
                "address_id": 111,
                "candidate_id": 1,
                "photo_url": null,
                "status": "PENDING",
                "reason_for_fail": null,
                "deleted_at": null,
                "created_at": "2018-04-11 17:16:18",
                "updated_at": "2018-04-11 17:16:18",
                "images": [
                    {
                        "id": 54,
                        "uuid": "b799ef46-5323-4467-8df5-a31d4a94879e",
                        "live_photo_id": 56,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5ace34d27c12d5926.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-04-11 17:16:18",
                        "updated_at": "2018-04-11 17:16:18",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5ace34d27c12d5926.jpeg"
                    }
                ],
                "address": {
                    "uuid": "748d8997-f9ba-4b12-ae2b-45b79081201a",
                    "user_id": 1,
                    "user_type": "partner",
                    "candidate_id": 1,
                    "flat_number": "",
                    "building_name": "",
                    "building_number": "13B",
                    "sub_street": "",
                    "street": "Bishop Street",
                    "landmark": "Police Station",
                    "state": "Lagos",
                    "city": "Ilueju",
                    "post_code": "",
                    "country": "Nigeria",
                    "longitude": "",
                    "latitude": "",
                    "what3words": "",
                    "what3words_map": "",
                    "agent_geo": "",
                    "start_date": "",
                    "end_date": "",
                    "status": "PENDING",
                    "reason_for_fail": null,
                    "item_id": "0",
                    "item_type": "live_photo",
                    "created_at": "2018-04-11 17:16:18",
                    "updated_at": "2018-04-11 17:16:18",
                    "formatted": "13b, Bishop  Street, Police Station, Ilueju, Lagos, Nigeria, ",
                    "map_format": "13b Bishop Street, Ilueju , Lagos, Nigeria",
                    "map_address_url": null,
                    "map_geolocation_url": null
                },
                "live_photos": [
                    {
                        "id": 54,
                        "uuid": "b799ef46-5323-4467-8df5-a31d4a94879e",
                        "live_photo_id": 56,
                        "candidate_id": 1,
                        "image_type": "image/jpeg",
                        "image_extension": "jpeg",
                        "path": "/",
                        "image_name": "photo5ace34d27c12d5926.jpeg",
                        "deleted_at": null,
                        "created_at": "2018-04-11 17:16:18",
                        "updated_at": "2018-04-11 17:16:18",
                        "image_path": "https://api.staging.youverify.co/uploads/tasks/livephoto/photo5ace34d27c12d5926.jpeg"
                    }
                ]
            },
            "has_address": true,
            "notes": [],
            "signature": [],
            "is_flagged": 1,
            "awaiting_qa": false,
            "reportable_id": "584d6da3-946b-4748-a7da-515b5a5165f4",
            "created_at": "2018-04-11 17:16:18",
            "last_updated_at": "2019-04-12 06:00:38",
            "what3words": "NULL",
            "what3words_map_link": "NULL",
            "digital_address_code": "NULL",
            "digital_address_url": "NULL",
            "map_address_url": null,
            "map_geolocation_url": null,
            "report_geolocation_url": null,
            "report_longitude": null,
            "report_latitude": null,
            "can_view_report": true,
            "business": "Youverify",
            "reasons_for_failure": [
                "Address does not exist",
                "Address not accessible",
                "Candidate does not live there"
            ],
            "submission_distance_in_meters": 0,
            "images": {
                "data": []
            }
        },
        {
            "id": "698efa83-568d-43ef-940c-7a1d0852cbac",
            "reference_id": "5ad0d624a9270",
            "subject_consent": true,
            "candidate": {
                "id": "df609d55-5d1e-47d0-a1b7-55e5697761d0",
                "reference_id": "YV5a0d93e640174",
                "name": "Akomolafe Seun Tosin",
                "first_name": "Tosin",
                "last_name": "Akomolafe",
                "middle_name": "Seun",
                "email": "gettosin4me@gmail.com",
                "mobile": null
            },
            "status": "failed",
            "reason": "-",
            "identity_status": "not verified",
            "identity_number": "11111111111",
            "package": "identity",
            "package_name": "Identity",
            "type": "nin",
            "business": "Youverify",
            "task_created_by": "Chinook Devops",
            "end_time": "2018-04-13",
            "created_at": "2018-04-13 17:09:08",
            "images": {
                "data": []
            }
        }
    ],
    "meta": {
        "pagination": {
            "total": 1074,
            "count": 20,
            "per_page": 20,
            "current_page": 1,
            "total_pages": 54,
            "links": {
                "next": "https://api.staging.youverify.co/v1/reports?page=2"
            }
        }
    },
    "total": 1074,
    "per_page": 20,
    "current_page": 1,
    "last_page": 54,
    "next_page_url": "https://api.staging.youverify.co/v1/reports?page=2",
    "prev_page_url": null,
    "to": 20,
    "from": 1,
    "message": "Successful",
    "status_code": 200
}
```

## Candidates

The endpoint returns all the candidates you have checked.

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/candidates",
  "headers": {
    "Token": "{{token}}"
  }
}
```

Response

```json
{
  "data": [
    {
      "id": "34ae16a6-a527-4759-8d66-fe5d27a4361b",
      "reference_id": "YV5a1d27c8c1d16",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "middle_name": "",
      "last_name": "Akomolafe",
      "gender": "male",
      "dob": "",
      "mobile": "08091213344",
      "email": "gettosin4me@gmail.com",
      "country": "",
      "has_live_photo": true,
      "live_photo_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg",
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/34ae16a6-a527-4759-8d66-fe5d27a4361b",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2017-11-28 10:09:28"
    },
    {
      "id": "1b8dcea0-c9af-496e-8d3d-883e639e55c8",
      "reference_id": "YV5ad604919c6c6",
      "name": "Ibrahim Kamoru Seun",
      "first_name": "Seun",
      "middle_name": "Kamoru",
      "last_name": "Ibrahim",
      "gender": "",
      "dob": "1986-07-15",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/1b8dcea0-c9af-496e-8d3d-883e639e55c8",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-04-17 15:28:33"
    },
    {
      "id": "229cd235-eb19-409c-a6aa-c8e90781c01e",
      "reference_id": "YV5ad6051c43184",
      "name": "Jiteh Chima Steven",
      "first_name": "Steven",
      "middle_name": "Chima",
      "last_name": "Jiteh",
      "gender": "",
      "dob": "1974-09-24",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/229cd235-eb19-409c-a6aa-c8e90781c01e",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-04-17 15:30:52"
    },
    {
      "id": "6aaa8948-76ce-40c7-95ac-9462fc339a8b",
      "reference_id": "YV5ada1592d50d3",
      "name": "Yemi Adedeji",
      "first_name": "Adedeji",
      "middle_name": "",
      "last_name": "Yemi",
      "gender": "male",
      "dob": "1992-01-16",
      "mobile": "09012312312",
      "email": "oluyemi@gmail.com",
      "country": "",
      "has_live_photo": true,
      "live_photo_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5ada15977ef1d5447.jpeg",
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/6aaa8948-76ce-40c7-95ac-9462fc339a8b",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-04-20 17:30:10"
    },
    {
      "id": "904c0993-d8f4-4c11-b390-3543911981ac",
      "reference_id": "YV5b322875ecd98",
      "name": "Chima Steven Jiteh",
      "first_name": "Jiteh",
      "middle_name": "Steven",
      "last_name": "Chima",
      "gender": "",
      "dob": "1975-10-01",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/904c0993-d8f4-4c11-b390-3543911981ac",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-06-26 12:50:13"
    },
    {
      "id": "bc8d55e0-cc54-4ec9-b9c4-d3b7d36a7e12",
      "reference_id": "YV5b3231b8ca0ef",
      "name": "Gbamgbose Olakanmi Nicholas",
      "first_name": "Nicholas",
      "middle_name": "Olakanmi",
      "last_name": "Gbamgbose",
      "gender": "",
      "dob": "1991-12-06",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/bc8d55e0-cc54-4ec9-b9c4-d3b7d36a7e12",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-06-26 13:29:44"
    },
    {
      "id": "949a0b3a-b832-4b08-984e-6421e1889e88",
      "reference_id": "YV5b3df448a662a",
      "name": "akomolafe tosin",
      "first_name": "tosin",
      "middle_name": "",
      "last_name": "akomolafe",
      "gender": "",
      "dob": "1991-01-02",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/949a0b3a-b832-4b08-984e-6421e1889e88",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-05 11:34:48"
    },
    {
      "id": "9a2c4bc3-0d22-4612-9171-0ee792b132e9",
      "reference_id": "YV5b3f35bb91a7f",
      "name": "Akinade Akintunde",
      "first_name": "Akintunde",
      "middle_name": "",
      "last_name": "Akinade",
      "gender": "",
      "dob": "1975-08-13",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/9a2c4bc3-0d22-4612-9171-0ee792b132e9",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-06 10:26:19"
    },
    {
      "id": "f914614a-dff7-4bf9-8552-64c5b6611980",
      "reference_id": "YV5b3f424dea599",
      "name": "Bashir Saidu",
      "first_name": "Saidu",
      "middle_name": "",
      "last_name": "Bashir",
      "gender": "",
      "dob": "1986-01-10",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/f914614a-dff7-4bf9-8552-64c5b6611980",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-06 11:19:58"
    },
    {
      "id": "e4fece2e-f1ac-4f1a-a244-fc8f4e48f7dc",
      "reference_id": "YV5b48b89744e12",
      "name": "Odegbami Gbenga",
      "first_name": "Gbenga",
      "middle_name": "",
      "last_name": "Odegbami",
      "gender": "",
      "dob": "1981-04-25",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/e4fece2e-f1ac-4f1a-a244-fc8f4e48f7dc",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-13 15:35:03"
    },
    {
      "id": "97de174f-c05f-431a-9071-8f801f19d1cc",
      "reference_id": "YV5b4cc85a5d774",
      "name": "Odegbami Gbenga",
      "first_name": "Gbenga",
      "middle_name": "",
      "last_name": "Odegbami",
      "gender": "",
      "dob": "1981-04-25",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/97de174f-c05f-431a-9071-8f801f19d1cc",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-16 17:31:22"
    },
    {
      "id": "f24cbf98-383a-48c9-ba57-348e9d68c9c6",
      "reference_id": "YV5a201de7aba7e",
      "name": "OLAITAN YISA KAZEEM",
      "first_name": "KAZEEM",
      "middle_name": "YISA",
      "last_name": "OLAITAN",
      "gender": "Male",
      "dob": "1976-07-29",
      "mobile": "08066885085",
      "email": "08066885085@halogen.com",
      "country": "NIGERIA",
      "has_live_photo": true,
      "live_photo_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5b536a507a6be9393.jpeg",
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/f24cbf98-383a-48c9-ba57-348e9d68c9c6",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2017-11-30 16:04:07"
    },
    {
      "id": "5d3c13e0-a125-4242-bcbb-bf2c02033fa6",
      "reference_id": "YV5b587d9b2e84b",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "middle_name": "",
      "last_name": "Akomolafe",
      "gender": "",
      "dob": "1981-04-25",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/5d3c13e0-a125-4242-bcbb-bf2c02033fa6",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-25 14:39:39"
    },
    {
      "id": "09a03866-55c7-467c-bc59-fcac33b448f0",
      "reference_id": "YV5b5881ea07b05",
      "name": "Odegbami Gbenga",
      "first_name": "Gbenga",
      "middle_name": "",
      "last_name": "Odegbami",
      "gender": "",
      "dob": "1981-04-25",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/09a03866-55c7-467c-bc59-fcac33b448f0",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-25 14:58:02"
    },
    {
      "id": "9ef6ba0b-8763-4b8b-8626-1dc8cd6e0ca7",
      "reference_id": "YV5b5882bc76334",
      "name": "Odegbami Gbenga",
      "first_name": "Gbenga",
      "middle_name": "",
      "last_name": "Odegbami",
      "gender": "",
      "dob": "1981-04-25",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/9ef6ba0b-8763-4b8b-8626-1dc8cd6e0ca7",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-25 15:01:32"
    },
    {
      "id": "a585d069-4cbe-48e5-9f5a-24750339d5dc",
      "reference_id": "YV5b5f5c819c171",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "middle_name": "",
      "last_name": "Akomolafe",
      "gender": "",
      "dob": "1990-10-01",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/a585d069-4cbe-48e5-9f5a-24750339d5dc",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-07-30 19:44:17"
    },
    {
      "id": "1efa5b84-f47d-4530-84c5-ce5ba24f4bf7",
      "reference_id": "YV5b632931276aa",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "middle_name": "",
      "last_name": "Akomolafe",
      "gender": "",
      "dob": "1990-10-01",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/1efa5b84-f47d-4530-84c5-ce5ba24f4bf7",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-08-02 16:54:25"
    },
    {
      "id": "2b6c89bf-6742-4d82-b600-c0429e3630d7",
      "reference_id": "YV5b632968ce8e7",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "middle_name": "",
      "last_name": "Akomolafe",
      "gender": "",
      "dob": "1990-10-01",
      "mobile": null,
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/2b6c89bf-6742-4d82-b600-c0429e3630d7",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-08-02 16:55:20"
    },
    {
      "id": "557fe674-1e34-42ba-aa85-a77048674f86",
      "reference_id": "YV5a201dee941e0",
      "name": "OSUAGWA OBINNA EZEKIEL",
      "first_name": "EZEKIEL",
      "middle_name": "OBINNA",
      "last_name": "OSUAGWA",
      "gender": "Male",
      "dob": "1996-11-18",
      "mobile": "08125425520",
      "email": "08125425520@halogen.com",
      "country": "NIGERIA",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/557fe674-1e34-42ba-aa85-a77048674f86",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2017-11-30 16:04:14"
    },
    {
      "id": "1e654fbc-d003-46c4-a13c-00fbe9cb6f19",
      "reference_id": "YV5b76cbcf66bba",
      "name": "Jiteh Chima Steven",
      "first_name": "Steven",
      "middle_name": "Chima",
      "last_name": "Jiteh",
      "gender": "",
      "dob": "1974-09-24",
      "mobile": "07035038924",
      "email": null,
      "country": "",
      "has_live_photo": false,
      "live_photo_path": null,
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/1e654fbc-d003-46c4-a13c-00fbe9cb6f19",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2018-08-17 14:21:19"
    },
    {
      "id": "b65aa159-e5e2-4198-9f8f-295a91fe73cd",
      "reference_id": "YV5a201deb83fe1",
      "name": "EKUMA UCHENNA NEBETH",
      "first_name": "NEBETH",
      "middle_name": "UCHENNA",
      "last_name": "EKUMA",
      "gender": "Male",
      "dob": "1992-02-02",
      "mobile": "08060467613",
      "email": "08060467613@halogen.com",
      "country": "NIGERIA",
      "has_live_photo": true,
      "live_photo_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5b76cf67433b07241.png",
      "mothers_maiden_name": "",
      "previous_last_name": "",
      "nationality": "",
      "country_of_birth": "",
      "town_of_birth": "",
      "href": "http://api.youverify.local/candidates/b65aa159-e5e2-4198-9f8f-295a91fe73cd",
      "has_reports": true,
      "id_numbers": [],
      "created_at": "2017-11-30 16:04:11"
    }
  ],
  "message": "Successful",
  "status_code": 200
}
```

## Candidate Report

This endpoint returns a particular candidates report.

```json http
{
  "method": "get",
  "url": "https://api.staging.youverify.co/v1/candidates/{candidate_id}/reports",
  "headers": {
    "Token": "{{token}}"
  }
}
```

Response

```json
{
    "data": [],
    "meta": {
        "pagination": {
            "total": 0,
            "count": 0,
            "per_page": 20,
            "current_page": 1,
            "total_pages": 0,
            "links": []
        }
    },
    "total": 0,
    "per_page": 20,
    "current_page": 1,
    "last_page": 0,
    "next_page_url": null,
    "prev_page_url": null,
    "to": 0,
    "from": 1,
    "message": "Successful",
    "status_code": 200
}
```

## Report

This endpoint returns the details of a report.

```json http
{
  "method": "get",
  "url": "https://api.staging.youverify.co/v1/reports/{id}",
  "headers": {
    "Token": "{{token}}"
  }
}
```

Response

```json
{
  "data": {
    "id": "381b87f0-f496-4052-a98e-8cb4c52b5fce",
    "reference_id": "5a1d27d09163d",
    "candidate": {
      "id": "34ae16a6-a527-4759-8d66-fe5d27a4361b",
      "reference_id": "YV5a1d27c8c1d16",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "last_name": "Akomolafe",
      "middle_name": "",
      "email": "gettosin4me@gmail.com",
      "mobile": "08091213344",
      "has_live_photo": true,
      "live_photo_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg"
    },
    "start_time": "2018-03-06",
    "end_time": "2018-03-08",
    "execution_date": "2019-02-26 17:54:03",
    "revalidation_date": "2018-06-08",
    "status": "canceled",
    "task_status": "VERIFIED",
    "task_created_by": "Chinook Developer",
    "package": "live_photo",
    "download_url": null,
    "description": "",
    "package_name": "Live Photo Address Verification",
    "details": {
      "uuid": "fa234602-49f6-48ec-9a8f-aaa569109eb7",
      "address_id": 1,
      "candidate_id": 1,
      "photo_url": null,
      "status": "VERIFIED",
      "reason_for_fail": null,
      "deleted_at": null,
      "created_at": "2017-11-28 10:09:36",
      "updated_at": "2018-02-13 15:50:59",
      "images": [
        {
          "id": 1,
          "uuid": "4cc6361e-791e-44c0-b797-9261fcc47a0c",
          "live_photo_id": 1,
          "candidate_id": 1,
          "image_type": "image/jpeg",
          "image_extension": "jpeg",
          "path": "/",
          "image_name": "photo5a1d27d0798da1087.jpeg",
          "deleted_at": null,
          "created_at": "2017-11-28 10:09:36",
          "updated_at": "2017-11-28 10:09:36",
          "image_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg"
        }
      ],
      "address": {
        "uuid": "73df8ed4-6d35-446a-8af0-54b60b88153a",
        "user_id": 1,
        "user_type": "partner",
        "candidate_id": 1,
        "flat_number": "",
        "building_name": "",
        "building_number": "13B",
        "sub_street": "",
        "street": "Bishop street",
        "landmark": "",
        "state": "Lagos",
        "city": "Ilupeju",
        "post_code": "",
        "country": "Nigeria",
        "longitude": "3.3598313",
        "latitude": "6.551594499999999",
        "what3words": "outdone.sprain.times",
        "what3words_map": "http://w3w.co/outdone.sprain.times",
        "agent_geo": "",
        "start_date": "",
        "end_date": "",
        "status": "PENDING",
        "reason_for_fail": null,
        "item_id": "0",
        "item_type": "live_photo",
        "created_at": "2017-11-28 10:09:36",
        "updated_at": "2017-11-28 10:09:36",
        "formatted": "13b, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
        "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
        "map_address_url": null,
        "map_geolocation_url": null
      },
      "live_photos": [
        {
          "id": 1,
          "uuid": "4cc6361e-791e-44c0-b797-9261fcc47a0c",
          "live_photo_id": 1,
          "candidate_id": 1,
          "image_type": "image/jpeg",
          "image_extension": "jpeg",
          "path": "/",
          "image_name": "photo5a1d27d0798da1087.jpeg",
          "deleted_at": null,
          "created_at": "2017-11-28 10:09:36",
          "updated_at": "2017-11-28 10:09:36",
          "image_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg"
        }
      ]
    },
    "has_address": true,
    "notes": [
      {
        "id": 1,
        "report_id": 1000,
        "agent_id": 1,
        "note": "Welcome to the land of turban",
        "created_at": "2018-02-13 15:51:08",
        "updated_at": "2018-02-13 15:51:08",
        "formatted_time": "13 Feb, 2018 03:51:pm"
      },
      {
        "id": 2,
        "report_id": 1000,
        "agent_id": 1,
        "note": "am testing note",
        "created_at": "2018-02-13 15:51:08",
        "updated_at": "2018-02-13 15:51:08",
        "formatted_time": "13 Feb, 2018 03:51:pm"
      },
      {
        "id": 3,
        "report_id": 1000,
        "agent_id": 1,
        "note": "created array of notes",
        "created_at": "2018-02-13 15:51:08",
        "updated_at": "2018-02-13 15:51:08",
        "formatted_time": "13 Feb, 2018 03:51:pm"
      }
    ],
    "signature": [
      "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAC0ElEQVRIibWVMWgTURjHf+9yOUPPEIu0NClKqg5C6RJFoYOISDft5NAxoFPJIAqKi3UpOjkUcXDIJA46uGQpKi46VGmG0iqCNLa2DYUGY5t6Jtd3Dt7Vd68Xi0I/eLz3uPv+/+9773v/D/bYxC7fjTZrANlmHTJzF2BDGzpBMNoSRRGogKY/DGUOgFxlDtY7SHQCHdhKDaYO9FzqKcTs2JAwRRbAc73KVmNrsvq0OlF/W/8GNBWiEIloA24BVvZm9px91L4vTJGJyBTP9ZYbnxtXK3crr3ySgGj76HSCADyRvZE9bx+3nwgEue4c+YE8/Qf7AZhdm6U4U2R6dRoPj8bHxkjlXuUF4GgkxLTo48C+5IlkV9dQ12NhiOTlgcuMnxmnL9WHHbex4zbZVJbhY8O40qW8WiZ+ID7oLDvPmitNh/DFe3oZmoCVHkmPClNkct05CrkChtALCAxhUMgVyHXnEKbIpEfSo372ajFElqNpJs3zAPmBfCS4SpIfyAPg+5hoZR2VgSlMcRjYPvO/WfCP76OWdSgDdd8+5N1th38kmGzJr/C7Wnaz4J/AJ4oxhA1It+a+BijOFJFeW5lBepLiTBEA30eXjlCZCn82nUXnU+p06mLVqe53pcup9CmECOui9CQT0xOU5kvIpqwuPly83lprfef3W2gFZDHFR/iEsdZaS1oZ60viUOJCebXM1MoUnYlO7LjNZmuTd9V3jL0ZozRfwsOjPlW/VpusfeDPQ2sBW4AXhBVcjgUkgA5gf++V3rOpk6nbhmX0RB5RU1br7+t3lh4tvQY2gE2FJJSBFwWwPr2+tDG3Ueo40oGwRFLERAcernRkpVltPl94sHCr9rI25wP/AH4q0UdqUUjs/GwSyl6V60DcHCXqHWKnynVw+6rkBnqvPyC1D6jAIXA9Az2T/2k4O8q0XU/+15YZ2c3+RqAT6WsdrP1r3Gv7BW4wIvqstIdzAAAAAElFTkSuQmCC"
    ],
    "is_flagged": 1,
    "reportable_id": "fa234602-49f6-48ec-9a8f-aaa569109eb7",
    "created_at": "2017-11-28 10:09:36",
    "last_updated_at": "2019-02-26 17:54:03",
    "what3words": "NULL",
    "what3words_map_link": "NULL",
    "digital_address_code": "NULL",
    "digital_address_url": "NULL",
    "map_address_url": null,
    "map_geolocation_url": null,
    "report_geolocation_url": null,
    "report_longitude": null,
    "report_latitude": null,
    "can_view_report": true,
    "reasons_for_failure": [
      "Address does not exist",
      "Address not accessible",
      "Candidate does not live there"
    ],
    "submission_distance_in_meters": 0,
    "images": {
      "data": []
    }
  },
  "message": "Successful",
  "status_code": 200
}
```

## Check Account Balance

This endpoint returns your Youverify account balance.

```json http
{
  "method": "get",
  "url": "https://api.staging.youverify.co/v1/check_balance",
  "headers": {
    "Token": "{{token}}"
  }
}
```

Response

```json
{
    "data": {
        "available_balance": 29744870,
        "ledger_balance": 30226420
    },
    "message": "Successful",
    "status_code": 200
}
```

## Cancel API Call

This endpoint cancels an initiated call.

```json http
{
  "method": "post",
  "url": "https://api.staging.youverify.co/v1/reports/%7Breport_id%7D/cancel",
  "headers": {
    "Token": "{{token}}",
    "Content-Type": "application/json"
  },
  "body": {
    "reason_for_cancellation": "Not sure why"
  }
}
```

Response

```json
{
    "success": true,
    "message": "Report cancelled successfully",
    "status_code": 200
}
```

## States Names

This endpoint returns the names for all the States.

```json http
{
  "method": "get",
  "url": "https://api.staging.youverify.co/v1/states",
  "headers": {
    "Token": "{{token}}"
  }
}
```

Response

```json
{
  "data": [
    {
    "id": 1,
    "state": "Abia",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:38"
    },
    {
    "id": 2,
    "state": "Adamawa",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:38"
    },
    {
    "id": 3,
    "state": "Anambra",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:38"
    },
    {
    "id": 4,
    "state": "Akwa Ibom",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:39"
    },
    {
    "id": 5,
    "state": "Bauchi",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:39"
    },
    {
    "id": 6,
    "state": "Bayelsa",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:39"
    },
    {
    "id": 7,
    "state": "Benue",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:39"
    },
    {
    "id": 8,
    "state": "Borno",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:39"
    },
    {
    "id": 9,
    "state": "Cross River",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:39"
    },
    {
    "id": 10,
    "state": "Delta",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:40"
    },
    {
    "id": 11,
    "state": "Ebonyi",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:40"
    },
    {
    "id": 12,
    "state": "Enugu",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:40"
    },
    {
    "id": 13,
    "state": "Edo",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:40"
    },
    {
    "id": 14,
    "state": "Ekiti",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:40"
    },
    {
    "id": 15,
    "state": "Abuja",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:40"
    },
    {
    "id": 16,
    "state": "Gombe",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:41"
    },
    {
    "id": 17,
    "state": "Imo",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:41"
    },
    {
    "id": 18,
    "state": "Jigawa",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:41"
    },
    {
    "id": 19,
    "state": "Kaduna",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:41"
    },
    {
    "id": 20,
    "state": "Kano",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:41"
    },
    {
    "id": 21,
    "state": "Katsina",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:41"
    },
    {
    "id": 22,
    "state": "Kebbi",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:42"
    },
    {
    "id": 23,
    "state": "Kogi",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:42"
    },
    {
    "id": 24,
    "state": "Kwara",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:42"
    },
    {
    "id": 25,
    "state": "Lagos",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:42"
    },
    {
    "id": 26,
    "state": "Nasarawa",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:42"
    },
    {
    "id": 27,
    "state": "Niger",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:42"
    },
    {
    "id": 28,
    "state": "Ogun",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:43"
    },
    {
    "id": 29,
    "state": "Ondo",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:43"
    },
    {
    "id": 30,
    "state": "Osun",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:43"
    },
    {
    "id": 31,
    "state": "Oyo",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:43"
    },
    {
    "id": 32,
    "state": "Plateau",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:43"
    },
    {
    "id": 33,
    "state": "Rivers",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:43"
    },
    {
    "id": 34,
    "state": "Sokoto",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:44"
    },
    {
    "id": 35,
    "state": "Taraba",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:44"
    },
    {
    "id": 36,
    "state": "Yobe",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:44"
    },
    {
    "id": 37,
    "state": "Zamfara",
    "is_active": 1,
    "created_at": "2019-06-26 14:35:44"
    }
  ],
  "message": "Successful",
  "status_code": 200
}

```

## Webhook Guide

Webhook get pushed when the address or identity has been completed.

Please follow the following steps;

  ▪ Set your webhook (If already set, ignore the next step).

  ▪ Login to <https://app.youverify.co>, Go to settings -> API KEY & Webhook. Scroll to "Application Webhook" and set your callback URL.

NB. To create your webhook for staging, Please contact Technical Support at [support@youverify.co.](mailto:support@youverify.co.) A status report “PENDING” for Identity services when our upstream identity providers are unavailable. This status enable us to manage the upstream downtime. To get the completed result for a verification with a “PENDING” status, you will have to listen to the webhook to retrieve the completed verification and the corresponding response. The sample below show an identity verification request with a “PENDING” status.

PENDING REQUEST IDENTITY RESPONSE PAYLOAD

```json
{ 
 "data": { 
 "id": "reports_7cf70262-0e6d-47fd-9792-9da167db2c6a", 
 "reference_id": "5c9260b8f2e11", 
 "candidate": { 
 "id": "c3cc9392-ee0d-4c8d-b78b-599dbbaba238", 
 "reference_id": "YV5c9260b7ac780", 
 "name": "John Doe", 
 "first_name": "John", 
 "last_name": "Doe", 
 "middle_name": "", 
 "email": null, 
 "mobile": null 
  }, 
  "status": "PENDING", 
  "reason": "Pending Request", 
  "identity_number": "AAA26887AA01", 
  "package": "identity", 
  "package_name": "Identity", 
  "type": "frsc | nin | bvn | ibvn | pvc", 
  "task_created_by": "Youverify Devops", 
  "end_time": "2019-03-20 16:48:09" 
  }, 
"message": "Successful", 
"status_code": 200 
} 
```

The information below is sample post data to your registered webhook for identity verification, immediately the result is ready.

IDENTITY RESPONSE PAYLOAD

```json
{ 
'data': { 
'id' : 'reports_424380ae-5e6a-425b-abcb-24e082e4a7a5', 
'status' : 'NOT VERIFIED | VERIFIED', 
'task_status' : 'NOT VERIFIED ' | 'VERIFIED', 
'reason' : 'Invalid application details.', 
'package_name' : 'Identity', 
'candidate_id' : 3388, 
'package' : 'identity', 
'identity_type' : 'frsc | nin | bvn | ibvn | pvc', 
'identity_number' : 22122122221 
} 
}; 
```

The information below is sample post data to your registered webhook for address verification, immediately the result is ready.

ADDRESS RESPONSE PAYLOAD

```json
{ 
  "data": { 
  "id" : "reports_424380ae-5e6a-425b-abcb-24e082e4a7a5", 
  "report": {
    "id": "381b87f0-f496-4052-a98e-8cb4c52b5fce",
    "reference_id": "5a1d27d09163d",
    "candidate": {
      "id": "34ae16a6-a527-4759-8d66-fe5d27a4361b",
      "reference_id": "YV5a1d27c8c1d16",
      "name": "Akomolafe Tosin",
      "first_name": "Tosin",
      "last_name": "Akomolafe",
      "middle_name": "",
      "email": "gettosin4me@gmail.com",
      "mobile": "08091213344",
      "has_live_photo": true,
      "live_photo_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg"
    },
    "start_time": "2018-03-06",
    "end_time": "2018-03-08",
    "execution_date": "2019-02-26 17:54:03",
    "revalidation_date": "2018-06-08",
    "status": "canceled",
    "task_status": "VERIFIED",
    "task_created_by": "Chinook Developer",
    "package": "live_photo",
    "download_url": null,
    "description": "",
    "package_name": "Live Photo Address Verification",
    "details": {
      "uuid": "fa234602-49f6-48ec-9a8f-aaa569109eb7",
      "address_id": 1,
      "candidate_id": 1,
      "photo_url": null,
      "status": "VERIFIED",
      "reason_for_fail": null,
      "deleted_at": null,
      "created_at": "2017-11-28 10:09:36",
      "updated_at": "2018-02-13 15:50:59",
      "images": [
        {
          "id": 1,
          "uuid": "4cc6361e-791e-44c0-b797-9261fcc47a0c",
          "live_photo_id": 1,
          "candidate_id": 1,
          "image_type": "image/jpeg",
          "image_extension": "jpeg",
          "path": "/",
          "image_name": "photo5a1d27d0798da1087.jpeg",
          "deleted_at": null,
          "created_at": "2017-11-28 10:09:36",
          "updated_at": "2017-11-28 10:09:36",
          "image_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg"
        }
      ],
      "address": {
        "uuid": "73df8ed4-6d35-446a-8af0-54b60b88153a",
        "user_id": 1,
        "user_type": "partner",
        "candidate_id": 1,
        "flat_number": "",
        "building_name": "",
        "building_number": "13B",
        "sub_street": "",
        "street": "Bishop street",
        "landmark": "",
        "state": "Lagos",
        "city": "Ilupeju",
        "post_code": "",
        "country": "Nigeria",
        "longitude": "3.3598313",
        "latitude": "6.551594499999999",
        "what3words": "outdone.sprain.times",
        "what3words_map": "http://w3w.co/outdone.sprain.times",
        "agent_geo": "",
        "start_date": "",
        "end_date": "",
        "status": "PENDING",
        "reason_for_fail": null,
        "item_id": "0",
        "item_type": "live_photo",
        "created_at": "2017-11-28 10:09:36",
        "updated_at": "2017-11-28 10:09:36",
        "formatted": "13b, Bishop  Street, Ilupeju, Lagos, Nigeria, ",
        "map_format": "13b Bishop Street, Ilupeju , Lagos, Nigeria",
        "map_address_url": null,
        "map_geolocation_url": null
      },
      "live_photos": [
        {
          "id": 1,
          "uuid": "4cc6361e-791e-44c0-b797-9261fcc47a0c",
          "live_photo_id": 1,
          "candidate_id": 1,
          "image_type": "image/jpeg",
          "image_extension": "jpeg",
          "path": "/",
          "image_name": "photo5a1d27d0798da1087.jpeg",
          "deleted_at": null,
          "created_at": "2017-11-28 10:09:36",
          "updated_at": "2017-11-28 10:09:36",
          "image_path": "http://api.youverify.local/uploads/tasks/livephoto/photo5a1d27d0798da1087.jpeg"
        }
      ]
    },
    "has_address": true,
    "notes": [
      {
        "id": 1,
        "report_id": 1000,
        "agent_id": 1,
        "note": "This address is verified. It is a bluish green duplex with gray gate. Confirmed by security.",
        "created_at": "2018-02-13 15:51:08",
        "updated_at": "2018-02-13 15:51:08",
        "formatted_time": "13 Feb, 2018 03:51:pm"
      },
      {
        "id": 2,
        "report_id": 1000,
        "agent_id": 1,
        "note": "This address is verified. It is a bluish green duplex with gray gate. Confirmed by security.",
        "created_at": "2018-02-13 15:51:08",
        "updated_at": "2018-02-13 15:51:08",
        "formatted_time": "13 Feb, 2018 03:51:pm"
      },
      {
        "id": 3,
        "report_id": 1000,
        "agent_id": 1,
        "note": "This address is verified. It is a bluish green duplex with gray gate. Confirmed by security.",
        "created_at": "2018-02-13 15:51:08",
        "updated_at": "2018-02-13 15:51:08",
        "formatted_time": "13 Feb, 2018 03:51:pm"
      }
    ],
    "signature": [
      "iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAC0ElEQVRIibWVMWgTURjHf+9yOUPPEIu0NClKqg5C6RJFoYOISDft5NAxoFPJIAqKi3UpOjkUcXDIJA46uGQpKi46VGmG0iqCNLa2DYUGY5t6Jtd3Dt7Vd68Xi0I/eLz3uPv+/+9773v/D/bYxC7fjTZrANlmHTJzF2BDGzpBMNoSRRGogKY/DGUOgFxlDtY7SHQCHdhKDaYO9FzqKcTs2JAwRRbAc73KVmNrsvq0OlF/W/8GNBWiEIloA24BVvZm9px91L4vTJGJyBTP9ZYbnxtXK3crr3ySgGj76HSCADyRvZE9bx+3nwgEue4c+YE8/Qf7AZhdm6U4U2R6dRoPj8bHxkjlXuUF4GgkxLTo48C+5IlkV9dQ12NhiOTlgcuMnxmnL9WHHbex4zbZVJbhY8O40qW8WiZ+ID7oLDvPmitNh/DFe3oZmoCVHkmPClNkct05CrkChtALCAxhUMgVyHXnEKbIpEfSo372ajFElqNpJs3zAPmBfCS4SpIfyAPg+5hoZR2VgSlMcRjYPvO/WfCP76OWdSgDdd8+5N1th38kmGzJr/C7Wnaz4J/AJ4oxhA1It+a+BijOFJFeW5lBepLiTBEA30eXjlCZCn82nUXnU+p06mLVqe53pcup9CmECOui9CQT0xOU5kvIpqwuPly83lprfef3W2gFZDHFR/iEsdZaS1oZ60viUOJCebXM1MoUnYlO7LjNZmuTd9V3jL0ZozRfwsOjPlW/VpusfeDPQ2sBW4AXhBVcjgUkgA5gf++V3rOpk6nbhmX0RB5RU1br7+t3lh4tvQY2gE2FJJSBFwWwPr2+tDG3Ueo40oGwRFLERAcernRkpVltPl94sHCr9rI25wP/AH4q0UdqUUjs/GwSyl6V60DcHCXqHWKnynVw+6rkBnqvPyC1D6jAIXA9Az2T/2k4O8q0XU/+15YZ2c3+RqAT6WsdrP1r3Gv7BW4wIvqstIdzAAAAAElFTkSuQmCC"
    ],
    "is_flagged": 1,
    "reportable_id": "fa234602-49f6-48ec-9a8f-aaa569109eb7",
    "created_at": "2017-11-28 10:09:36",
    "last_updated_at": "2019-02-26 17:54:03",
    "what3words": "NULL",
    "what3words_map_link": "NULL",
    "digital_address_code": "NULL",
    "digital_address_url": "NULL",
    "map_address_url": null,
    "map_geolocation_url": null,
    "report_geolocation_url": null,
    "report_longitude": null,
    "report_latitude": null,
    "can_view_report": true,
    "reasons_for_failure": [
      "Address does not exist",
      "Address not accessible",
      "Candidate does not live there"
    ],
    "submission_distance_in_meters": 0,
    "images": {
      "data": []
    },
  "status" : "completed | failed", 
  "task_status" : "NOT VERIFIED | VERIFIED", 
  "package_name" : "Live Photo Address Verification | Reference Check | Merchant Verification", 
  "candidate_id" : 3388, 
  "package" : "live_photo | reference_check | merchant_verification", 
  "is_flagged" : "0 | 1"
  } 
}
}
```

NB: Please note that that the above symbol " | " is used to differentiate the possible outcomes.

## Error Codes

Below are the error codes our systems will generate.

| **Codes** | **Error Messages**                                                                                                                                                                                     | **What it means**                                                                                   |
| :-------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------- |
| 422       | {<br/>    "message": "422 Unprocessable Entity",<br/>    "errors": {<br/>        "report_type": [            "The report type field is required."        ]<br/>    },<br/>    "status_code": 422<br/>} | Unprocessible Entity-Validity Error. The sent an invalid payload. IT does not meet validation rule. |
| 400       | {<br/>    "message": "400 Bad Request",<br/>    "status_code": 400<br/>}                                                                                                                               | Bad Request - The client has sent a bad request, usually a wrong ID format.                         |
| 400       | {<br/>    "message": "You are low on credit",<br/>    "status_code": 400<br/>}                                                                                                                         | Insufficient fund-The client does not enough funds in their account.                                |
| 500       | {<br/>     "message": "The server could not handle the request ",<br/>     "status_code": 500<br/>}                                                                                                    | Internal Server Error - The server encountered an error while processing the request.               |
| 404       | {<br/>    "message": "404 Not Found",<br/>    "status_code": 404<br/>}                                                                                                                                 | Not Found - The ID number doesn’t exist.                                                            |
| 401       | {<br/>    "message": "Token does not exist",<br/>    "status_code": 401<br/>}                                                                                                                          | Token does not exist. Token was not properly referenced.                                            |
| 403       | {<br/>    "message": "Insufficient Fund",<br/>    "status_code": 403<br/>}                                                                                                                             | Insufficient fund-The client does not enough funds in their account.                                |
| 503       | {<br/>    "message": "Service Unavailable",<br/>    "status_code": 503<br/>}                                                                                                                           | Connection error-The service is currently unavailable. Try again later.                             |
| 504       | {<br/>    "message": "Unable to Connect to FRSC service provider",<br/>    "status_code": 504<br/>}                                                                                                    | Service downtime-The service is currently unavailable. Try again later.                             |
