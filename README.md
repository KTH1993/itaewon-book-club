# Itaewon Book Club — website

A single-page site for the [Itaewon Book Club](https://www.meetup.com/itaewon-book-club/):
current read, upcoming schedule, and how to join. Founded and run by Christopher Jones;
site maintained by Taehwan.

Everything is in `index.html` — no build step, no dependencies, no framework.
Open the file in a browser and it works.

## Publishing

The site is served by GitHub Pages from the `main` branch, root folder.
Push to `main` and the live site updates within a minute or two.

## Updating the schedule

Almost every change you'll want to make lives in one array near the bottom of
`index.html`, in the `<script>` block:

```js
var SESSIONS = [
  {
    date: "2026-09-13",        // meeting date, YYYY-MM-DD (Sundays, 4pm)
    title: "Oblomov",
    author: "Ivan Goncharov",
    pages: 500,                // rough page count, for the pace tracker
    kind: "Novel, Russia, 1859",
    note: "One line of context — translation, prize, warning.",
    talk: "Discussion prompts, separated by ·"
  },
  // ...
];
```

Add a meeting by appending an object to the end of the array. Remove the ones
that have passed whenever you like — the page hides them on its own, so there's
no rush.

Two other values in the same script:

- `PREVIOUS_MEETING` — the meeting *before* the first one in `SESSIONS`.
  The reading-pace clock counts from this date. Update it when you delete
  old sessions from the top of the array.
- `MEETUP` — the group URL every "RSVP on Meetup" link points at. If you
  start posting per-event links, give each session its own `url` field and
  use it in the schedule renderer.

The page picks the next meeting that hasn't happened yet and promotes it to
"Reading now" by itself, so the site stays current between edits.

## Things deliberately left out

- **No contact details.** Christopher's phone number and email are on the
  Meetup page; they're not on this site. Ask him before adding either.
- **No member data.** The bookmark tracker, the "I'm in" toggles and the
  shortlist are all stored in each visitor's own browser (`localStorage`).
  Nothing is sent anywhere, and nothing is shared between people. If the club
  ever wants a shared RSVP, that needs a backend — Meetup already does it well.
- **No analytics.**

## Page counts

The counts in `SESSIONS` are approximations used only to drive the pace bar.
Editions and translations vary a lot — that's why the tracker lets each reader
type in their own total.

## License

Content belongs to the Itaewon Book Club. The code is yours to reuse.
