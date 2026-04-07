---
title: "Fundraising"
type: moc
tags:
  - moc
  - fundraising
---

## Overview

Investment rounds, valuations, investor meetings, and pitch strategy.

## All Related Notes

```dataview
TABLE date, meeting_type, people
FROM ""
WHERE contains(tags, "fundraising")
SORT date DESC
```

## Key People

```dataview
TABLE length(rows) as "Meetings"
FROM ""
WHERE contains(tags, "fundraising")
FLATTEN people as person
GROUP BY person
SORT length(rows) DESC
```

## Timeline

```dataview
TABLE title
FROM ""
WHERE contains(tags, "fundraising")
SORT date ASC
```
