---
weight: 15
bookFlatSection: false
bookCollapseSection: true
title: "Data Indexing"
---

{{< hint warning >}}
 Data indexing requires [basic authentication](../authentication#basic).
{{< /hint >}}

Usually all indexing of pages, files and so on will be handled by the Cludo crawlers, but if necessary, Cludo provides some API endpoints to control the data in your data storage.

The following three endpoints are currently available:

- [pushurls](url-pushing)
- [push](data-pushing)
- [delete](deleting-data)

Typically, pushurls should be used when you just want to add or update content using the supplied crawler's configuration. Use the push endpoint when you want to have total control over the data model indexed, or if you need to index content that is not accessible to the crawler.