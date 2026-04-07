---
title: "Monad Ecosystem"
type: moc
tags:
  - moc
  - monad
---

## Overview

Monad blockchain ecosystem — strategy, networking, and opportunities.

## All Related Notes

```dataview
TABLE date, meeting_type, people
FROM ""
WHERE contains(tags, "monad")
SORT date DESC
```

## Key People

```dataview
TABLE length(rows) as "Meetings"
FROM ""
WHERE contains(tags, "monad")
FLATTEN people as person
GROUP BY person
SORT length(rows) DESC
```

## Timeline

```dataview
TABLE title
FROM ""
WHERE contains(tags, "monad")
SORT date ASC
```
