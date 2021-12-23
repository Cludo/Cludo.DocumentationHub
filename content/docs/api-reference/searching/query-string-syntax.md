---
weight: 3
title: "Query string syntax"
---


The Cludo query string syntax supports the following command types within the search query string:


- [Operators](#operators)
- [Grouping](#grouping)
- [Sentences](#sentences)
- [Fields](#fields)
- [WildCards](#wildcards)
- [Fuzzyness](#fuzzyness)
- [Ranges](#ranges)
- [Boosting](#boosting)

To avoid expressing everything as one big string, when making requests from a server, See [Filtering](#filtering), and [Ranking](#ranking).

{{< hint warning >}}
 Remember to escape symbols if you wish to search after the symbol and not use it as a command.
{{< /hint >}}


## Operators

When making a search such as `school activity`, it is usually interpreted as `school` OR `activity`, meaning that either term must match. It is possible to specify operators to control the search further. Operators supported are:

- **AND**
- **OR**
- **NOT**

You may also use symbols instead of words:

- **&&**
- **||**
- **!**

Each operator operates on the 2 terms next to it, except `NOT` which only negates the term to the right. However, take notice that `NOT` takes precedence over `AND`,
which again takes precedence over `OR`. Another way to control the search is to use `+` and `-` just before a term. The search string: `insurance +car -bike` states that *car* must be present, *bike* must not be present, and insurance is optional, but its presence increaces the scoring.



## Grouping

Multiple terms can be grouped together with parentheses, to form sub-queries:

`(mint OR new) AND condition`

{{< markdown-with-header title=""  content="Examples on using grouping:">}}
```
(Harvard OR Oxford OR Princeton) AND University
(Harvard Oxford Princeton) AND University
(Hamster OR ginny AND pig) AND (Food OR nutrition)
```
{{< /markdown-with-header >}} 

## Sentences

To match a specific sentence, simply wrap the terms with quotes:

`"Quick brown fox"`

This enforces that all terms must be found, and in the order specified. It's possible to use [fuzzyness](#fuzzyness) on sentences to allow unknown terms to occur between the terms specified, but the order of the terms must still be the same. To do this use `~`:

`"Quick fox"~`

{{< markdown-with-header title=""  content="Examples on using sentences:">}}
```
"Tax deductions"
"car repair"~4
```
{{< /markdown-with-header >}} 

## Fields

To search only within a specific field, add the field name before the search:

`Title:Taxdeductions`

or to match a sentence in a field:

`Title:"Car insurance"`

{{< markdown-with-header title=""  content="Examples on using fields:">}}
```
Title:school
Title:"news channel"~3
food AND (Title:"animal (store OR shop)"~2)
```
{{< /markdown-with-header >}} 

## WildCards

Searching with wildcards lets the searchengine insert zero or more characters within the string, in an attempt to match results. Use `?` to specify a single character wildcard and `*` to specify a zero or more characters wildcard. Both and multiple may be used simultaneously.

For example: `*bike` will match *bike*, *mountainbike*, *citybike* and other terms ending with bike, wheras `si?e` will match *site* and *size* but not *resize*.

{{< hint warning >}}
 <b>Please note</b>

  we perform stemming on content that is indexed, and that queries containing wildcards won't be stemmed. That means you will need to keep your query within the boundaries of the stem to match the content.
  The stemming is language specific, but an example for an English index could be the word  <b>community</b>, the stem of which is  <b>commun</b>.

The following queries <b>would</b> match:
- com*
- commun*

The following queries would <b>not</b> match:
- communi*
- community*
{{< /hint >}}

{{< markdown-with-header title=""  content="Examples on using wildcards:">}}
```
school*
ba?k
analy*
```
{{< /markdown-with-header >}} 

## Fuzzyness

Fuzzyness helps with misspellings, by allowing insertion, deletion, substitution or transposition of characters. To allow fuzzyness add `~` to the end of a word. The amount of fuzzyness allowed may be specified by adding a number such as `~2`. Fuzzyness are also available to sentences, to allow extra terms between the ones written.

`"Car insurance"~2` will match `"Car and motorcycle insurance"`, since `~2` allows up to 2 extra terms between the specified terms.

The less changes to a search, the more relevant scoring will the search result get.

{{< markdown-with-header title=""  content="Examples on using fuzzyness:">}}
```
trukc~   -> truck  (transposition)
bron~    -> brown  (insertion)
schoool~ -> school (deletion)
skhool~  -> school (substitution)
```
{{< /markdown-with-header >}} 

## Ranges

To search for ranges of numbers, dates or strings, use square bracks to specify inclusive ranges `<field>:[min TO max]` and exclusive ranges with curly brackets `<field>:{min TO max}`. It is allowed to mix inclusive and exclusive ranges, and if an open range is required, use `*` as value.

{{< markdown-with-header title=""  content="Examples on using ranges:">}}
```
Price:[20 TO 40]
ProductionYear:[2016 TO 2017]
ShoeSize:[8 TO *]
Price:[20 TO 40}
```
{{< /markdown-with-header >}} 

## Boosting

Sometimes, to the user, one term is more important than another.
To indicate this importance to the search engine, add a boosting score to terms with `^#` where # is the boosting factor.
The boost value must be a positive number, and decimals are allowed.
A boosting value between 0 and 1 reduces the importance of a word, whereas one over 1 increases the importance.

{{< markdown-with-header title=""  content="Examples on using boosting:">}}
```
car^2 bike
hamster^2 "ginny pig"
vodka^0.5 gin^2 "white wine"^3
```
{{< /markdown-with-header >}} 