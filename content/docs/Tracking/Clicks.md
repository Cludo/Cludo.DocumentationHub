---
weight: 2
bookFlatSection: true
title: "Clicks"
---

Record a search result click.

## Request

```
POST https://api.cludo.com/api/v3/<CustomeID>/<EngineID>/search/pushstat/clicklog

POST https://api.cludo.com/api/v3/<CustomerID>/<EngineID>/search/pushstat/clicklog?<Query parameters>
```

## URL Parameters

| Parameter   |Type|Default| Description                                     |
| ----------- |----|-------|------------------------------------------|
| CustomerId  |int ||Your customer id                                 | 
| EngineId   |int ||The ID of the specific engine| 



{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}



## Body/Query Parameters

| Key         |Represents|Type| Description                                      |
| ----------- |----      |-------|-----------------------------------------------|
| ls  |Log source       |string    |Definition of the log source. For tracking regular clicks, it must be set to searchresult. For tracking banner clicks, it must be set to banner| 
| sz  |Screen size       |string    |The pixel resolution of the visitor's screen| 
| ua  |User agent       |string    |The visitor's user agent string| 
| refurl  |Referal url       |string    |The URL of the page the query originated from| 
| refpt  |Referal page title |string    |The title of the page the query originated from| 
| sw  |Query       |string    |The query| 
| brl  |Browser language       |string    |The language of the visitor's browser| 
| pn  |Page number       |string    |The page number requested in the search| 
| hn  |Host name       |string    |The host name of the page the query originated from| 
| qid  |Query ID       |string    |A unique string used as the ID of the query| 
| sid  |Visitor session ID       |string    |A unique string used as the ID of the visitor session| 
| qsid  |Query session ID       |string    |A unique string used as the ID of the query session| 
| clurl  |Click URL       |string    |The URL of the clicked search result| 
| cli  |Clicked search result index       |string    |The index of the clicked search result| 
| cloi  |Clicked banner ID       |string    |The ID of the banner, if it was a banner that was clicked| 
| title  |Title       |string    |The title of the clicked search result| 
| dt  |Device Type       |string    |The type of device from which the search has been performed. Currently, our cludo.js script supplies the abstract device types - mobile, tablet, or desktop. These accepted values are case sensitive and an important part of our visualization services. If not passed correctly, all services relying on them won't work as expected.| 
| it  |Input type       |string    |The type of search, it can be standard or voice| 



{{< markdown-with-header title="Example" content="using body parameters:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/search/pushstat/clicklog"
    -X POST
    -H "Content-Type: application/json"
    -d '{
            "ls": "searchresult",
            "sz": "4096x2160",
            "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36",
            "refurl": "https://www.cludo.com/site-search-features/",
            "refpt": "Customizable, whitebox AI driven site search built for marketers - Cludo",
            "sw": "government",
            "brl": "en-US",
            "pn": "1",
            "hn": "www.cludo.com",
            "qid": "be74e31601814d8fb90750e5a7082916",
            "sid": "",
            "qsid": "1696ba3d02e74658a3673b509435b082",
            "clurl": "https://www.cludo.com/government/",
            "cli": "1",
            "cloi": "",
            "title": "Government"
        }'
```
{{< /markdown-with-header >}} 

{{< markdown-with-header title="Example" content="using querystring parameters:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/search/pushstat/clicklog?
ls=searchresult&sz=4096x2160&ua=Mozilla%2F5.0%20(Windows%20NT%2010.0%3B%20Win64%3B%20x64)%20AppleWebKit%2F537.36%20(KHTML%2C%20like%20Gecko)%20Chrome%2F70.0.3538.77%20Safari%2F537.36&
refurl=https%3A%2F%2Fwww.cludo.com%2Fsite-search-features%2F&refpt=Customizable%2C%20whitebox%20AI%20driven%20site%20search%20built%20for%20marketers%20-%20Cludo&sw=government&brl=en-US&
pn=1&hn=www.cludo.com&qid=be74e31601814d8fb90750e5a7082916&sid=&qsid=1696ba3d02e74658a3673b509435b082&clurl=https%3A%2F%2Fwww.cludo.com%2Fgovernment%2F&cli=1&cloi=&title=Government"
    -X POST
```
{{< /markdown-with-header >}} 



## TRY IT
{{< swagger-op operation="pushstat" >}}