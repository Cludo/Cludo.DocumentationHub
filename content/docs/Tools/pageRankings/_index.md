---
weight: 1
bookFlatSection: false
title: "Page Rankings"
---

Page rankings are useful if you want to control the top search results for your visitors when they search for a pre-defined term.

{{< hint info >}}
You can read more about page rankings <a href="https://cludo.zendesk.com/hc/en-us/articles/115002451271-Page-Rankings" target="_blank">here Broken link</a>
{{< /hint >}}

## Data structures

### Ranking group

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the ranking group                       | 
| WebsiteId    |int | The ID of the engine the ranking group belongs to| 
| name	    |string | The name of the ranking group| 
| pages    |array | An array of **Ranked pages**| 
| rankingterms    |array | An array of **Terms**| 

```
{
    "id": 1689348,
    "WebsiteId": 7578030,
    "name": "Hello, World!",
    "pages": [],
    "rankingterms": []
}
```



### Ranked page
| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the ranked page                      | 
| WebsiteId    |int | The ID of the engine the ranked page belongs to| 
| RankingId	    |int | The ID of the ranking group the ranked page belongs to| 
| rank    |int | The rank of the ranked page| 
| showpage    |bool | Whether the ranked page should be included| 
| page    |**Page** | A **Page**| 

```
{
    "id": 6512590,
    "websiteid": 7578030,
    "RankingId": 1689348,
    "rank": 1,
    "showpage": true,
    "page": {}
}
```

### Page

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the page                      | 
| WebsiteId    |int | The ID of the engine the page belongs to| 
| pageid	    |string | The unique identifier of the page. Usually the URL but could be any string| 
| pageurl    |string | The URL of the page| 
| searchable    |bool | Whether the page is searchable| 
| url	    |string | Legacy, disregard| 
| website	    |string |Legacy, disregard| 

```
{
    "id": 9728711,
    "websiteid": 7578030,
    "pageid": "https://www.cludo.com/contact",
    "pageurl": "https://www.cludo.com/contact/",
    "searchable": true,
    "url": "http://cludo.com/9728711/",
    "website": "http://cludo.com/7578030/"
}
```

### Term

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the term                       | 
| RankingId	    |int | The ID of the ranking group this term belongs to| 
| name    |string | The actual term| 
 
```
{
    "id": 8720627,
    "rankingId": 1689348,
    "name": "hello"
}
```

### Indexed document

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| url           |string | The URL of the original resource                       | 
| title	    |string | The title of the original resource| 
| documentId    |string | The unique identifier of the document| 
| pageId    |int | Legacy, disregard| 
| hasPageId    |bool | Legacy, disregard| 
| isAddedAlready    |bool | Whether the document is already added to a ranking group| 

 
## Get all page rankings

Get all page rankings for the entire account.

### Request
```
GET https://api.cludo.com/api/rankings
```


{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/rankings"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT
{{< swagger-op operation="AllRankings" >}}

### Response
Will return an array of ranking groups. See <a href="#ranking-group">data structures</a>

## Get all page rankings by engine

Get all page rankings for a specific engine.

### Request
```
GET https://api.cludo.com/api/rankings/site/<engineID>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| engineId           |int | The ID of the specific engine                       | 

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/rankings/site/7578030"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT
{{< swagger-op operation="RankingsByEngine" >}}

### Response
Will return an array of ranking groups. See <a href="#ranking-group">data structures</a>

## Get single page ranking

Get a specific page ranking.

### Request
```
GET https://api.cludo.com/api/rankings/<id>
```
### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| id           |int | The ID of the specific page ranking                    | 

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/rankings/1689348"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT
{{< swagger-op operation="RankingsByPageRankingId" >}}

### Response
Will return an array of ranking groups. See <a href="#ranking-group">data structures</a>


## Get indexed documents

Get indexed documents for an engine by either title or URL similarity.

### Request
```
POST https://api.cludo.com/api/v3/<customerID>/<engineID>/search/alldocuments?filter=<Filter>&type=<Type>&functionType=<Function type>&page=<Page>&perpage=<Per page>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| customerID           |int | Your ID                      | 
| engineID	    |int | The ID of the specific engine| 
| Filter    |string | The search term| 
| Type    |string | How you want it to match on the filter. Either **any**, **title**, or **url**| 
| Function type|string    |In this context, this **must** be **pageranking**| 
| Page    |int | Used for pagination. If omitted, it will default to **1**| 
| Per page    |int | Used for pagination. If omitted, it will default to **25**| 


### Body
An array of unique identifiers for documents that you want to exclude from the results. Otherwise, just an empty array.

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/v3/9056485/7578030/search/alldocuments?filter=contact&type=title&functionType=pageranking&page=1&perpage=25"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '[
            "https://www.cludo.com/site-search-features",
            "https://www.cludo.com/intranet"
        ]'
```
{{< /markdown-with-header >}} 

### TRY IT
{{< swagger-op operation="AllDocuments" >}}

### Response
Will return an array of indexed documents. See <a href="#indexed-document">data structures</a>



## Create page ranking

Create a page ranking.

### Request
```
POST https://api.cludo.com/api/rankings
```

### Body

{{< hint warning >}}
The id key must be omitted.
{{< /hint >}}


{{< hint warning >}}
It's important that the pageid key is an exact match with the unique identifier we have for the document internally. It's usually the same as the URL, but it could be any string. See <a href="#get-indexed-documents">Get indexed documents</a>  for a way to obtain it.
{{< /hint >}}

A single ranking group. See <a href="#ranking-group">data structures</a> .

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/rankings"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
            "WebsiteId": 7578030,
            "name": "Hello, World!",
            "pages": [
                {
                    "websiteid": 7578030,
                    "rank": 1,
                    "showpage": true,
                    "page": {
                        "websiteid": 7578030,
                        "pageid": "https://www.cludo.com/contact",
                        "pageurl": "https://www.cludo.com/contact/",
                        "searchable": true
                    }
                }
            ],
            "rankingterms": [
                {
                    "name": "hello"
                }
            ]
        }'
```
{{< /markdown-with-header >}} 

{{< button relref="#try-it-create-or-update-page-ranking" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

### Response
Will return the created ranking group. See <a href="#ranking-group">data structures</a>



## Update page ranking

Update a specific page ranking.

### Request
```
PUT https://api.cludo.com/api/rankings/<Page ranking ID>

POST https://api.cludo.com/api/rankings
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| Page ranking ID           |int | The ID of the specific page ranking | 


### Body

{{< hint info >}}
The id key can be omitted with a PUT request, as it won't be respected.
{{< /hint >}}


{{< hint warning >}}
The id key must be included with a POST request.
{{< /hint >}}

{{< hint warning >}}
It's important that the pageid key is an exact match with the unique identifier we have for the document internally. It's usually the same as the URL, but it could be any string. See <a href="#get-indexed-documents">Get indexed documents</a>  for a way to obtain it.
{{< /hint >}}

A single ranking group. See <a href="#ranking-group">data structures</a> .



{{< markdown-with-header title="Example using a POST">}}
```
curl "https://api.cludo.com/api/rankings"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
            "WebsiteId": 7578030,
            "name": "Hello, World!",
            "pages": [
                {
                    "websiteid": 7578030,
                    "rank": 1,
                    "showpage": true,
                    "page": {
                        "websiteid": 7578030,
                        "pageid": "https://www.cludo.com/contact",
                        "pageurl": "https://www.cludo.com/contact/",
                        "searchable": true
                    }
                }
            ],
            "rankingterms": [
                {
                    "name": "hello"
                }
            ]
        }'

```
{{< /markdown-with-header >}} 

{{< markdown-with-header title="Example using a PUT">}}
```
curl "https://api.cludo.com/api/rankings/1689348"
    -X PUT
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
            "WebsiteId": 7578030,
            "name": "Hello, World!",
            "pages": [
                {
                    "websiteid": 7578030,
                    "rank": 1,
                    "showpage": true,
                    "page": {
                        "websiteid": 7578030,
                        "pageid": "https://www.cludo.com",
                        "pageurl": "https://www.cludo.com/",
                        "searchable": true
                    }
                },
                {
                    "id": 6512590,
                    "websiteid": 7578030,
                    "rank": 2,
                    "showpage": true,
                    "page": {
                        "id": 9728711,
                        "websiteid": 7578030,
                        "pageid": "https://www.cludo.com/contact",
                        "pageurl": "https://www.cludo.com/contact/",
                        "searchable": true
                    }
                }
            ],
            "rankingterms": [
                {
                    "id": 8720627,
                    "rankingId": 1689348,
                    "name": "hello"
                },
                {
                    "name": "world"
                }
            ]
        }'

```
{{< /markdown-with-header >}} 

### TRY IT Create or Update Page Ranking
{{< swagger-op operation="PageRankingCreationUpdate" >}}


{{< swagger-op operation="PageRankingUpdate" >}}

### Response
Will return the updated ranking group. See <a href="#ranking-group">data structures</a>




## Delete page ranking

Delete a specific page ranking.

### Request
```
DELETE https://api.cludo.com/api/rankings/<Page ranking ID>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| Page ranking ID           |int | The ID of the specific page ranking | 

```
curl "https://api.cludo.com/api/rankings/1689348"
    -X DELETE
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```

### TRY IT 
{{< swagger-op operation="PageRankingDelete" >}}