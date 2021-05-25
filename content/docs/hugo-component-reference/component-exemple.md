---
weight: 2
title: "Components Exemple"
---

{{< markdown-with-header title="Example" content="Lorem ipsum">}}
```
{{ <a class="btn" href="#">This is an HTML content</a> }}
```

{{< button relref="#" class="btn btn-gradiant" >}}Button 1{{< /button >}}
{{< button relref="#" class="btn btn-solid" >}}Button 2{{< /button >}}

{{< /markdown-with-header >}} 

## Markdown table

**Code**

```
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
```

**Output**

| Syntax      | Description | Title 1 |
| ----------- | ----------- | ------- |
| Header      | Title       | teste   |
| Paragraph   | Text        | teste   |


## Hints

Hint shortcode can be used as hint/alerts/notification block.
There are 3 colors to choose: `info`, `warning`, `danger`.
### Example

{{< hint info >}}
**Markdown content**  
**Lorem markdownum insigne.** Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
{{< /hint >}}

{{< hint warning >}}
**Markdown content**  
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
{{< /hint >}}

{{< hint danger >}}
**Markdown content**  
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
{{< /hint >}}

