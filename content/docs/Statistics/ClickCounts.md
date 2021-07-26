---
weight: 3
bookFlatSection: true
title: "Click counts"
---

Retrieves a list of clicked targets for a specified period, ordered by popularity by default.

## Request

```
GET https://api.cludo.com/api/v3/<CustomerID>/<EngineID>/statistics/clickCounts?
from=<From>&to=<To>&query=<Query>&clickTarget=<Click Target>&orderBy=<Order By>&sortOrder=<Sort Order>&
limit=<Limit>&pageNumber=<Page Number>
```

## URL Parameters

| Parameter   |Type|Default| Description                                     |
| ----------- |----|-------|------------------------------------------|
| CustomerId  |int ||Your customer id                                 | 
| EngineId   |int ||The ID of the specific engine| 
| From    |string ||Datetime when you want statistics from eg. 2016-08-14T22:00:00.000Z| 
| To   |string ||Datetime when you want the statistics to eg. 2016-08-18T22:00:00.000Z| 
| Query  |string |optional	|A search word to filter results by to only get results for a single search term| 
| Click Target|string |page	|Click type to get results for, currently only supports 'page' which means ordinary search results| 
| Order By|string |count	|Property to order by| 
| Sort Order|string |descending	|Sort direction (ascending, descending)| 
| Limit|int |10	|Number of results pr. page| 
| Page Number|int |1	|Page number, zero indexed| 

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

## Example
{{< markdown-with-header title="" content="request:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/statistics/clickCounts?
from=2019-03-28T22:00:00.000Z&to=2019-04-30T21:59:59.999Z&query=&clickTarget=page&orderBy=count&
sortOrder=descending&limit=10&pageNumber=1"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

{{< markdown-with-header title="" content="The above command returns daily aggregated data in the following JSON structure:">}}
```
[
    {
        "pageNumber": 0,
        "pageSize": 10,
        "totalItems": 1,
        "items": [
            {
                "title": "Cludo click tracking statistics",
                "clickTarget": "http://cludo.com/all-about-clicktracking.pdf",
                "count": 22,
                "uniqueCount": 11,
                "previousCount": 10,
                "previousUniqueCount": 5
            }
        ]
    }
]
```
{{< /markdown-with-header >}} 

## TRY IT
{{< swagger-op operation="ClickCounts" >}}