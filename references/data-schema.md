# Itinerary data schema

The bundled template uses one `days` array. Each day has:

```js
{
  m: 'OCT',
  d: '01',
  w: '周四',
  city: '目的地',
  title: '务实的当日主题',
  hotel: 'Exact Hotel Name and Address',
  e: [/* events */]
}
```

Each event is an ordered tuple:

```js
[start, end, type, title, note, mapQuery, tag, mapPoints]
```

| Index | Meaning | Requirement |
| --- | --- | --- |
| 0 | `start` | Local `HH:MM` |
| 1 | `end` | Local `HH:MM`, later than start |
| 2 | `type` | `normal`, `break`, `transfer`, or `fixed` |
| 3 | `title` | Concise visible label |
| 4 | `note` | Operational detail, optional |
| 5 | `mapQuery` | Exact Google Maps search query; blank only when no POI applies |
| 6 | `tag` | Short status or context, optional |
| 7 | `mapPoints` | Optional ordered queries for a composite event |

Rules:

- A composite activity's `mapPoints` replaces its single `mapQuery` in the day route.
- A transfer event may leave `mapQuery` blank; its destination is the following event's POI.
- Keep events chronologically sorted and non-overlapping.
- `fixed` renders as transport blue in the bundled template and is intended for booked flights or trains.
- A taxi transfer title uses `打车N分钟 Xkm`; `N` must equal the event's time span.
