---
weight: 2
title: "AutoComplete"
---

AutoComplete searches is a more minimalistic way of searching; Ideal for dropdown lists, helping the user input the correct search words.

{{< hint info >}}
There are two ways you may make a Autocomplete request. GET or POST.
{{< /hint >}}

## Parameters

| Parameter   |Type| Description                                     |
| ----------- |----|-------------------------------------------------|
| customerId  |int |Your customer id                                 | 
| engineId    |int |The id of the search engine to use for the search| 

## Query Parameters
| Parameter   |Type |Description                                      |
| ----------- |--|-------------------------------------------------|
| query       |string |The string query to search for                   | 
| responsetype|string |the format to return the search results in       | 


## GET REQUEST

{{< markdown-with-header title="HTTP GET request" content="">}}
```
GET https://api.cludo.com/api/v3/{customerId}/{engineId}/autocomplete?query={query}&responsetype={responseType}}
```
{{< /markdown-with-header >}} 



**Curl Example**

```
curl 
-X GET \
-I -G https://api.cludo.com/api/v3/{customerId}/{engineId}/autocomplete \
-u {customerId}:{API_Key} \
-d query={query} \
-d responsetype={responseType} \
-d filters={filters} \
-d results={results} \
```





{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

## POST REQUEST
{{< markdown-with-header title="HTTP POST request" content="">}}
```
POST https://api.cludo.com/api/v3/{customerId}/{engineId}/autocomplete
```
{{< /markdown-with-header >}} 

**Curl Example**

```
curl 
curl 
-X POST \
-I https://api.cludo.com/api/v3/{customerId}/{engineId}/autocomplete \
-u {customerId}:{API_Key} \
-H "Content-Type: application/json" \
-d <JSON BODY> \
```

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

## TRY IT
{{< swagger-op operation="AutoComplete" >}}




## HTTP response

Depending on the responseType set in the request, different types of responses may be received.

### Not specified response

If no response type is set, then an array of titles will be returned

### JsonHtml response

Parameter Type Description QueryId string A random string identifying the search query. ResponseTime uint64 The time in milliseconds it took the Cludo servers to make the search. TotalResults uint32 The total amount of matches found. TotalSuggestions uint32 The total amount of suggestions. Facets string The html generated string of the facets, created with the template set in the request. SearchResult string The html generated string of the search results, created with the template set in the request.

{{< markdown-with-header title="HTTP response" content="An example of a HTTP response with no response type:">}}
```
[
    "Feats",
    "Feets",
    "Features"
]
```
{{< /markdown-with-header >}} 

{{< markdown-with-header title="HTTP response" content="Full JsonHtml HTTP response example:">}}
```
{
  "QueryId": "c77f19d9a4b243b182466ca31cf9848c",
  "ResponseTime": 40,
  "TotalResults": 8,
  "TotalSuggestions": 2,
  "Facets": "<A HTML STRING>",
  "SearchResult": "<A HTML STRING>"
}]
```
{{< /markdown-with-header >}} 