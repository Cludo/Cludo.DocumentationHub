---
weight: 1
title: "Full Search"
---

Full searches
Full searches is the standard way to search with Cludo. With these requests you have a great variety of functions available to express your search. To read more about the HTTP response, click here.

## Request


```
POST https://api.cludo.com/api/v3/{customerId}/{engineId}/search
```


## Parameters

| Parameter   |Type| Description                                      |
| ----------- |---| -------------------------------------------------|
| customerId  |int| Your customer id                                 | 
| engineId    |int| The id of the search engine to use for the search| 

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


**Curl Example**

```
curl 
-x POST \
-i https://api.cludo.com/api/v3/{customerId}/{engineId}/search \
-H "Content-Type: application/json" \
-u {customerId}:{API_Key} \
-d <JSON BODY> \
```

## TRY IT
{{< swagger-op operation="FullSearch" >}}


## Query
When making a search, the main feature is the user text input, specified with the query property. This property is used by the searchengine to filter and rank the search results based on importance. A query is simply just the terms you wish to exist in the search result, such as:

`school activity`

In this example search results containing either school or activity will be returned, but if a search result contains both terms, it will be considered more important, and will be shown before search results containin only one of the terms.


{{< hint info >}}
 Plurizations of words are taken care of, by the search engine, so activity will also search for activities, and vice versa.
{{< /hint >}}

The default behavior for all searches is to match at least one term. The alternative is to require all terms to match. To change the behavior for a search, just set the `operator` property.
Possible values for the `operator` are:

- **or**
- **and**

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

Currently, three properties are used to set filters: `filters`, `notFilters` and `postFilters`. Which property you use, depends on when in the search process the filter is added: `filters` and `notFilters` are executed along with the query, and will affect the ranking and facets, whereas the `postFilter` only filters out not matching search results, but does not affect facets. To enable `postFilters` on facets use the `enableFacetFiltering` property.

By default, when specifying multiple post filters, then all filters must match, before a search result is valid. To change this behavior use the `postFilterOperator` property. Its possible values are:
- **and**
- **or**

### Syntax
When adding a filter to any of the properties, you must first decide which type of filter is neded:


- values
- number ranges
- date ranges

**Values** 

The value filter limits a field to specific values. This is recommended when you have a limited, known amount of choices such as with categories, car brands or file types in which you show to the user via facets.

The value filter type is simply just a range of values to match.

{{< markdown-with-header content="Examples on using a value filter:">}}
```
"Category": ["Publications", "Events"]
"DocumentType": ["PDF"]
```
{{< /markdown-with-header >}} 

**Range**  

The range filter is used to limit a number field to be within or greater- or less-than-or-equal-to than the specified value(s). The filter consists of three parameters:

- Field to filter
- Minimum value
- Maximum value

Use comma ',' as the parameter separator, and a dot '.' as a decimal separator. String representation of the values are also allowed. To use only one end of the range, just insert an empty string as value. If both value parameters are empty, then the filter will be ignored.

{{< markdown-with-header content="Examples on using a range filter:">}}
```
"range": ["Price", 20, 100]
"range": ["WheelRimSize", 25.5, ""]
"range": ["PoolSize", "", 2000]
"range": ["LegoPieces", "500.75", "750.57"]
```
{{< /markdown-with-header >}} 

**Date** 

The date filter is used to limit a date-time field to be within, before or after the specified date(e). The filter consists of three parameters:

- Field to filter
- Minimum date-time
- Maximum date-time

Both date-time values must be strings and in <a href="https://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> format, such as:

- 2017-06-13T02:50:25+00:00
- 2017-06-13T02:50:25Z
- 20170613T025025Z
- 2017-06-13

If no time part is specified, then the full date is included in the search, meaning the date-time 2017-06-13T22:13 wil be considered within a range using 2017-06-13. If only one limit is needed just insert an empty string into the one to ignore. If both value parameters are empty, then the filter will be ignored.

{{< markdown-with-header title=""  content="Examples on using a date filter:">}}
```
"date": ["ProductionYear", "2015", "2017"]
"date": ["PremiereDate", "2017-06-01", ""]
"date": ["Exipration", "", "2020-12-24T20:00"]
```
{{< /markdown-with-header >}} 


## Ranking
When searching, the Cludo will attempt to order the search results, based on how well they match the given query.
For most searches the Cludo ranking algorithm will be enough, but if you need to override the ranking completely,
or at least affect affect certain aspects of it, then use the `sort` property or the `valueBoost` property.

### Custom sort
A custom sort set on the `sort` property, overrides the entire ranking algorithm with the given sort model.
The sort type is a model, where the property names are the fields to sort, and the values specifies the direction of the sort.
The order of the properties determine the order of the sort.

### Value boost
Value boostings set on the `valueBoost` property, will increase search results matching a given boost to be ranked higher than others.
The `valueBoost` property type is an array of boost models, each consisting of the field to boost and an array of boostings,
determining the boost value when matching a given value


{{< markdown-with-header title=""  content="Ranking example:">}}
```
{
  "sort": {
    "City": "asc",
    "Street": "asc",
    "LastName": "desc"
  },
  "valueBoost": [
    {
      "fieldName": "Category",
      "Boosts": [
        {
          "Boost": 23.4,
          "Values": ["A", "B", "C"]
        }
      ]
    }
  ]
}
```
{{< /markdown-with-header >}} 

## Grouping

Grouping allows you to slice a search result into batches, and return each bach in a controlled manner. This allows paging of search results.

The `perPage` property controls the amount of search results returned in the HTTP response, wheras the `page` property selects the page to return.

Both properties must be a positive integer.

{{< markdown-with-header title=""  content="Grouping example:">}}
```
{
  "perPage": 10,
  "page": 2
}
```
{{< /markdown-with-header >}} 

## Rendering

The final step before returning search results is selecting how you want the results presented.
For this you use the `responseType` property with one of the following options:

- **JsonObject**
- **JsonHtml**

To read more about the variation in the HTTP Response click **here(INCOMPLETE)**.

*JsonObject* returns all data as json, wheras *JsonHtml* pre-renders the search results, and the facets with a pre-determined template.

The template to use is specified with the `template` property when you have a *Business* or *Enterprise* solution and with the `overlay` property when you have a *Essential* or *Professional* solution.

{{< markdown-with-header title=""  content="Rendering example:">}}
```
{
  "responseType": "JsonHtml",
  "template": "MainSite Template",
  "overlay": "Overlay Template V2"
}
```
{{< /markdown-with-header >}} 

## Related Searches

{{< hint info >}}
 This feature might not be part of your subscription. If you want to know more, please <a href="https://www.cludo.com/contact/" target="_blank">contact us</a>.
{{< /hint >}}

Related searches is a feature that can be used to conveniently suggest possible search terms based on their usages by other users and, at the same time, close to the one that the user has entered.

To enable this feature, use the enableRelatedSearches property.

{{< markdown-with-header title=""  content="Related searches example:">}}
```
{
  "enableRelatedSearches": true
}
```
{{< /markdown-with-header >}} 


## HTTP Response

Depending on the requested `responseType` described <a href="/docs/searching/fullsearch/#related-searches">here</a>, one of the two types of responses may be received. Their differences lies within how the search results, facets and suggestions are returned.

{{< hint info >}}
  To se a full table of all HTTP response body properties, click <a href="/docs/searching/fullsearch/#table-of-request-properties">here</a>.
{{< /hint >}}

***JsonObject* response**

The *JsonObject* response returns all data as json models, to be processed client side by JavaScript or other code.

***JsonHtml* response**

The *JsonHtml* response returns search results and facets as pre-rendered HTML code, ready to be injected into a HTML page.

## Table of request properties 

{{< hint info >}}
  Features marked with a * denotes that it's not included with all subscription levels. If you want to know more, please <a href="https://www.cludo.com/contact/" target="_blank">contact us</a>.
{{< /hint >}}

###  <a href="/docs/searching/fullsearch/#query">Query</a>

| Parameter   |Required|Type|Default| Description                                     |
| ----------- |--------|----|-------|------------------------------------------|
| query       |yes     |string |       | The text you want to search for.              | 
| operator    |no     |enum    |Engine specific|Specify if one or more query terms should match, or all terms must match.Possible values are: <ul><li>`or`<li>`and`</li></ul>| 

###  <a href="/docs/searching/fullsearch/#filtering">Filtering</a>

| Parameter   |Required|Type|Default| Description                                     |
| ----------- |--------|----|-------|------------------------------------------|
| filters       |no     |Filter Model |       | Specify `range` and `date` filters to limit the search results.              | 
| notFilters    |no     |Filter Model |   |Specify exclusion `range` and `date` filters to limit the search results.| 
| postFilters    |no     |postFilter Model|   |Specify facet filters to limit the search results.| 
| postFiltersOperator    |no     |enum|and    |The relation between post filters.Possible values are:<ul><li>`or`<li>`and`</li></ul>| 
| enableFacetFiltering    |no     |bool|false   |If you require post filters to be set on the HTTP response facets. See also **Response facets(Broken Link)**.| 

###  <a href="/docs/searching/fullsearch/#ranking">Ranking</a>

| Parameter   |Required|Type|Default| Description                                     |
| ----------- |--------|----|-------|------------------------------------------|
| sort       |no     |Sort Model |       | Set a value to override the default sort behavior with an explicit one.           | 
| valueBoost       |no     |ValueBoost Model |       | Allows explicit search result boosting based on specific values.              | 

###  <a href="/docs/searching/fullsearch/#grouping">Grouping</a>

| Parameter   |Required|Type|Default| Description                                     |
| ----------- |--------|----|-------|------------------------------------------|
| perPage       |no     |uint32 |   10    | Amount of search results in the response. Use together with `page` to batch the results.      | 
| page       |no     |uint32 |   1    |The page index of search results to return. Use together with `perPage` to batch the results.            | 


###  <a href="/docs/searching/fullsearch/#rendering">Rendering</a>

| Parameter   |Required|Type|Default| Description                                     |
| ----------- |--------|----|-------|------------------------------------------|
| responseType       |no     |enum |   JsonObject    | The resulting format to return the search results as in the HTTP Response.     | 
| template       |no     |string |      |The name of the template to use for rendering JsonHTML.         | 
| overlay       |no     |string |      |The name of the overlay template to use for rendering JsonHTML.    | 


###  <a href="/docs/searching/fullsearch/#related-searches">Related searches</a>

| Parameter   |Required|Type|Default| Description                                     |
| ----------- |--------|----|-------|------------------------------------------|
| enableRelatedSearches       |no     |bool |   false    | If you want to also get related searches for the specific search term.    | 


### Full HTTP request example

{{< markdown-with-header title=""  content="Full HTTP request example:">}}
```
{
  "query": "The search string here",
  "operator": "or",

  "filters": {
    "range": ["Price", 20, 100]
  },
  "notFilters": {
    "date": ["EventDate", "20170601", "20170630"]
  },
  "postFilters": {
    "Category": ["Publications", "Events"]
  },
  "postFilterOperator": "or",
  "enableFacetFiltering": true,
  "enableRelatedSearches": true,

  "sort": {
    "City": "asc"
  },
  "valueBoost": [
    {
      "fieldName": "Category",
      "Boosts": [
        {
          "Boost": 23.4,
          "Values": ["A", "B", "C"]
        }
      ]
    }
  ],

  "responseType": "JsonHtml",
  "template": "MainSite Template",
  "overlay": "Overlay Template V2"
}
```
{{< /markdown-with-header >}} 


## Table of response properties

Depending on the `responseType` property on the request, the reponse have different properties.

### Common properties
Common properties for both response types are:

| Parameter   |Type| Description                                      |
| ----------- |---| -------------------------------------------------|
| QueryId  |string| A random string identifying the search query.                                | 
| ResponseTime    |uint64| The time in milliseconds it took the Cludo servers to make the search.| 
| FixedQuery  |string|If no results where found for the original query, the searchengine will attempt another search with spelling corrections. If so, the corrected terms will be displayed here.                 | 
| TotalDocument  |uint32| The total amount of matches found.                  | 
| Banners  |Banner model array|An array of banners matching the search query.                            | 
| Synonyms  |string array| An array of synonyms matching the search query.                             | 



### JsonObject response
Unique to the JsonObject response:

| Parameter   |Type| Description                                      |
| ----------- |---| -------------------------------------------------|
| Suggestions  |suggestion model array|An array of suggestions for alternative searches.                              | 
| TypedDocuments  |Typed document model array|An array of the search results.                             | 
| Facets  |Facet model|Model containg all facets currently implemented on the engine.                        | 
| RelatedSearchDocuments  |Related searches model| An array of related searches.                         | 

### Full JsonObject HTTP response example

{{< markdown-with-header title=""  content="Full JsonObject HTTP response example:">}}
```
{
  "QueryId": "c77f19d9a4b243b182466ca31cf9848c",
  "ResponseTime": 40,
  "FixedQuery": "tollroad",
  "Suggestions": [
    {
      "Text": "roadpricing",
    }
  ],
  "TotalDocument": 80,
  "TypedDocuments": [ 
    {
      "ResultIndex": 1,
      "Fields": {
        "Title": {
          "Field": "Title",
          "Value": "Amazing title about tollroads",
          "Values": [ "Amazing title about tollroads"],
          "Highlights": ["Amazing title about <b>tollroads</b>"],
          "IsArray": false
        },
        "Description":{
          "Field": "Description",
          "Value": "A long description",
          "Values": [ "A long description"],
          "Highlights": ["A long description"],
          "IsArray": false
        },
        "NewsArea":{
          "Field": "NewsArea",
          "Value": "Sports",
          "Values": ["Sports"],
          "Highlights": ["Sports"],
          "IsArray": false
        }
      },
      "FieldNames": [
        "Title",
        "Description",
        "NewsArea"
      ]
    }
  ], 
  "Facets": {
    "Category": {
      "FieldName": "Category",
      "MissingCount": 0,
      "AllCount": 35,
      "Items": [
        {
          "Key": "News",
          "Count": 30,
          "Facets": {
             "NewsArea": {
              "FieldName": "NewsArea",
              "MissingCount": 0,
              "AllCount": 30,
              "Items": [
                {
                  "Key": "Sports",
                  "Count": 20,
                  "Facets": {}
                },
                {
                  "Key": "Politics",
                  "Count": 10,
                  "Facets": {}
                }
              ]
            }
          }
        },
          {
          "Key": "Events",
          "Count": 5,
          "Facets": {}
        }
      ]
    }  
  },
  "Banners": [
    {
      "Banner":"<A HMTL STRING>",
      "Name":"My banner"
    }
  ],
  "Synonyms": [
    "highwaypricing"
  ],
  "RelatedSearchDocuments": [  
      {  
         "SearchTerm": "search term 1",
         "DocsCount": 10
      },
      {  
         "SearchTerm": "search term 2",
         "DocsCount": 5
      }
   ]
}
```
{{< /markdown-with-header >}} 

### JsonHtml response
Unique to the JsonHtml response:

| Parameter   |Type| Description                                      |
| ----------- |---| -------------------------------------------------|
| DidYouMean  |string|The first suggestion, if any.                       | 
| Facets  |string|The html generated string of the facets, created with the template set in the request.                      | 
| SearchResult  |string|The html generated string of the search results, created with the template set in the request.                          | 
| RelatedSearchesResult  |string|The html generated string of the related searches results, created with the template set in the request.                            | 

### Full JsonHtml HTTP response example

{{< markdown-with-header title=""  content="Full JsonHtml HTTP response example:">}}
```
{
  "QueryId": "c77f19d9a4b243b182466ca31cf9848c",
  "ResponseTime": 40,
  "FixedQuery": "tollroad",
  "DidYouMean": "roadpricing",
  "TotalDocument": 80,
  "SearchResult": "<A HTML STRING>", 
  "Facets": "<A HTML STRING>",
  "RelatedSearchesResult": "<A HTML STRING>",
  "Banners": [
    {
      "Banner":"<A HMTL STRING>",
      "Name":"My banner"
    }
  ],
    "Synonyms": [
    "highwaypricing"
  ]
}
```
{{< /markdown-with-header >}} 