---
weight: 1
title: "Full Search"
---

Full searches
Full searches is the standard way to search with Cludo. With these requests you have a great variety of functions available to express your search. To read more about the HTTP response, click here.


## Parameters

| Parameter   | Description                                      |
| ----------- | -------------------------------------------------|
| CustomerId  | Your customer id                                 | 
| EngineId    | The id of the search engine to use for the search| 

## Query Parameters
There are several features available when making a full search. The features can be grouped into these five categories, each controling a different element of the search:


- Query  
- Filtering    
- Ranking    
- Grouping    
- Rendering    



{{< hint info >}}
 To se a full table of all HTTP request body properties, click here (INCOMPLETE).
{{< /hint >}}

## POST REQUEST

{{< markdown-with-header title="HTTP GET request" content="">}}
```
POST https://api.cludo.com/api/v3/{CustomerId}/{EngineId}/search
```
{{< /markdown-with-header >}} 

**Curl Example**

```
curl 
-x POST \
-i https://api.cludo.com/api/v3/{CustomerId}/{EngineId}/search \
-H "Content-Type: application/json" \
-u {CustomerId}:{API_Key} \
-d <JSON BODY> \
```

## TRY IT
{{< swagger-op operation="FullSearch" >}}


## Query
When making a search, the main feature is the user text input, specified with the query property. This property is used by the searchengine to filter and rank the search results based on importance. A query is simply just the terms you wish to exist in the search result, such as:

school activity

In this example search results containing either school or activity will be returned, but if a search result contains both terms, it will be considered more important, and will be shown before search results containin only one of the terms.


{{< hint info >}}
 Plurizations of words are taken care of, by the search engine, so activity will also search for activities, and vice versa.
{{< /hint >}}

The default behavior for all searches is to match at least one term. The alternative is to require all terms to match. To change the behavior for a search, just set the operator property.
Possible values for the operator are:

- and
- or

{{< hint info >}}
 It is possible to change the default operator behavior for all searches by <a href="https://www.cludo.com/en/contact/">contacting</a> Cludo.
{{< /hint >}}

{{< markdown-with-header title="Query body example" content="">}}
```
{
  "query": "My search string",
  "operator": "or"
}
```
{{< /markdown-with-header >}} 

{{< button relref="#try-it" class="btn btn-solid" >}}Try it with swagger{{< /button >}}

### Advanced Query

{{< hint info >}}

 If more advanced queries are needed, either use the other <a href="#query-parameters">HTTP request properties</a>, or use the query string syntax.(Incomplete)
{{< /hint >}}

## Filtering

Filtering limits search request fields to match given values, such as a price within a given range, a date within a specific month, or have a given category.

Currently, three properties are used to set filters: filters, notFilters and postFilters. Which property you use, depends on when in the search process the filter is added: filters and notFilters are executed along with the query, and will affect the ranking and facets, whereas the postFilter only filters out not matching search results, but does not affect facets. To enable postFilters on facets use the enableFacetFiltering property.

By default, when specifying multiple post filters, then all filters must match, before a search result is valid. To change this behavior use the postFilterOperator property. Its possible values are:
- and
- or

### Syntax
When adding a filter to any of the properties, you must first decide which type of filter is neded:

- values
- number ranges
- date ranges

#### Values
The value filter limits a field to specific values. This is recommended when you have a limited, known amount of choices such as with categories, car brands or file types in which you show to the user via facets.

The value filter type is simply just a range of values to match.

#### Range
The range filter is used to limit a number field to be within or greater- or less-than-or-equal-to than the specified value(s). The filter consists of three parameters:

Field to filter
Minimum value
Maximum value
Use comma ',' as the parameter separator, and a dot '.' as a decimal separator. String representation of the values are also allowed. To use only one end of the range, just insert an empty string as value. If both value parameters are empty, then the filter will be ignored.