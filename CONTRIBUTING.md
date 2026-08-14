# Updating the site

The site used to be a Django app with an admin panel you logged into. It is now
a set of files in this repository, and GitHub rebuilds and publishes the site
automatically within a minute or two of a change landing on `main`.

You do not need to install anything. Every task below can be done from
github.com: open the file, click the pencil icon, edit, and click
**Commit changes**. If you are not sure about a change, commit it to a new
branch and open a pull request so someone else can look first.

Dates, names and links are copied verbatim onto the site, so double-check
spelling before committing.

---

## Add a meeting

Meetings are files in the `_posts/` folder. **The filename matters**: it must
start with the meeting date as `YYYY-MM-DD`, followed by a short name made of
lowercase letters, numbers and hyphens. That short name becomes the page's web
address.

```
_posts/2026-03-31-s26-m5.html   ->   https://miamicyber.org/s26-m5/
```

The homepage groups meetings into semesters automatically from the date —
January through July is Spring, August through December is Fall. You never write
the semester anywhere.

### If the meeting is just a slide deck

This is the common case. Create the file, paste this in, change the four values,
done. There is no body to write.

```
---
layout: redirect
title: "Fall 2026 - Meeting 1: Getting Started"
date: 2026-09-02
author: President
external_url: "https://docs.google.com/presentation/d/PASTE_THE_LINK_HERE/edit?usp=sharing"
sitemap: false
---
```

`author` is whatever should show in the middle of the card on the homepage —
usually a role like `President`, not a person's name.

### If the meeting has a write-up on the site

Use `layout: post` instead, leave out `external_url`, and write the body below
the second `---`. The body is HTML, so use `<p>` around paragraphs, `<br>` for a
line break, `<b>` for bold, and `<a href="...">` for links.

```
---
layout: post
title: "Fall 2026 - Meeting 2: Insider Threats"
date: 2026-09-09
author: President
---
<p>A short description of the meeting.</p>
<p><b>When:</b> Wednesday, 6:30 - 7:30 PM<br><b>Where:</b> McVey 126/128</p>
<p><b>Meeting Link:</b> <a href="https://meet.google.com/xxx-xxxx-xxx">Join here</a></p>
```

Every past meeting is already in `_posts/`, so the closest thing to what you are
writing is almost certainly sitting right there — copy it and edit. Two to start
from:

- `_posts/2026-03-31-s26-m5.html` — a meeting with a write-up
- `_posts/2026-03-04-spring-2026-meeting-4-nation-state-actors.md` — a link-only meeting

---

## Update the executive board

Edit `_data/officers.yml`. One block per person:

```yaml
- name: "Jane Doe"
  position: "President"
  rank: 0
  linkedin: "https://www.linkedin.com/in/jane-doe/"
  photo: "/assets/img/exec/jane-doe.jpg"
```

- `rank` controls the order on the page, low to high. Use the standard numbers
  listed in the comments at the top of `officers.yml` (President is 0, Vice
  President is 1, and so on) so the board always renders in the same order.
- `linkedin` and `photo` are both optional. Leave `linkedin` out and no LinkedIn
  icon appears. Leave `photo` out and the Anonymous emblem placeholder is used.
- For a photo, upload the image into `assets/img/exec/` first (on github.com:
  open that folder, **Add file → Upload files**), then point `photo` at it. Name
  the file after the person, like `jane-doe.jpg`, to match the others. A square
  image around 300×300 looks best — it is displayed as a 130px circle, so please
  resize before uploading rather than committing a multi-megabyte photo.

At the end of the year, move the outgoing officers' blocks into
`_data/alumni.yml`, dropping the `rank` and `photo` lines (alumni photos are not
shown) and setting `position` to the highest position that person held.

---

## Add or remove a sponsor

Edit `_data/sponsors.yml`:

```yaml
- company_name: "Example Corp"
  logo: "/assets/img/sponsors/example-corp.png"
  website_link: "https://example.com"
  color: "#8C140C"
  content: "A short thank-you blurb."
```

Upload the logo into `assets/img/sponsors/` first. `color` sets the stripe down
the left edge of the card — use the company's brand color, or leave it out for
the default red. `website_link` and `content` are optional.

To remove a sponsor, delete their block. Sponsors appear in the order they are
listed in the file. While the file has no sponsors in it, the sponsors page just
shows the "Support Us" and "How to support" cards.

---

## Change the typing animation in the header

Edit `_data/banner.yml`. Entries without `show_mobile` are typed out on desktop;
an entry marked `show_mobile: true` is used on phones instead, so keep that one
short (about 10 characters).

```yaml
- message: "sudo rm -rf /*"
- message: "MUCSC"
  show_mobile: true
```

## Put a notice at the top of the homepage

Edit `_data/alert.yml` and fill in `message`. Set it back to `""` to remove the
box.

```yaml
message: 'No meeting this week — <a href="https://discord.gg/k5fvEVTyB5">see Discord</a>.'
```

## Add CTF results

Edit `_data/ctftime.yml`, newest season first. CTFtime blocks automated
scraping, so these numbers are copied by hand from
<https://ctftime.org/team/214233>.

```yaml
- year: "2026"
  place: "1234"
  points: "12.345"
  events:
    - place: "42/900"
      name: "Some CTF 2026"
      link: "https://ctftime.org/event/0000"
      points: "1500.0000"
      rating: "3.210"
```

---

## Running the site on your own machine

Only needed if you are changing the layout or styles.

```sh
bundle install
bundle exec jekyll serve
```

Then open <http://localhost:4000>. The site rebuilds as you save files.

## If a change does not show up

Check the **Actions** tab in GitHub. A red X means the build failed — click into
it to see the error. The most common cause is a YAML mistake in a `_data/` file:
inconsistent indentation, or a value containing a `:` or `#` that is not wrapped
in quotes. When in doubt, wrap the value in double quotes.
