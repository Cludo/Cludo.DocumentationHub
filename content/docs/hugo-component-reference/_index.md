---
weight: 1
bookFlatSection: true
title: "Hugo Component Reference"
---
<!-- {{< edit-github >}} -->
This is intended to be component usage examples and will be removed when development is underway or complete.

## List W/ sublisting

1. Remansit notam Stygia feroxque
2. Et dabit materna
3. Vipereas Phrygiaeque umbram sollicito cruore conlucere suus
4. Quarum Elis corniger
5. Nec ieiunia dixit

{{< ordered-list-title number="1" title="Remansit notam Stygia feroxque" id="1-Remansit-notam-Stygia-feroxque" >}}
Videt e flammis Scythica parantem rupisque pectora umbras. Haec ficta canistris repercusso simul ego aris Dixit! Esse Fama trepidare hunc crescendo vigor ululasse vertice exspatiantur celer `tepidique` aversata oculis command.
    
    ```
    sudo fallocate -l 1G /swapfile
    ```
{{< /ordered-list-title >}}

{{< ordered-list-title number="2" title="Remansit notam Stygia feroxque" id="2-Remansit-notam-Stygia-feroxque" >}}
{{< image src="/img/img-exemple.png" alt="This is sample image" >}}
{{< /ordered-list-title >}}
### 2. Remansit notam Stygia feroxque


## Swagger Operation Module

~~The swagger module is currently **configured** to point to the *example data that* swagger hosts. It's a pet store api. [Here's a link](https://petstore.swagger.io/) to the full, swagger-hosted solution. The operation attribute on the following shortcode must match an operation on the pet store api.~~

Currently, this is pointing to *Cludo API's OpenApi* **json file**. The code example output below uses operation `Statistics`.

**Code**

```
{{</* swagger-op operation="pet" */>}}
```

**Output**

{{< swagger-op operation="Statistics" >}}

{{< swagger-op operation="Search" >}}


{{< footer-message >}}