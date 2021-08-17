---
weight: 3
bookFlatSection: false
title: "Ip addresses"
---

Some of our features are driven directly by the IP address of the visitor, like excluding analytics from certain ranges in My Cludo or our geo analytics. Usually we get that automatically as the tracking is initiated by our script on the visitor's machine, but if the tracking request to us doesn't originate from the visitor, you will need to provide the real IP address to us separately.

You can do so by providing an additional HTTP header with the tracking request or using a ip parameter in the body.

## Header

`X-Real-IP: <ip>`


{{< markdown-with-header title="Example" content="using header parameter:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/search/pushstat/querylog"
    -H "X-Real-IP: 127.0.0.1"

curl "https://api.cludo.com/api/v3/4545589/7578030/search/pushstat/clicklog"
    -H "X-Real-IP: 127.0.0.1"
```
{{< /markdown-with-header >}}



## Header/Body Parameters

| Key         |Represents|Type| Description                                      |
| ----------- |----      |-------|-----------------------------------------------|
| ip  |The IP address of the visitor       |string    |ip address|

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
            "title": "Government",
            "ip":"127.0.0.1"
        }'
```
{{< /markdown-with-header >}} 

 



## TRY IT
{{< swagger-op operation="pushstat" >}}
