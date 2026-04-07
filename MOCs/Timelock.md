---
title: "Timelock"
type: moc
tags:
  - moc
  - timelock
---

## Overview

Perpetuals without liquidations — a novel financial derivative.

## All Related Notes

```dataview
TABLE date, meeting_type, people
FROM ""
WHERE contains(tags, "timelock")
SORT date DESC
```

## Key People

```dataview
TABLE length(rows) as "Meetings"
FROM ""
WHERE contains(tags, "timelock")
FLATTEN people as person
GROUP BY person
SORT length(rows) DESC
```

## Timeline

```dataview
TABLE title
FROM ""
WHERE contains(tags, "timelock")
SORT date ASC
```
