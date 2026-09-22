# Planning and route rules

## New-plan checklist

1. Lock fixed transport, tickets, classes, restaurant bookings, and lodging.
2. Record the hotel and exact POIs before sequencing the day.
3. Cluster candidate POIs by area and opening window.
4. Choose a realistic daily load; keep meals and recovery time visible.
5. Build the route in chronological order and research every adjacent leg.
6. Insert transfers only after the route is stable, then adjust event times.
7. Recheck evening return-to-hotel travel and the next morning's start.

## Transfer threshold

- Walking distance `< 1.5 km`: no taxi card by default.
- Walking distance `>= 1.5 km`: create a separate taxi card using current directions data.
- A short geometric distance does not override a materially longer real walking route caused by rivers, highways, restricted entrances, hills, luggage, weather, or accessibility needs.
- Airport, intercity, or luggage transfers should be explicit even when their display conventions differ from ordinary POI transfers.

## Timing

- Use the researched travel duration, not a cosmetic rounded value.
- If directions say 17–24 minutes, schedule at least 24 minutes or a clearly labeled buffer.
- The transfer card fills the entire scheduled transfer interval.
- Avoid overlaps and unexplained gaps. A deliberate gap should be represented as rest, free time, or buffer when it matters to the user.

## Titles and content

- Prefer functional titles such as `古城步行与市场` over dramatic marketing language.
- Describe what is actually planned; do not imply a booking is confirmed when it is tentative.
- When deleting an activity, also remove its map point, transfer dependencies, notes, images, and stale title references.

## Map route

- Default start: the day's hotel.
- Add each distinct activity POI once, in schedule order.
- Add the hotel again only when the itinerary explicitly returns there.
- For a compound event, list all internal stops in `mapPoints`.
