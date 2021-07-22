---
weight: 2
title: "Basic authentication"
---


{{< hint info >}}
Unless stated otherwise, basic authentication is required for all API requests.
{{< /hint >}}

{{< markdown-with-header title="Header" content="">}}
```
Authorization: Basic <Customer ID>:<API Key>
```
{{< /markdown-with-header >}} 

## Parameters

| Parameter   |Type| Description                                      |
| ----------- |---|-------------------------------------------------|
| CustomerId  |int |Your customer id                                 | 
| API Key    | string |Your API key| 


```
curl "https://api.cludo.com/api/v3/someEndpoint"
    -u 4545589:3ede38fdc0824e18bb3adb9a21fbbdc8

curl "https://api.cludo.com/api/v3/someEndpoint"
    -H "Authorization: Basic NDU0NTU4OTozZWRlMzhmZGMwODI0ZTE4YmIzYWRiOWEyMWZiYmRjOA=="
```