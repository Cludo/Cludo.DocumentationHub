---
weight: 1
title: "Site key authentication"
---


Site key authentication is a means of authentication that can only be used for search, and exists to facilitate public facing search where you **don't** want to expose your API key, which is otherwise the case with  <a href="/docs/authentication/basicauthentication/">basic authentication</a>.

{{< hint warning >}}
The credentials must be Base64-encoded as a single unit.
{{< /hint >}}




## Parameters

| Parameter   |Type| Description                                     |
| ----------- |----|-------------------------------------------------|
| customerId  |int |Your customer id                                 | 
| engineId    |int |The id of the search engine to use for the search| 





{{< markdown-with-header title="Header" content="Note that the last part of the credentials is not a parameter, but literally the string SearchKey.">}}
```
Authorization: SiteKey <customerId>:<engineId>:SearchKey
```
{{< /markdown-with-header >}} 


{{< markdown-with-header title="Example" content="NDU0NTU4OTo3NTc4MDMwOlNlYXJjaEtleQ== is the base64 string of : customerId:engineId:SearchKey">}}
```
curl "https://api.cludo.com/api/v3/search"
-H "Authorization: SiteKey NDU0NTU4OTo3NTc4MDMwOlNlYXJjaEtleQ=="
```
{{< /markdown-with-header >}} 