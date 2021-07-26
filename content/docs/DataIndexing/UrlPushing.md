---
weight: 1
title: "Url Pushing"
---

Since full domain crawls are not frequent (maybe once a day), new pages to your website won't appear in search results before the domain is recrawled. If you cannot wait for a complete recrawl, then you may push the urls in question, which will be crawled within a couple of minutes.

## HTTP request
```
POST https://api.cludo.com/api/v3/<CustomerID>/content/<CrawlerID>/pushurls
```
 

## Parameters

| Parameter   |Type| Description                                     |
| ----------- |----|-------------------------------------------------|
| CustomerId  |int |Your customer id                                 | 
| CrawlerId   |int |The ID of the specific crawler you'd like to crawl the given URLs| 

## HTTP body

{{< markdown-with-header title="" content="The body content is a list of urls to crawl.">}}
```
curl "https://api.cludo.com/api/v3/4545589/content/2368899/pushurls"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '[
            "https://www.cludo.com/en/products/",
            "https://www.cludo.com/en/features/"
        ]'
```
{{< /markdown-with-header >}} 

## TRY IT
{{< swagger-op operation="pushurls" >}}