# Preface
This API is for use with internal, approved applications. To access this API you must authenticate using HTTP Basic Authorization.

# Response Format
Before we get into the API, we must define how data is passed from the server back to the client. Every response from the server is wrapped in a common JSON object with the following fields:
#### JSON Object Properties
Property | Description
-------- | -----------
`err` | This property contains a string or an array of strings. These strings contain information about errors with the request. This property will be `null` if there were no errors while processing the request.
`data` | This property contains the server's response data. What this property contains depends on the API used for the request. This property will be `null` if there were errors while processing the request.
`details` | This property may contain additional information relating to the response. Some API endpoints do not utilize this property, so it may not be present.

# GET Requests
## Query
API Method: `GET`

API Location: `/[table]/paginate`

This API is used to query the database. It supports server-side pagination,
filtering, and sorting. Pagination should be used if requests are made
frequently to reduce latency and server load. You can specify your query with
the following parameters:
#### Query Parameters
Parameter | Required | Default Value | Description 
--------- | -------- | ------------- | -----------
`filter` | No | *None* | May contain a string specifying a filter to apply to the query. This filter will be checked against every field. If no filter is provided, the query will return all table entries.
`sortBy` | No | `Legacy ID` | May contain a string specifying the field to be used for sorting.
`sortDirection` | No | `ascending` | May contain a string specifying the direction of the sorting. The string must have a value of `ascending`, `asc`, `descending`, or `desc`.
`pageIndex` | No | `1` | May contain a positive integer specifying the index of the page to retrieve in the query. Page indexes start at 1.
`numItems` | No | `10` | May contain a positive integer specifying the number of items each page in the query should contain.

This API will return a JSON object with the following properties:
#### Data Object
Property | Description
-------- | -----------
`docs` | Contains an array of table entries as JSON objects. These objects have different fields depending on the table type (see [Data Types](#data-types)).
`total` | Contains an integer sppecifying the total number of entries that matched the query.
`limit` | Contains the total number of items in each page.
`page` | Contains the current page index.
`pages` | Contains the total number of pages in the query.

### Usage
#### *cURL*
```bash
curl --location --request GET \
  --header "X-Username: My App" \
  "api.workday-account-translator.usc.edu/accounts/paginate"
```
#### *Python (requests)*
```python
import requests

r = requests.get( url = "http://api.workday-account-translator.usc.edu/api/accounts/paginate",
                  headers = {
                    "X-Username": "My App"
                  }
                )
print("Result Body: ")
print(r.json())
```
#### *Javascript (jQuery)*
```javascript
$.ajax({
    url: "http://api.workday-account-translator.usc.edu/api/accounts/paginate",
    type: "GET",
    headers: {"X-Username": "My App"},
    success: function( data) {
       alert('Result Body: ' + data);
    }
});
```

### Results
#### Result Body on Success:
```json
{
    "err": null,
    "data": {
        "docs": [
            {
                "Legacy System": "Unknown",
                "Status": "Active",
                "_id": "5d1cce88232d6c4f02ea4563",
                "Legacy ID": "1000000000",
                "Account Type": "1",
                "Capital": "1",
                "Company Worktag": "1",
                "Cost Center Description": "1",
                "Cost Center Worktag": "1",
                "Currency": "1",
                "Fund Description": "1",
                "Fund Legacy": "1",
                "Fund Worktag": "1",
                "Gift Type": "1",
                "Hierarchy 1": "1",
                "Hierarchy 2": "1",
                "Hierarchy 3": "1",
                "Hierarchy 4": "1",
                "Legacy Description": "[TEST] this is a description",
                "Organization Code Legacy": "1000000000",
                "Workday Description": "1",
                "Workday ID": "1"
            },
            {
                "Legacy System": "Unknown",
                "Status": "Active",
                "_id": "5d1cce88232d6c4f02ea4564",
                "Legacy ID": "2000000000",
                "Account Type": "2",
                "Capital": "2",
                "Company Worktag": "2",
                "Cost Center Description": "2",
                "Cost Center Worktag": "2",
                "Currency": "2",
                "Fund Description": "2",
                "Fund Legacy": "2",
                "Fund Worktag": "2",
                "Gift Type": "2",
                "Hierarchy 1": "2",
                "Hierarchy 2": "2",
                "Hierarchy 3": "2",
                "Hierarchy 4": "2",
                "Legacy Description": "[TEST] THIS IS A DESCRIPTION",
                "Organization Code Legacy": "2000000000",
                "Workday Description": "2",
                "Workday ID": "2"
            },
            {
                "Legacy System": "Unknown",
                "Status": "Active",
                "_id": "5d1cce88232d6c4f02ea4565",
                "Legacy ID": "3000000000",
                "Account Type": "3",
                "Capital": "3",
                "Company Worktag": "3",
                "Cost Center Description": "3",
                "Cost Center Worktag": "3",
                "Currency": "3",
                "Fund Description": "3",
                "Fund Legacy": "3",
                "Fund Worktag": "3",
                "Gift Type": "3",
                "Hierarchy 1": "3",
                "Hierarchy 2": "3",
                "Hierarchy 3": "3",
                "Hierarchy 4": "3",
                "Legacy Description": "[TEST] 3",
                "Organization Code Legacy": "3000000000",
                "Workday Description": "3",
                "Workday ID": "3"
            },
            {
                "Legacy System": "Unknown",
                "Status": "Inactive",
                "_id": "5d1cce88232d6c4f02ea4566",
                "Legacy ID": "4000000000",
                "Account Type": "4",
                "Capital": "4",
                "Company Worktag": "4",
                "Cost Center Description": "4",
                "Cost Center Worktag": "4",
                "Currency": "4",
                "Fund Description": "4",
                "Fund Legacy": "4",
                "Fund Worktag": "4",
                "Gift Type": "4",
                "Hierarchy 1": "4",
                "Hierarchy 2": "4",
                "Hierarchy 3": "4",
                "Hierarchy 4": "4",
                "Legacy Description": "[TEST] 4",
                "Organization Code Legacy": "4000000000",
                "Workday Description": "4",
                "Workday ID": "4"
            },
            {
                "Legacy System": "Unknown",
                "Status": "Inactive",
                "_id": "5d1cce88232d6c4f02ea4567",
                "Legacy ID": "5000000000",
                "Account Type": "5",
                "Capital": "5",
                "Company Worktag": "5",
                "Cost Center Description": "5",
                "Cost Center Worktag": "5",
                "Currency": "5",
                "Fund Description": "5",
                "Fund Legacy": "5",
                "Fund Worktag": "5",
                "Gift Type": "5",
                "Hierarchy 1": "5",
                "Hierarchy 2": "5",
                "Hierarchy 3": "5",
                "Hierarchy 4": "5",
                "Legacy Description": "[TEST] 5",
                "Organization Code Legacy": "5000000000",
                "Workday Description": "5",
                "Workday ID": "5"
            }
        ],
        "total": 5,
        "limit": 10,
        "page": 1,
        "pages": 1
    }
}
```
#### Result Body on Failure:
```json
{
    "err": "An error occurred on the server. The error details will be here.",
    "data": null
}
```

## Verify
API Method: `GET`

API Location: `/[table]/verify`

This API is used to verify whether or not the given value is unique in the
database. This is useful for form validation, since it only supports one
value at a time. You can provide data to validate through the following query
parameters:
#### Query Parameters
Parameter | Required | Default Value | Description
--------- | -------- | ------------- | -----------
`column` | Yes | *None* | Should contain a string specifying the field in the table to check against.
`value` | Yes | *None* | Should contain a string specifying the value to validate.

This API will return a boolean which will be **True** if the value was not
present in the database. If the value was already present, the boolean will be
**False**.
### Usage
#### *cURL*
```bash
curl --location --request GET \
--header "X-Username: My App" \
"api.workday-account-translator.usc.edu/api/accounts/verify?column=Legacy%20ID&value=1234567890"
```
#### *Python (requests)*
```python
import requests

r = requests.get( url = "http://api.workday-account-translator.usc.edu/api/accounts/verify",
                  headers = {
                    "X-Username": "My App",
                    "Comment": "This is an example from the API Documents."
                  },
                  params = {
                    "column": "Legacy ID",
                    "value": "1234567890"
                  }
                )
print("Result Body: ")
print(r.json())
```
#### *Javascript (jQuery)*
```javascript
$.ajax({
    url: "http://api.workday-account-translator.usc.edu/api/accounts/verify",
    method: "GET",
    headers: {"X-Username": "My App", "Comment": "This is an example from the API Documents"},
    data: {"column": "Legacy ID", "value": "1234567890"},
    success: function(data) {
       alert('Result Body: ' + data);
    }
});
```
### Results
#### Result Body on Success:
```json
{
    "err": null,
    "data": true
}
```
#### Result Body on Failure:
```json
{
    "err": "An error occurred on the server. The error details will be here.",
    "data": null
}
```

# POST Requests
## Advanced Query
API Method: `POST`

API Location: `/[table]/paginate`

This API is an extension of the [Query API](#Query) which gives access to
multiple, field-specific filters. These filters may contain regular expressions
and may be case-sensitive. In addition to the query parameters specified in the
[Query API](#Query), you may specify advanced filters in the request body
formatted as a JSON objects. This JSON object is formatted such that the
property key is the field the filter applies to and the property value is an
advanced filter object:
#### Advanced Filter Object
Property | Description
-------- | -----------
`filter` | Should contain a string specifying the value or regular expression to check against the field
`regex` | Should contain a boolean specifying whether the filter is a regular expression. See the [MongoDB Regex documentation](https://docs.mongodb.com/manual/reference/operator/query/regex/) for more information on regular expressions. if this property is missing, the value is assumed to be false.
`casesensitive` | Should contain a boolean specifying whether the filter should be treated as case sensitive. If this property is missing, the value is assumed to be false.

Note that because the JSON object can only have one property for each field in
the table, only one filter can be applied to each field at a time.

### Usage
#### *cURL*
```bash
curl --location --request POST \
  --header "X-Username: My App, Content-Type: application/json" \
  --data '{"Legacy Description": {filter: "description", regex: "false", casesensitive: "true"}}'
  "api.workday-account-translator.usc.edu/api/accounts/paginate"
```
#### *Python (requests)*
```python
import requests

r = requests.post(  url = "http://api.workday-account-translator.usc.edu/api/accounts/paginate",
                    headers = {
                      "X-Username": "My App",
                      "Comment": "This is an example from the API Documents.",
                      "Content-Type": "application/json"
                    },
                    data = {
                      "Legacy Description": {
                        "filter": "description",
                        "regex": "false",
                        "casesensitive": "true"
                      }
                    }
                  )
print("Result Body: ")
print(r.json())
```
#### *Javascript (jQuery)*
```javascript
$.ajax({
    url: "http://api.workday-account-translator.usc.edu/api/accounts/paginate",
    method: "POST",
    headers: {"X-Username": "My App", "Comment": "This is an example from the API Documents", "Content-Type": "application/json"},
    data: {"Legacy Description": {"filter": "description", "regex": "false", "casesensitive": "true"}},
    success: function(data) {
       alert('Result Body: ' + data);
    }
});
```
### Results
#### Result Body on Success:
```json
{
    "err": null,
    "data": {
        "docs": [
            {
                "Legacy System": "Unknown",
                "Status": "Active",
                "_id": "5d1cce88232d6c4f02ea4563",
                "Legacy ID": "1000000000",
                "Account Type": "1",
                "Capital": "1",
                "Company Worktag": "1",
                "Cost Center Description": "1",
                "Cost Center Worktag": "1",
                "Currency": "1",
                "Fund Description": "1",
                "Fund Legacy": "1",
                "Fund Worktag": "1",
                "Gift Type": "1",
                "Hierarchy 1": "1",
                "Hierarchy 2": "1",
                "Hierarchy 3": "1",
                "Hierarchy 4": "1",
                "Legacy Description": "[TEST] this is a description",
                "Organization Code Legacy": "1000000000",
                "Workday Description": "1",
                "Workday ID": "1"
            }
        ],
        "total": 1,
        "limit": 10,
        "page": 1,
        "pages": 1
    }
}
```
#### Result Body on Failure:
```json
{
    "err": "An error occurred on the server. The error details will be here.",
    "data": null
}
```

## Create or Update
API Method: `POST`

API Location: `/[table]`

This API is used to insert new entries or update existing ones in the table.
You can provide entries via an array of JSON objects in the body of the
request. These JSON objects should contain properties for each of the fields in
the table (see [Data Types](#data-types)). There is no upper limit to the
number of entries that can be sent via this request, but more entries could
take longer to process.

This API returns a JSON object containing the following properties:
#### Data Object
Property | Description
-------- | -----------
`successfulRows` | Contains an array of *`Legacy IDs`* which were successfully added to the database
`errorRows` | Contains an array of *`Legacy IDs`* which were not added to the database

This API does not give any information about failed inserts or updates. To
figure out errors whether your data has errors, please use the
[Process API](#Process).

### Usage
#### *cURL*
```bash
curl --location --request POST \
  --header "X-Username: My App, Content-Type: application/json" \
  --data '[{
          		"Legacy ID": "1111111111",
          		"Legacy Description": "This is an example entry for the accounts table",
          		"Fund Legacy": "example",
          		"Organization Code Legacy": "1111111111",
          		"Workday ID": "WD567",
          		"Workday Description": "This is an example entry for the accounts table",
          		"Status": "Active",
          		"Account Type": "example",
          		"Capital": "example",
          		"Gift Type": "example",
          		"Currency": "example",
          		"Company Worktag": "example",
          		"Fund Worktag": "example",
          		"Fund Description": "example",
          		"Cost Center Worktag": "example",
          		"Cost Center Description": "example",
          		"Hierarchy 1": "example",
          		"Hierarchy 2": "example",
          		"Hierarchy 3": "example",
          		"Hierarchy 4": "example"
          }]'
  "api.workday-account-translator.usc.edu/api/accounts"
```
#### *Python (requests)*
```python
import requests

r = requests.post(  url = "http://api.workday-account-translator.usc.edu/api/accounts",
                    headers = {
                      "X-Username": "My App",
                      "Comment": "This is an example from the API Documents.",
                      "Content-Type": "application/json"
                    },
                    data = [
                           	{
                           		"Legacy ID": "1111111111",
                           		"Legacy Description": "This is an example entry for the accounts table",
                           		"Fund Legacy": "example",
                           		"Organization Code Legacy": "1111111111",
                           		"Workday ID": "WD567",
                           		"Workday Description": "This is an example entry for the accounts table",
                           		"Status": "Active",
                           		"Account Type": "example",
                           		"Capital": "example",
                           		"Gift Type": "example",
                           		"Currency": "example",
                           		"Company Worktag": "example",
                           		"Fund Worktag": "example",
                           		"Fund Description": "example",
                           		"Cost Center Worktag": "example",
                           		"Cost Center Description": "example",
                           		"Hierarchy 1": "example",
                           		"Hierarchy 2": "example",
                           		"Hierarchy 3": "example",
                           		"Hierarchy 4": "example"
                           	}
                          ]
                  )
print("Result Body: ")
print(r.json())
```
#### *Javascript (jQuery)*
```javascript
$.ajax({
    url: "http://api.workday-account-translator.usc.edu/api/accounts",
    method: "POST",
    headers: {"X-Username": "My App", "Comment": "This is an example from the API Documents", "Content-Type": "application/json"},
    data: [{
           		"Legacy ID": "1111111111",
           		"Legacy Description": "This is an example entry for the accounts table",
           		"Fund Legacy": "example",
           		"Organization Code Legacy": "1111111111",
           		"Workday ID": "WD567",
           		"Workday Description": "This is an example entry for the accounts table",
           		"Status": "Active",
           		"Account Type": "example",
           		"Capital": "example",
           		"Gift Type": "example",
           		"Currency": "example",
           		"Company Worktag": "example",
           		"Fund Worktag": "example",
           		"Fund Description": "example",
           		"Cost Center Worktag": "example",
           		"Cost Center Description": "example",
           		"Hierarchy 1": "example",
           		"Hierarchy 2": "example",
           		"Hierarchy 3": "example",
           		"Hierarchy 4": "example"
          }],
    success: function(data) {
       alert('Result Body: ' + data);
    }
});
```
### Results
#### Result Body on Success:
```json
{
    "err": null,
    "details": {
        "successfulRows": [
            "1111111111",
            "0000000000"
        ],
        "errorRows": []
    }
}
```
#### Result Body on Failure:
```json
{
    "err": "An error occurred on the server. The error details will be here.",
    "data": null
}
```

## Process
API Method: `POST`

API Location: `/[table]/process`

This API is used to validate mass quantities of entries before importing them
into the database. You can provide entries via a CSV file or an array of JSON
objects in the body of the request. These JSON objects should contain
properties for each of the fields in the table (see [Data Types](#data-types)).
If a CSV file is sent through this request, it will automatically be parsed.
There is no upper limit to the number of entries that can be sent via this
request, but more entries could take longer to process.

This API returns an array of entries as JSON objects, as well as additional
information for determining any issues with the data. Assuming there were no
errors found in the data, this array of JSON objects is compatible with the
[Create or Update API](#create-or-update). The additional information is
contained in the `details` portion of the response data with the following
properties: 
#### Details Object Properties
Property | Description
-------- | -----------
`fileName` | Contains the name of the CSV file sent through the API. If no CSV file was sent, this property will be `null`.
`totalNumOfRows` | Contains an integer specifying the total number of rows sent through the API.
`totalNumOfRowsInError` | Contains an integer specifying the total number of rows that have errors.
`rowsInError` | Contains an array of *`Legacy ID`* strings representing the rows which have errors. If there are no rows with errors, this property will be `null`.
`alreadyInSQL` | Contains an array of *`Legacy ID`* strings representing the rows which already exist in the database. If there are no rows that already exist, this property will be `null`.

### Usage
#### *cURL*
```bash
curl --location --request POST \
  --header "X-Username: My App, Content-Type: application/json" \
  --data '[
           {
             "Legacy ID": "1111111111",
             "Legacy Description": "This is an example entry for the accounts table",
             "Fund Legacy": "example",
             "Organization Code Legacy": "1111111111",
             "Workday ID": "WD5678",
             "Workday Description": "This is an example entry for the accounts table",
             "Status": "Active",
             "Account Type": "example",
             "Capital": "example",
             "Gift Type": "example",
             "Currency": "example",
             "Company Worktag": "example",
             "Fund Worktag": "example",
             "Fund Description": "example",
             "Cost Center Worktag": "example",
             "Cost Center Description": "example",
             "Hierarchy 1": "example",
             "Hierarchy 2": "example",
             "Hierarchy 3": "example",
             "Hierarchy 4": "example"
           },
           {
             "Legacy ID": "0000000000",
             "Legacy Description": "This is an example entry for the accounts table",
             "Fund Legacy": "example",
             "Organization Code Legacy": "0000000000",
             "Workday ID": "WD1234",
             "Workday Description": "This is an example entry for the accounts table",
             "Status": "Active",
             "Account Type": "example",
             "Capital": "example",
             "Gift Type": "example",
             "Currency": "example",
             "Company Worktag": "example",
             "Fund Worktag": "example",
             "Fund Description": "example",
             "Cost Center Worktag": "example",
             "Cost Center Description": "example",
             "Hierarchy 1": "example",
             "Hierarchy 2": "example",
             "Hierarchy 3": "example",
             "Hierarchy 4": "example"
           }
         ]' \
  "api.workday-account-translator.usc.edu/api/accounts/process"
```
#### *Python (requests)*
```python
import requests

r = requests.post(  url = "http://api.workday-account-translator.usc.edu/api/accounts/process",
                    headers = {
                      "X-Username": "My App",
                      "Comment": "This is an example from the API Documents.",
                      "Content-Type": "application/json"
                    },
                    data = [
                              {
                                "Legacy ID": "1111111111",
                                "Legacy Description": "This is an example entry for the accounts table",
                                "Fund Legacy": "example",
                                "Organization Code Legacy": "1111111111",
                                "Workday ID": "WD5678",
                                "Workday Description": "This is an example entry for the accounts table",
                                "Status": "Active",
                                "Account Type": "example",
                                "Capital": "example",
                                "Gift Type": "example",
                                "Currency": "example",
                                "Company Worktag": "example",
                                "Fund Worktag": "example",
                                "Fund Description": "example",
                                "Cost Center Worktag": "example",
                                "Cost Center Description": "example",
                                "Hierarchy 1": "example",
                                "Hierarchy 2": "example",
                                "Hierarchy 3": "example",
                                "Hierarchy 4": "example"
                              },
                              {
                                "Legacy ID": "0000000000",
                                "Legacy Description": "This is an example entry for the accounts table",
                                "Fund Legacy": "example",
                                "Organization Code Legacy": "0000000000",
                                "Workday ID": "WD1234",
                                "Workday Description": "This is an example entry for the accounts table",
                                "Status": "Active",
                                "Account Type": "example",
                                "Capital": "example",
                                "Gift Type": "example",
                                "Currency": "example",
                                "Company Worktag": "example",
                                "Fund Worktag": "example",
                                "Fund Description": "example",
                                "Cost Center Worktag": "example",
                                "Cost Center Description": "example",
                                "Hierarchy 1": "example",
                                "Hierarchy 2": "example",
                                "Hierarchy 3": "example",
                                "Hierarchy 4": "example"
                              }
                          ]
                  )
print("Result Body: ")
print(r.json())
```
#### *Javascript (jQuery)*
```javascript
$.ajax({
    url: "http://api.workday-account-translator.usc.edu/api/accounts/process",
    method: "POST",
    headers: {"X-Username": "My App", "Comment": "This is an example from the API Documents", "Content-Type": "application/json"},
    data: [
            {
               "Legacy ID": "1111111111",
               "Legacy Description": "This is an example entry for the accounts table",
               "Fund Legacy": "example",
               "Organization Code Legacy": "1111111111",
               "Workday ID": "WD5678",
               "Workday Description": "This is an example entry for the accounts table",
               "Status": "Active",
               "Account Type": "example",
               "Capital": "example",
               "Gift Type": "example",
               "Currency": "example",
               "Company Worktag": "example",
               "Fund Worktag": "example",
               "Fund Description": "example",
               "Cost Center Worktag": "example",
               "Cost Center Description": "example",
               "Hierarchy 1": "example",
               "Hierarchy 2": "example",
               "Hierarchy 3": "example",
               "Hierarchy 4": "example"
            },
            {
               "Legacy ID": "0000000000",
               "Legacy Description": "This is an example entry for the accounts table",
               "Fund Legacy": "example",
               "Organization Code Legacy": "0000000000",
               "Workday ID": "WD1234",
               "Workday Description": "This is an example entry for the accounts table",
               "Status": "Active",
               "Account Type": "example",
               "Capital": "example",
               "Gift Type": "example",
               "Currency": "example",
               "Company Worktag": "example",
               "Fund Worktag": "example",
               "Fund Description": "example",
               "Cost Center Worktag": "example",
               "Cost Center Description": "example",
               "Hierarchy 1": "example",
               "Hierarchy 2": "example",
               "Hierarchy 3": "example",
               "Hierarchy 4": "example"
           }
         ],
    success: function(data) {
       alert('Result Body: ' + data);
    }
});
```

### Results
#### Result Body on Success:
```json
{
    "err": null,
    "data": [
        {
            "Legacy ID": "1111111111",
            "Legacy Description": "This is an example entry for the accounts table",
            "Fund Legacy": "example",
            "Organization Code Legacy": "1111111111",
            "Workday ID": "WD5678",
            "Workday Description": "This is an example entry for the accounts table",
            "Status": "Active",
            "Account Type": "example",
            "Capital": "example",
            "Gift Type": "example",
            "Currency": "example",
            "Company Worktag": "example",
            "Fund Worktag": "example",
            "Fund Description": "example",
            "Cost Center Worktag": "example",
            "Cost Center Description": "example",
            "Hierarchy 1": "example",
            "Hierarchy 2": "example",
            "Hierarchy 3": "example",
            "Hierarchy 4": "example"
        },
        {
            "Legacy ID": "0000000000",
            "Legacy Description": "This is an example entry for the accounts table",
            "Fund Legacy": "example",
            "Organization Code Legacy": "0000000000",
            "Workday ID": "WD1234",
            "Workday Description": "This is an example entry for the accounts table",
            "Status": "Active",
            "Account Type": "example",
            "Capital": "example",
            "Gift Type": "example",
            "Currency": "example",
            "Company Worktag": "example",
            "Fund Worktag": "example",
            "Fund Description": "example",
            "Cost Center Worktag": "example",
            "Cost Center Description": "example",
            "Hierarchy 1": "example",
            "Hierarchy 2": "example",
            "Hierarchy 3": "example",
            "Hierarchy 4": "example"
        }
    ],
    "details": {
        "fileName": null,
        "totalNumOfRows": 2,
        "totalNumOfRowsInError": 0,
        "rowsInError": null,
        "alreadyInSQL": [
            "0000000000"
        ]
    }
}
```
#### Result Body on Failure:
```json
{
    "err": "An error occurred on the server. The error details will be here.",
    "data": null
}
```

# DELETE Requests
## Delete
API Method: `DELETE`

API Location: `/[table]`

This API is used to remove entries from a table. The entry to remove is
specified by the following query parameter:
#### Query Parameters
Parameter | Required | Default Value | Description 
--------- | -------- | ------------- | -----------
`Legacy ID` | Yes | *None* | Should contain a specific *`Legacy ID`*, which represents the entry you want to remove.

This API returns an array of *`Legacy ID`* strings in the `details` portion of
the response, which represent the entries removed from the database.

### Usage
#### *cURL*
```bash
curl --location --request DELETE \
--header "X-Username: My App" \
"api.workday-account-translator.usc.edu/api/accounts?column=Legacy%20ID&value=1234567890"
```
#### *Python (requests)*
```python
import requests

r = requests.get( url = "http://api.workday-account-translator.usc.edu/api/accounts",
                  headers = {
                    "X-Username": "My App",
                    "Comment": "This is an example from the API Documents."
                  },
                  params = {
                    "Legacy ID": "0000000000"
                  }
                )
print("Result Body: ")
print(r.json())
```
#### *Javascript (jQuery)*
```javascript
$.ajax({
    url: "http://api.workday-account-translator.usc.edu/api/accounts/verify",
    method: "DELETE",
    headers: {"X-Username": "My App", "Comment": "This is an example from the API Documents"},
    data: {"Legacy ID": "0000000000"},
    success: function(data) {
       alert('Result Body: ' + data);
    }
});
```
### Results
#### Result Body on Success:
```json
{
    "err": null,
    "details": [
        "0000000000"
    ]
}
```
#### Result Body on Failure:
```json
{
    "err": "An error occurred on the server. The error details will be here.",
    "details": null
}
```

# HEAD Requests
Any `HEAD` request will simply echo back the headers sent to the server. This
allows your application to see gateway or proxy specific headers invisible to
the client.

# Data Types
The following sections detail the data fields in each of the tables in the database.
## `accounts` Table
- `Legacy ID` : 10 digit number
- `Legacy Description` : String
- `Fund Legacy` : String
- `Legacy System` : Enum - Can have a value of *`KFS`*, *`LAW`*, *`VHS`*, *`Workday`*, *`Other`*, or *`Unknown`*
- `Organization Code Legacy` : String
- `Workday ID` : String
- `Workday Description` : String
- `Status` : Enum - Can have a value of *`Active`* or *`Inactive`*
- `Account Type` : String
- `Capital` : String
- `Gift Type` : String
- `Currency` : String
- `Company Worktag` : String
- `Fund Worktag` : String
- `Fund Description` : String
- `Cost Center Worktag` : String
- `Cost Center Description` : String
- `Hierarchy 1` : String
- `Hierarchy 2` : String
- `Hierarchy 3` : String
- `Hierarchy 4` : String

## `Objects` Table
- `Legacy ID` : 10 digit number
- `Legacy Description` : String
- `Legacy System` : Enum - Can have a value of *`KFS`*, *`LAW`*, *`VHS`*, *`Workday`*, *`Other`*, or *`Unknown`*
- `Workday ID` : String
- `Workday Description` : String
- `Status` : Enum - Can have a value of *`Active`* or *`Inactive`*
- `Account Type` : String
- `Summary 1` : String
- `Summary 2` : String
- `Summary 3` : String

## `Organizations` Table
- `Legacy ID` : 10 digit number
- `Legacy Description` : String
- `Legacy System` : Enum - Can have a value of *`KFS`*, *`LAW`*, *`VHS`*, *`Workday`*, *`Other`*, or *`Unknown`*
- `Workday ID` : String
- `Workday Description` : String
- `Status` : Enum - Can have a value of *`Active`* or *`Inactive`*
- `Organization Subtype` : String
- `Restricted to Comp` : String
- `Hierarchy 1` : String
- `Hierarchy 2` : String
- `Hierarchy 3` : String
