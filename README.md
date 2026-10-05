# Itaewon Book Club — website

A single-page site for the [Itaewon Book Club](https://www.meetup.com/itaewon-book-club/):
current read, upcoming schedule, and how to join. Founded and run by Christopher Jones;
site maintained by Taehwan.

Everything is in `index.html` — no build step, no dependencies, no framework.
Open the file in a browser and it works.

## Publishing

The site is served by GitHub Pages from the `main` branch, root folder.
Push to `main` and the live site updates within a minute or two.

Live at **https://itaewon.club**.

## Domain and email

- **Domain:** `itaewon.club`, registered with Cloudflare Registrar. DNS is on
  Cloudflare too.
- **Website:** the apex domain points at GitHub Pages (four `A` records plus
  four `AAAA` records), and `www` is a `CNAME` to `kth1993.github.io`. The
  `CNAME` file in this repo tells GitHub Pages which domain it serves — don't
  delete it.
- **Email:** `contact@itaewon.club` is handled by Cloudflare Email Routing
  (the `MX` and SPF records are managed by Cloudflare). Incoming mail is
  forwarded to Taehwan's Gmail; replies go out from Gmail's "Send mail as"
  using that address. There is no separate mailbox to log in to.

## Updating the schedule

The schedule mirrors the group's [Meetup events](https://www.meetup.com/itaewon-book-club/events/).
Almost every change you'll want to make lives in one array, `BOOKS`, in the
`<script>` block near the bottom of `index.html`:

```js
var BOOKS = [
  {
    date: "2026-10-25",          // meeting date, YYYY-MM-DD (Sundays, 4pm)
    title: "The Last of the Just",
    author: "Andre Schwarz-Bart",
    url: "https://www.meetup.com/itaewon-book-club/events/315102463/",
    cover: "",                   // optional, see below
    tint: "#e6e1d4", on: "#2b2a26"
  },
  // ...
];
```

- Add a meeting by appending an object to the end, oldest first.
- `url` is the Meetup event page. The RSVP button opens it; leave it out and
  the button falls back to the group page.
- `cover` is optional. When it's empty the page looks the book up on Open
  Library; if nothing is found it draws a plain cover from `tint` (background)
  and `on` (text colour).
- Past meetings stay in the timeline as "Already read". Delete old ones from
  the top whenever the list gets long.

The page opens on the next meeting that hasn't finished yet, so the site stays
current between edits.

Two other values in the same script:

- `VENUE` / `VENUE_MAP` — where upcoming meetings happen (currently
  The Craic House, Itaewon) and the map link. Change both if the venue moves.
- `MEETUP` — the group URL, used by "Join on Meetup" and as the RSVP fallback.

## Impersonation notice

The banner at the very top says the club never contacts anyone first to ask for
money or promotion, in English and Korean. Visitors can close it; it stays
closed for 30 days in their browser and then shows again once. The wording is
in the `<aside class="notice">` at the top of `<body>`.

## Things deliberately left out

- **No personal contact details.** The only address on the site is the club's
  own `contact@itaewon.club` (in the notice, under the organiser's name and in
  the footer). It's assembled by the script rather than written into the HTML,
  so address-harvesting bots don't pick it up. Christopher's phone number and
  personal email are on the Meetup page; they're not on this site. Ask him
  before adding either.
- **No member data.** Nothing about visitors is collected or sent anywhere. The
  browser only remembers which cover image was found for each book and whether
  the notice was closed (`localStorage`). If the club ever wants a shared RSVP,
  that needs a backend — Meetup already does it well.
- **No analytics.**

## License

Content belongs to the Itaewon Book Club. The code is yours to reuse.
