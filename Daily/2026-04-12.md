---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - daily
---

## Focus Today
-

## Tasks Due Today

```tasks
not done
due on <% tp.date.now("YYYY-MM-DD") %>
```

## Meetings Today

```dataview
TABLE title, meeting_type, people
FROM ""
WHERE date = date("<% tp.date.now('YYYY-MM-DD') %>")
AND type = "meeting"
```

## Notes
-

## End of Day Review
-
