---
weight: 2
bookFlatSection: true
title: "Search counts totals"
---
Retrieves the search count, for a specified period.

## Request

```
GET https://api.cludo.com/api/v3/<customerId>/<engineId>/statistics/totalSearches?
from=<From>&to=<To>&onlyIncludeUnique=<Only Include Unique>&includePreviousPeriod=<Include Previous Period>
```

## URL Parameters

| Parameter   |Type|Default| Description                                     |
| ----------- |----|-------|------------------------------------------|
| customerId  |int ||Your customer id                                 | 
| engineId   |int ||The ID of the specific engine| 
| From    |string ||Datetime when you want statistics from eg. 2016-08-14T22:00:00.000Z| 
| To   |string ||Datetime when you want the statistics to eg. 2016-08-18T22:00:00.000Z| 
| Only Include Unique   |bool |false	|Whether you want to retrieve the unique count only| 
| Include Previous Period   |bool |false	|Whether you want to also retrieve the count for the previous period| 

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

## Example
{{< markdown-with-header title="" content="request:">}}
```
curl "https://api.cludo.com/api/v3/4545589/7578030/statistics/totalSearches?
from=2019-03-28T22:00:00.000Z&to=2019-04-30T21:59:59.999Z&onlyIncludeUnique=false&includePreviousPeriod=false"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

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