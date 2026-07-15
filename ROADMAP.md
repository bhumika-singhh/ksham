# Roadmap

Ideas that came out of real user feedback, and the thinking behind them.

---

## Allowed tabs (up to 3) — future update

**Where this came from:** a friend testing Ksham said she studies with PDFs open and uses AI to help
her learn, so she needs to reach a couple of other tabs without the alarm screaming at her.

### The constraint (read this first)

**A website cannot see your other tabs.** The Page Visibility API — the thing Ksham uses today — only
reports that *this* tab lost focus. It cannot report *where you went*. Browsers deliberately forbid a
page from inspecting other tabs, their URLs, or the site you switched to. This is a security boundary,
not a limitation of the code.

So the obvious version of this feature — *"allow these 3 tabs, ring for everything else"* — **is
impossible to build honestly as a website.** Anything claiming to detect ChatGPT vs Instagram would be
a lie, and Ksham does not lie to its users.

Two things follow from that:

1. The alarm's trigger cannot be **place**. It can only be **time**.
2. The allowed-tabs list is therefore not a filter Ksham *enforces*. It's a **promise the user makes** —
   the same honor system already used by *"did you actually do it?"*, just moved to the start of the
   session.

### The design

Two modes, decided by whether the user declares anything.

**Strict mode** — nothing declared. Today's behavior, unchanged and still the default.
- Leaving the tab means drifting.
- Timer pauses, bell rings immediately.

**Open mode** — 1–3 allowed tabs declared before starting.
- The user names up to 3 resources they'll legitimately need (e.g. `my PDF`, `chatgpt.com`, `notes`).
- The user also declares **their own grace window** — roughly how long they expect to be away at a
  time (e.g. ~4 minutes).
- Leaving the tab no longer means drifting. **The timer keeps running**, because reading your PDF *is*
  the work. This is the real change the feature makes.
- No instant alarm. The declared tabs are shown on screen as a quiet reminder of what was promised.
- The bell rings only when the user exceeds **their own stated window** — not an arbitrary number
  Ksham picked.

### Why the bell keeps its meaning

The worry: *"if we ring only after a threshold, the whole point of the bell is gone."*

It isn't, for three reasons:

1. **Strict mode is still the default.** The sharp, instant bell is what most sessions get. Open mode
   is opt-in, for when you genuinely need resources.
2. **The bell now enforces your word, not Ksham's rule.** You set the window. Breaking it is breaking
   your own promise — which is exactly the contract Ksham already runs on. Set it to 30 minutes to
   game it and you already know you cheated. That's between you and you.
3. **This trade was already made.** Someone can click "yes, I did it" after 25 minutes of YouTube.
   Ksham never could stop that and never tried. Declaring "my PDF" and then scrolling Instagram is the
   same dishonesty, costing the same thing: nothing but your own progress. The bell was never a cop.

### Known tension

Time cannot cleanly separate a long, legitimate study stretch from a long drift. Any threshold will
sometimes be wrong. The honest choice is *which* error to prefer — punishing real work, or occasionally
missing real drift. Open mode chooses the latter, and lets the user set the line.

### Alternative considered: browser extension

An extension *can* read tab URLs and would do the literal thing requested. Rejected for now because:
- It's a different product (extension code, store review, users must install it).
- It makes Ksham something that **watches you**, which contradicts the whole philosophy.

---

## Shipped instead: read your study material inside Ksham

Rather than working around the tab problem, the better fix for the original complaint was to remove the
tab switch entirely. You can now load **PDFs and images** directly into Ksham and read them in place:

- **Multiple files** can be loaded at once — PDFs and images side by side — with a tab strip in the
  reading view to switch between them. More can be added mid-session, and any can be removed.
- Images (photos of notes, diagrams, slides) render in a fitted viewer; PDFs use the browser's native
  viewer. Anything that isn't a PDF or image is rejected with a gentle message.
- The files **never leave the device** — they're read locally via object URLs, nothing is uploaded.
- No tab switch means **nothing to detect, no alarm to dodge, and the timer just keeps running.**
- Solves the PDF/notes half of the original request completely and honestly.

This does not cover AI sites — ChatGPT and most others block embedding — so the allowed-tabs design
above still matters for that half.

### Known limitations

- **No size cap is imposed.** Nothing is uploaded, so there's no server limit; object URLs reference the
  file on disk rather than loading it into memory. The real ceiling is device RAM and the browser's PDF
  viewer — typical study PDFs (a few MB to ~50MB) are fine; hundreds of MB may get sluggish.
- PDFs are per-session. Session persistence restores the timer, but files can't be stored in
  `localStorage`, so they must be re-picked after a refresh.
- PDF-in-iframe rendering is unreliable on iOS Safari.

---

## Smaller ideas

- Hide the support button while a session is active, to keep the focus screen clean.
- Cloudflare Web Analytics, to see real usage once shared.
- A custom domain, replacing the `workers.dev` URL.
