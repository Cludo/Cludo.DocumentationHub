---
weight: 1
bookFlatSection: true
title: "Hugo Component Reference"
---

This is intended to be component usage examples and will be removed when development is underway or complete.

## Markdown table

**Code**

```
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
```

**Output**

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |


## Swagger Operation Module

~~The swagger module is currently configured to point to the example data that swagger hosts. It's a pet store api. [Here's a link](https://petstore.swagger.io/) to the full, swagger-hosted solution. The operation attribute on the following shortcode must match an operation on the pet store api.~~

Currently, this is pointing to Cludo API's OpenApi json file. The code example output below uses operation `Statistics`.

**Code**

```
{{</* swagger-op operation="pet" */>}}
```

**Output**

{{< swagger-op operation="Statistics" >}}


