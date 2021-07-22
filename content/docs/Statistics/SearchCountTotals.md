---
weight: 2
bookFlatSection: true
title: "Search counts totals"
---

## Request

```
GET https://api.cludo.com/api/v3/<Customer ID>/<Engine ID>/statistics/totalSearches?
from=<From>&to=<To>&onlyIncludeUnique=<Only Include Unique>&includePreviousPeriod=<Include Previous Period>
```
{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}
## URL Parameters

| Parameter   |Type|Default| Description                                     |
| ----------- |----|-------|------------------------------------------|
| CustomerId  |int ||Your customer id                                 | 
| EngineId   |int ||The ID of the specific engine| 
| From    |string ||Datetime when you want statistics from eg. 2016-08-14T22:00:00.000Z| 
| To   |string ||Datetime when you want the statistics to eg. 2016-08-18T22:00:00.000Z| 
| Only Include Unique   |bool |false	|Whether you want to retrieve the unique count only| 
| Include Previous Period   |bool |false	|Whether you want to also retrieve the count for the previous period| 


## Example

```
curl "https://api.cludo.com/api/v3/4545589/7578030/statistics/totalSearches?
from=2019-03-28T22:00:00.000Z&to=2019-04-30T21:59:59.999Z&onlyIncludeUnique=false&includePreviousPeriod=false"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< markdown-with-header title="" content="The above command returns the following JSON structure::">}}
```
{
    "withinCurrentPeriod": 25000,
    "withinPreviousPeriod": null
}
```
{{< /markdown-with-header >}} 

## TRY IT
{{< swagger-op operation="SearchCountsTotal" >}}