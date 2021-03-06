---
weight: 1
bookFlatSection: false
title: "Queries"
---

Record a search query.

## Request

```
POST https://api.cludo.com/api/v3/<customerId>/<engineId>/search/pushstat/querylog

POST https://api.cludo.com/api/v3/<customerId>/<engineId>/search/pushstat/querylog?<Query parameters>
```

## URL Parameters

| Parameter   |Type| Description                                     |
| ----------- |----|------------------------------------------|
| customerId  |int |Your customer id                                 | 
| engineId   |int |The ID of the specific engine| 

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

## Body/Query Parameters

| Key         |Represents|Type| Description                                      |
| ----------- |----      |-------|-----------------------------------------------|
| sz  |Screen size       |string    |The pixel resolution of the visitor's screen| 
| ua  |User agent       |string    |The visitor's user agent string| 
| refurl  |Referal url       |string    |The URL of the page the query originated from| 
| refpt  |Referal page title |string    |The title of the page the query originated from| 
| sw  |Query       |string    |The query| 
| brl  |Browser language       |string    |The language of the visitor's browser| 
| pn  |Page number       |string    |The page number requested in the search| 
| hn  |Host name       |string    |The host name of the page the query originated from| 
| rc  |Result count       |string    |The amount of results for the query| 
| fquery  |Fixed query       |string    |The actual performed query, if the original query was intercepted and adjusted by Cludo (e.g. spelling mistakes)| 
| ban  |Banners count       |string    |The number of banners shown| 
| bnrs  |Banner IDs       |string    |The IDs of the banners shown (comma separated)| 
| rt  |Response time       |string    |The time it took to perform the query| 
| ql  |Quicklink ID       |string    |The quicklink ID, if a quicklink redirection occurs| 
| qid  |Query ID       |string    |A unique string used as the ID of the query| 
| sid  |Visitor session ID       |string    |A unique string used as the ID of the visitor session| 
| qsid  |Query session ID       |string    |A unique string used as the ID of the query session| 
| dt  |Device Type       |string    |The type of device from which the search has been performed. Currently, our cludo.js script supplies the abstract device types - mobile, tablet, or desktop. These accepted values are case sensitive and an important part of our visualization services. If not passed correctly, all services relying on them won't work as expected.| 
| it  |Input type       |string    |The type of search, it can be standard or voice| 


{{< markdown-with-header title="Example" content="using body parameters:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/search/pushstat/querylog"
    -X POST
    -H "Content-Type: application/json"
    -d '{
            "sz": "4096x2160",
            "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36",
            "refurl": "https://www.cludo.com/site-search-features/",
            "refpt": "Customizable, whitebox AI driven site search built for marketers - Cludo",
            "sw": "government",
            "brl": "en-US",
            "pn": "1",
            "hn": "www.cludo.com",
            "rc": "7",
            "fquery": "",
            "ban": "2",
            "bnrs": "2673284,3933858",
            "rt": "34",
            "ql": "",
            "qid": "be74e31601814d8fb90750e5a7082916",
            "sid": "",
            "qsid": "1696ba3d02e74658a3673b509435b082"
        }'
```
{{< /markdown-with-header >}} 

{{< markdown-with-header title="Example" content="using querystring parameters:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/search/pushstat/querylog?
sz=4096x2160&ua=Mozilla%2F5.0%20(Windows%20NT%2010.0%3B%20Win64%3B%20x64)%20AppleWebKit%2F537.36%20(KHTML%2C%20like%20Gecko)%20Chrome%2F70.0.3538.77%20Safari%2F537.36&r
efurl=https%3A%2F%2Fwww.cludo.com%2Fsite-search-features%2F&refpt=Customizable%2C%20whitebox%20AI%20driven%20site%20search%20built%20for%20marketers%20-%20Cludo&
sw=government&brl=en-US&pn=1&hn=www.cludo.com&rc=7&fquery=&ban=2&bnrs=2673284%2C3933858&rt=34&ql=&qid=be74e31601814d8fb90750e5a7082916&sid=&qsid=1696ba3d02e74658a3673b509435b082"
    -X POST
```
{{< /markdown-with-header >}} 



## TRY IT
{{< swagger-op operation="pushstat" >}}