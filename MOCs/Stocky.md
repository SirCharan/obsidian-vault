---
title: "Stocky"
type: moc
tags:
  - moc
  - stocky
---

## Overview

AI-powered trading system — satellite data, multi-agent analysis, global markets.

## All Related Notes

```dataview
TABLE date, meeting_type, people
FROM ""
WHERE contains(tags, "stocky")
SORT date DESC
```

## Key People

```dataview
TABLE length(rows) as "Meetings"
FROM ""
WHERE contains(tags, "stocky")
FLATTEN people as person
GROUP BY person
SORT length(rows) DESC
```

## Timeline

```dataview
TABLE title
FROM ""
WHERE contains(tags, "stocky")
SORT date ASC
```
