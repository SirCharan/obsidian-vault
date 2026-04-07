---
title: "Fuze"
type: moc
tags:
  - moc
  - fuze
---

## Overview

FinTech platform — wealth products, payments, stablecoin infrastructure across 15 countries.

## All Related Notes

```dataview
TABLE date, meeting_type, people
FROM ""
WHERE contains(tags, "fuze")
SORT date DESC
```

## Key People

```dataview
TABLE length(rows) as "Meetings"
FROM ""
WHERE contains(tags, "fuze")
FLATTEN people as person
GROUP BY person
SORT length(rows) DESC
```

## Timeline

```dataview
TABLE title
FROM ""
WHERE contains(tags, "fuze")
SORT date ASC
```
