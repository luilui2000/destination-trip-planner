---
name: destination-trip-planner
description: Research, create, audit, or update an hour-by-hour travel itinerary with precise POI mapping, route-aware timing, semantic activity cards, transfer cards, and an interactive HTML map. Use for destination guides, multi-day trip plans, itinerary HTML, or requests that add, remove, move, or replace stops while keeping travel time and map routes consistent.
---

# Destination Trip Planner

Create a realistic itinerary that remains internally consistent after every edit. Treat time, place, route, and presentation as one connected system.

## Choose the working mode

- **Create:** research the destination, draft the itinerary data, then build the HTML from `assets/itinerary-template.html`.
- **Update:** inspect the existing artifact and preserve its visual language and unrelated user edits. Change only what the request requires, plus dependent times, transfers, and map points.
- **Audit:** report route, opening-hours, timing, or workload problems without changing files unless the user asks for changes.

If an existing itinerary or source file is available, read it before asking questions. Ask only for missing choices that materially change the plan, such as destination, dates, hotel area, fixed bookings, or pace.

## Research current facts

Browse for details that can drift: opening days and hours, closures, reservation requirements, exact addresses, seasonal conditions, walking distance, driving distance, and driving time. Prefer official venue pages and current map/directions results. State when a value is an estimate.

Do not invent precise travel times. Preserve the map result or an honest range; do not normalize every duration to multiples of five or ten.

## Plan by geography and energy

Group nearby POIs, respect fixed bookings, and avoid unnecessary backtracking. Include meals, hotel breaks, weather buffers, and realistic visit duration. Put high-effort or outdoor items earlier when practical. Keep optional items visibly optional rather than silently overloading the day.

Read `references/planning-rules.md` when creating a new multi-day plan or substantially rerouting a day.

## Apply the atomic update rule

For **every** added, removed, moved, renamed, or retimed activity, complete all of the following before considering the update finished:

1. Update the visible time and content.
2. Resolve the exact POI and use a stable, specific map query or address.
3. Identify the previous and next mappable POIs.
4. Check walking distance plus driving time and distance for both adjacent legs.
5. If walking distance is **1.5 km or more**, add a separate blue transfer event covering the full travel interval. Its visible title must be `打车N分钟 Xkm`.
6. If walking distance is under 1.5 km, do not add a transfer card unless the user requests one; walking can be mentioned in the activity note.
7. Shift dependent events as needed so cards neither overlap nor imply impossible travel.
8. Update the single-POI map target and the full-day route order. A transfer card is not itself a map stop.

When a route estimate is a range, use the conservative value for the timetable and explain the range in the note if useful.

## Preserve the card semantics

- `transfer`: blue — flights, trains, taxis, airport or hotel transfers.
- `break`: green — meals, hotel check-in, rest, and hotel time.
- `normal`: orange — sightseeing, shopping, classes, spa, cafés, bars, and other activities.

Transfer cards must occupy their actual duration; their time span and the minutes stated in their title must match. Do not combine arrival transport and hotel check-in into one card.

Read `references/data-schema.md` when modifying the provided template or an itinerary that follows its tuple schema.

## Keep the map trustworthy

- Use the hotel as the day's starting point unless the itinerary begins elsewhere.
- Day-route mode must list mappable stops in chronological order.
- Composite activities may provide multiple ordered map queries.
- Use exact venue names and addresses when similarly named POIs exist.
- Prefer Google Maps visual output when requested. A keyless Google Maps embed is acceptable for simple place or route display; do not claim API-only features are available without a configured key.

## Verify before delivery

After an HTML edit:

1. Search for removed or superseded text and confirm it no longer appears.
2. Check times, overlaps, card types, map queries, route ordering, and adjacent transfers.
3. Run `node scripts/validate_itinerary_html.mjs <html-file>` from this skill folder. Resolve errors; review warnings.
4. Open or render the result when UI layout may have changed, especially on narrow screens.
5. Report the changed schedule, any added or omitted transfer cards, and the verified file link.

Do not add decorative images unless the user requests them. Do not overwrite unrelated local changes.
