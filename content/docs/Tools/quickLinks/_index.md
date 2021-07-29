---
weight: 2
bookFlatSection: false
title: "QuickLinks"
---

Quicklinks are useful if you want to redirect your visitors to a specific url when they search for a pre-defined term.

{{< hint info >}}
 You can read more about quicklinks here. <a href="https://cludo.zendesk.com/hc/en-us/articles/115002466252-Quicklinks" target="_blank">here (Broken link)</a>.
{{< /hint >}}

## Data structures

### QuickLink

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the quicklink                       | 
| WebsiteId    |int | The ID of the engine the quicklink belongs to| 
| url	    |string | The URL to redirect to| 
| terms    |array | An array of terms| 

```
{
    "id": 5807805,
    "websiteId": 7578030,
    "url": "https://www.cludo.com/contact/",
    "terms": []
}
```

### Term

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| name           |string | The term that should trigger the redirect                       | 

```
{
    "name": "contact"
}
```

## Get quicklink

Get a specific quicklink.

### Request
```
GET https://api.cludo.com/api/quicklinks/<id>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the specific quicklink | 


{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/quicklinks/5807805"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT 
{{< swagger-op operation="GetQuicklinkById" >}}

### Response
Will return a single quicklink. See <a href="#quicklink">data structures</a>



## Get quicklink by engine

Get all quicklinks for a specific engine.

### Request
```
GET https://api.cludo.com/api/engine/<engineId>/quicklinks
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| engineId          |int | The ID of the specific engine | 


{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/engine/7578030/quicklinks"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT 
{{< swagger-op operation="GetQuicklinksByEngineId" >}}

### Response
Will return an array of quicklinks. See <a href="#quicklink">data structures</a>


## Get quicklink by engine and term

Get all quicklinks for a specific engine and term.

### Request
```
GET https://api.cludo.com/api/engine/<engineId>/quicklinkterms?searchword=<Term>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| engineId          |int | The ID of the specific engine | 

### Query Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| Term          |string | The specific term. | 



{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/engine/7578030/quicklinkterms?searchword=contact"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT 
{{< swagger-op operation="GetQuicklinksByEngineIdAndTerm" >}}

### Response
Will return an array of quicklinks. See <a href="#quicklink">data structures</a>


## Create quicklink

Create a quicklink.

### Request
```
POST https://api.cludo.com/api/quicklinks
```

### Body

{{< hint warning >}}
The id key must be omitted.
{{< /hint >}}

A single quicklink. See <a href="#quicklink">data structures</a>

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/quicklinks"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
           "websiteId": 7578030,
           "url": "https://www.cludo.com/contact/",
           "terms": [
               {
                   "name": "contact"
               }
           ]
       }'
```
{{< /markdown-with-header >}} 

{{< button relref="#try-it-create-or-update-quicklink" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

### Response
Will return the created quicklink. See <a href="#quicklink">data structures</a>

## Update quicklink

Update a specific quicklink.

### Request
```
PUT https://api.cludo.com/api/quicklinks/<id>

POST https://api.cludo.com/api/quicklinks
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the specific quicklink | 

### Body

{{< hint info >}}
The id key can be omitted with a PUT request, as it won't be respected.
{{< /hint >}}

{{< hint warning >}}
**Please note**   
The id key **must** be included with a POST request.
{{< /hint >}}

A single quicklink. See <a href="#quicklink">data structures</a>

{{< markdown-with-header title="Example with a POST">}}
```
curl "https://api.cludo.com/api/quicklinks"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
           "id": 5807805,
           "websiteId": 7578030,
           "url": "https://www.cludo.com/contact/",
           "terms": [
               {
                   "name": "contact"
               }
           ]
       }'
```
{{< /markdown-with-header >}} 

{{< markdown-with-header title="Example with a PUT">}}
```
curl "https://api.cludo.com/api/quicklinks/5807805"
    -X PUT
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
           "websiteId": 7578030,
           "url": "https://www.cludo.com/contact/",
           "terms": [
               {
                   "name": "contact"
               }
           ]
       }'
```
{{< /markdown-with-header >}} 

### TRY IT Create or Update QuickLink
{{< swagger-op operation="CreateOrUpdateQuicklink" >}}
{{< swagger-op operation="UpdateQuicklink" >}}

### Response
Will return the updated quicklink. See <a href="#quicklink">data structures</a>


## Delete quicklink

Delete a quicklink.

### Request
```
DELETE https://api.cludo.com/api/quicklinks/<id>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the specific quicklink | 


{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/quicklinks/5807805"
    -X DELETE
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 



### TRY IT
{{< swagger-op operation="DeleteQuicklink" >}}


