---
weight: 4
title: Authentication
---

We offer different means of authentication depending on the action you're looking to perform.

- For public facing search, we support our custom  <a href="/docs/authentication/sitekeyauthentication/">site key authentication</a>.
- Otherwise, we support <a href="/docs/authentication/basicauthentication/">basic authentication</a>.

## Basic

{{< hint info >}}
Unless stated otherwise, basic authentication is required for all API requests.
{{< /hint >}}

{{< markdown-with-header title="Header" content="">}}
```
Authorization: Basic <customerId>:<APIKey>
```
{{< /markdown-with-header >}} 

### Parameters

| Parameter   |Type| Description                                      |
| ----------- |---|-------------------------------------------------|
| customerId  |int |Your customer id                                 | 
| APIKey    | string |Your API key| 


{{< markdown-with-header title="Example" content="NDU0NTU4OTozZWRlMzhmZGMwODI0ZTE4YmIzYWRiOWEyMWZiYmRjOA== is the base64 string of : customerId:ApiKey">}}
```
curl "https://api.cludo.com/api/v3/someEndpoint"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8

curl "https://api.cludo.com/api/v3/someEndpoint"
    -H "Authorization: Basic NDU0NTU4OTozZWRlMzhmZGMwODI0ZTE4YmIzYWRiOWEyMWZiYmRjOA=="
```
{{< /markdown-with-header >}} 

## SiteKey

Site key authentication is a means of authentication that can only be used for search, and exists to facilitate public facing search where you **don't** want to expose your API key, which is otherwise the case with  <a href="/docs/authentication/basicauthentication/">basic authentication</a>.

{{< hint warning >}}
The credentials must be Base64-encoded as a single unit.
{{< /hint >}}




### Parameters

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