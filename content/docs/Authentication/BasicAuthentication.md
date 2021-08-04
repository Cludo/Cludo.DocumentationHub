---
weight: 2
title: "Basic authentication"
---


{{< hint info >}}
Unless stated otherwise, basic authentication is required for all API requests.
{{< /hint >}}

{{< markdown-with-header title="Header" content="">}}
```
Authorization: Basic <customerId>:<APIKey>
```
{{< /markdown-with-header >}} 

## Parameters

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