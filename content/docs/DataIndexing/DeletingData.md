---
weight: 3
title: "Deleting data"
---

If a page or file is removed from your website, you don't want for it to appear in your search results anymore, as it will lead to dead links. It will be removed upon a recrawl regardless, but if it can't wait, you can use this endpoint to manually delete it.

## HTTP request

```
POST https://api.cludo.com/api/v3/{CustomerId}/content/{CrawlerId}/delete
```

{{< markdown-with-header title="" content="The command below deletes search results:">}}
```
curl
-X POST \
-I https://api.cludo.com/api/v3/{CustomerId}/content/{CrawlerId}/delete \
-u {CustomerId}:{API_Key} \
```
{{< /markdown-with-header >}} 



## Body Parameters

| Parameter   |Type| Description                                     |
| ----------- |----|-------------------------------------------------|
| CustomerId  |int |Your customer id                                 | 
| CrawlerId   |int |The id of the crawler to delete the results from| 

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

## HTTP body

The body consists of an array of key/value pairs. The key is the ID of the resource and the value is the type of the resource.

## Parameters

| Parameter   |Type   | Description                                     |
| ----------- |----   |-------------------------------------------------|
| Resource ID       |string |Any. The ID of page and file resources will be their URL by default. | 
| Resource Type   |string    |"FileContent" or "PageContent"|

{{< markdown-with-header title="" content="An example of a HTTP body for a data delete request:">}}
```
[
    {
        "https://www.cludo.com/some-page/": "PageContent"
    },
    {
        "some-string": "PageContent"
    },
    {
        "https://www.cludo.com/some-file.pdf": "FileContent"
    }
]
```
{{< /markdown-with-header >}} 

## TRY IT
{{< swagger-op operation="deleteData" >}}