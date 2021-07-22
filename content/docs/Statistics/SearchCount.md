---
weight: 1
bookFlatSection: true
title: "Search counts per day"
---

Retrieves a list of search counts summed by day for a specified period.

## Request

```
GET https://api.cludo.com/api/v3/<Customer ID>/<Engine ID>/statistics/searchHistogram?
type=<Type>&from=<From>&to=<To>&timezone=<Timezone>
```
{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}
## URL Parameters

| Parameter   |Type|Default| Description                                     |
| ----------- |----|-------|------------------------------------------|
| CustomerId  |int ||Your customer id                                 | 
| EngineId   |int ||The ID of the specific engine| 
| Type   |string |all|What statistics do you want. Options are: <ul><li>`All` - all statistics</li><li>`unsuccessfull`  - only retrive search statistics without any results </li><li>`successful` - only retrieve search statistics which returned results</li></ul>| 
| From    |string ||Datetime when you want statistics from eg. 2016-08-14T22:00:00.000Z| 
| To   |string ||Datetime when you want the statistics to eg. 2016-08-18T22:00:00.000Z| 
| Timezone   |string |00:00 (UTC)	|The timezone (UTC offset) the histogram should be formatted with, eg.:  <ul><li>`00:00` - UTC</li><li>`02:00`  -  UTC+2 (CEST) </li><li>`-05:00` - UTC-5 (CDT)</li></ul>| |

## Example

```
curl "https://api.cludo.com/api/v3/4545589/7578030/statistics/searchHistogram?
type=successful&from=2016-08-14T22:00:00.000Z&to=2016-08-22T12:44:38.799Z&timezone=00:00"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```

{{< markdown-with-header title="" content="The above command returns daily aggregated data in the following JSON structure:">}}
```
{
    "totalSearches": [
        {
            "Key": "2016-08-14", 
            "Value": 200
        },
        {
            "Key": "2016-08-15", 
            "Value": 900
        },
        {
            "Key": "2016-08-16", 
            "Value": 0
        }
    ],
    "uniqueSearches": [
        {
            "Key": "2016-08-14", 
            "Value": 100
        },
        {
            "Key": "2016-08-15", 
            "Value": 450
        },
        {
            "Key": "2016-08-16", 
            "Value": 0
        }
    ]
}
```
{{< /markdown-with-header >}} 

## TRY IT
{{< swagger-op operation="SearchCounts" >}}