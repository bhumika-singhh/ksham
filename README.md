# Ksham — the patience to return

A minimal focus timer built on honesty instead of locks.

Most focus apps treat you like a child — they block sites, lock your phone, and assume you can't be
trusted. Ksham does the opposite. It assumes you're an adult who wants to do good work and sometimes
drifts, and it helps you build the two things that actually matter: **focus**, and the
**responsibility to keep your word to yourself**.

The name means *forgiveness* — the kind you give yourself when you drift, and come back anyway.

## How it works

1. **Name the one thing** you'll do right now. You can't start without it.
2. **Pick a length** — 5, 25, 45, or 60 minutes — and focus.
3. **Stay on the tab.** If you drift away, Ksham rings a bell to call you back. It never blocks
   anything; it just refuses to let you wander off without noticing.
4. **Return.** The timer picks up exactly where it left off. There's no penalty for having left.
5. **Answer honestly.** When time's up, Ksham asks: *"Did you actually do it?"* Nothing verifies your
   answer — the whole thing runs on your word.
6. **Build the streak.** Every honest yes grows your streak of honest focus. An honest no resets it,
   gently, and you begin again.

## What it's built on

- **Honesty** — Ksham can't check whether you worked. Only you know. That's the point.
- **Responsibility** — every session is a rep in keeping your word to yourself.
- **Respect** — you're treated like an adult, not something to be managed.
- **Forgiveness** — drifting is human. Returning is the whole practice.

## Tech

No frameworks, no build step, no accounts, no tracking. Just static HTML, CSS, and vanilla JS.
Sessions and streaks are stored in `localStorage`. Tab-focus detection uses the Page Visibility API.

```
index.html     the timer
how.html       how it works
blog.html      why I built it
support.html   support the project
crisis.mp3     the recall bell
```

To run it locally, serve the folder with any static server and open `index.html`.

## Support

Ksham is free, and it always will be. If it helped you sit down and do the thing, you can
[buy me a coffee](https://ko-fi.com/bhumika_singh) or [buy me a chai](https://buymeachai.in/bhumikasingh).

---

love, bhumi xx
