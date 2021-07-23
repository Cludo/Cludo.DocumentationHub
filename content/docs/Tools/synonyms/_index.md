---
weight: 3
bookFlatSection: false
title: "Synonyms"
---

Synonyms are useful if you have the content your visitors are looking for, but they're searching for other words for the same thing.

{{< hint info >}}
 You can read more about synonyms here. <a href="https://cludo.zendesk.com/hc/en-us/articles/115002580111-Synonyms" target="_blank">here (Broken link)</a>.
{{< /hint >}}

## Data structures

### Synonyms Group

| Key         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| groupId           |int | The ID of the synonyms group                       | 
| words    |array | Collection of words which are synonyms| 
| language	    |string | A two-letter ISO language code| 


```
{
    "groupId": 1,
    "words": ["work", "job", "career"],
    "language": "en"
}
```

## Get all synonyms by language

Get all synonyms groups for a specific language.

### Request
```
GET https://api.cludo.com/api/synonymsgroup/<Language>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| Language    |string | A two-letter ISO language code | 


{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/synonymsgroup/en"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT 
{{< swagger-op operation="GetSynonymsGroupByLanguage" >}}

### Response
Will return an array of synonyms groups. See <a href="#synonyms-group">data structures</a>


## Get single synonyms group

Get a specific synonyms group.

### Request
```
GET https://api.cludo.com/api/synonymsgroup/<Synonym Group ID>
```

### URL Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| Synonym Group ID    |int | The ID of the specific synonyms group| 


{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/synonymsgroup/9457415"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### TRY IT 
{{< swagger-op operation="GetSynonymsGroupByGroupId" >}}

### Response
Will return a single synonyms group. See <a href="#synonyms-group">data structures</a>.



## Create synonyms group

Create a synonyms group.

### Request
```
POST https://api.cludo.com/api/synonymsgroup
```

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/synonymsgroup"
    -X POST
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
            "words": ["work", "job", "career"],
            "language": "en"
        }'
```
{{< /markdown-with-header >}} 

### Body
A single synonyms group composed of multiple words which are synonyms. See <a href="#synonyms-group">data structures</a>.


### TRY IT 
{{< swagger-op operation="CreateSynonymsGroup" >}}

### Response
Will return the created synonyms group. See <a href="#synonyms-group">data structures</a>



## Update synonyms group

Update a specific synonyms group.

### Request
```
PUT https://api.cludo.com/api/synonymsgroup
```

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/synonymsgroup"
    -X PUT
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
    -H "Content-Type: application/json"
    -d '{
            "groupId": 1,
            "words": ["work", "job", "opportunity"],
            "language": "en"
        }'
```
{{< /markdown-with-header >}} 

### Body Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| group Id   |int | group Id to update | 
| words   |array | array with synonyms words | 
| language   |string | A two-letter ISO language code | 

### Body
A single synonyms group. See <a href="#synonyms-group">data structures</a>.


### TRY IT 
{{< swagger-op operation="UpdateSynonymsGroup" >}}

### Response
Will return the updated synonyms group. See <a href="#synonyms-group">data structures</a>


## Delete synonym

Delete one or more synonyms groups.

### Request
```
DELETE https://api.cludo.com/api/synonymsgroup?groupIds=<Synonym Group ID>&groupIds=<Synonym Group ID>
```

{{< markdown-with-header title="Example">}}
```
curl "https://api.cludo.com/api/synonymsgroup?groupIds=1&groupIds=2&groupIds=3"
    -X DELETE
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8
```
{{< /markdown-with-header >}} 

### Query Parameters
| Parameter         |Type | Description                                      |
| ----------- |---  | -------------------------------------------------|
| Synonym Group ID   |int | The ID of the specific synonyms group | 



### TRY IT 
{{< swagger-op operation="DeleteSynonymsGroup" >}}

