# Errors

Selequity uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a charge failed, etc.), and codes in the 5xx range indicate an error with Selequity's servers (these are rare).

Generally, responses will only contain one error. Generally, the
HTTP response code will match the errors, but in cases where that's not
true, we need to make sure to document them here.

Error Code | Meaning
---------- | -------
200 | Validation Errors | The request was good, but the data was bad.
400 | Bad Request -- The request was unacceptable, often due to missing a required parameter.
401 | Unauthorized -- No valid API key provided.
402 | Request Failed -- The parameters were valid but the request failed.
404 | Not Found -- The requested resource doesn't exist.
429 | Too Many Requests -- Too many requests hit the API too quickly.
500, 502, 503, 504 | Internal Server Error -- We had a problem with our server. Try again later.


## The error object


FIELDS

```json
// HTTP 422
{
  "errors":[
    {
      "status": 422,
      "code": "RecordInvalid",
      "title": "Record Invalid",
      "detail": "Minimum investment cannot exceed maximum investment.",
      "parameter": [
        {
          "id": 3,
          "type": "investments"
        }
      ]
    }
  ]
}
```

A response will never contain both a data key and an errors key.

Name | Type | Description
---- | ---- | -----------
status | integer | the HTTP status code applicable to this problem, expressed as a string value.
code | string | an application-specific error code, expressed as a string value.
title | string | a short, human-readable summary of the problem that SHOULD NOT change from occurrence to occurrence of the problem, except for purposes of localization.
detail | string | a human-readable explanation specific to this occurrence of the problem. Like title, this field’s value can be localized.
parameter | string | extra information about any relevant parameters
meta | string | a meta object containing non-standard meta-information about the error.
