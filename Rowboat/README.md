---
tags:
  - rowboat
  - index
---

# Rowboat Knowledge Base

Imported from Rowboat on 2026-04-08.

## Summary

| Category | Count |
|----------|-------|
| People | 229 |
| Organizations | 297 |
| Projects | 6 |
| Topics | 14 |
| Fireflies Transcripts | 6 |
| **Total** | **569** |

People merged with existing vault notes: 17

---

## Key Notes

- [[Story - The Journey]] - CK's 9-month arc with chapters
- [[Axis A - Fundraising Journey]]
- [[Axis B - Trading & Market Intel]]
- [[Axis C - VC & Investor Constellation]]
- [[Axis D - Ecosystem Leaders & Advisors]]
- [[Axis E - Career & Life Decisions]]

---

## All People (by relationship strength)

```dataview
TABLE
  role,
  org,
  relationship_type,
  relationship_strength,
  meeting_count,
  last_seen,
  sentiment
FROM "Rowboat/People"
WHERE contains(tags, "person")
SORT relationship_strength DESC
```

## All Organizations

```dataview
TABLE
  type,
  cluster
FROM "Rowboat/Organizations"
WHERE contains(tags, "organization")
SORT file.name ASC
```

## All Projects

```dataview
TABLE WITHOUT ID
  file.link AS "Project",
  file.tags AS "Tags"
FROM "Rowboat/Projects"
WHERE contains(tags, "project")
SORT file.name ASC
```

## All Topics

```dataview
LIST
FROM "Rowboat/Topics"
WHERE contains(tags, "topic")
SORT file.name ASC
```

## Fireflies Transcripts

```dataview
TABLE WITHOUT ID
  file.link AS "Transcript"
FROM "Rowboat/Fireflies"
WHERE contains(tags, "fireflies")
SORT file.name ASC
```

---

## People in Vault (Merged with Rowboat Data)

```dataview
TABLE
  name,
  organization,
  role,
  relationship
FROM "People"
WHERE contains(tags, "person")
SORT file.name ASC
```
