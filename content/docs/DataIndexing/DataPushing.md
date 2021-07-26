---
weight: 2
title: "Data Pushing"
---

If you don't have any crawlers setup, or know exactly how your data is stored, you may directly push search results into your data storage with this endpoint.

## HTTP request


```
POST https://api.cludo.com/api/v3/{CustomerId}/content/{CrawlerId}/push
```


## Parameters

| Parameter   |Type| Description                                     |
| ----------- |----|-------------------------------------------------|
| CustomerId  |int |Your customer id                                 | 
| CrawlerId   |int |The id of the crawler to index the data into| 

{{< markdown-with-header title="HTTP request" content="The command below indexes data directly:">}}
```
curl
-X POST \
-I https://api.cludo.com/api/v3/{CustomerId}/content/{CrawlerId}/push \
-u {CustomerId}:{API_Key} \
```
{{< /markdown-with-header >}} 

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}


## HTTP body

The body consists of result models of the data you wish to index. Each model consist of the field name with the associated value to set.

## Body Parameters

| Parameter   |Type   | Description                                     |
| ----------- |----   |-------------------------------------------------|
| Title       |string |The title of a search result                                | 
| Description   |string    |The description of a search result| 
| Type   |string    |Must be **PageContent** for pages and **FileContent** for files| 
| CustomField   |string/int    |Custom field, can be set to anything| 

{{< markdown-with-header title="" content="An example of a HTTP body for a data index request::">}}
```
[
  {
    "Title":"My title",
    "Description":"Description",
    "Type": "PageContent",
    "CustomField1":222,
    "CustomField2":"News"
  },
  {
    "Title":"My title",
    "Description":"Description",
    "Type": "PageContent",
    "CustomField1":123,
    "CustomField2":"Events",
  }
]
```
{{< /markdown-with-header >}} 


## TRY IT
{{< swagger-op operation="push" >}}