---
title: "Static site, real CMS, zero servers"
date: 2026-07-11
description: "How this blog works: markdown in a GitHub repo, rendered by Jekyll on GitHub Pages, written from a hosted rich-text dashboard — no servers, no database, no build pipeline to babysit."
---

This site is deliberately boring infrastructure: hand-written HTML and CSS on GitHub Pages, no frameworks, no build step. Adding a blog usually breaks that — a "dashboard with a login" sounds like a server, a database, and a monthly bill.

It doesn't have to be. Here's the whole stack behind the post you're reading:

## The publishing path

1. I write in [Pages CMS](https://pagescms.org) — a hosted dashboard with a rich text editor and image uploads. Login is just my GitHub account.
2. Hitting publish commits a markdown file to this repo, images included.
3. GitHub Pages notices the push and runs Jekyll — the static site generator it has had built in since forever — which turns the markdown into a real HTML page.

No servers of mine anywhere in that path. The "database" is a git history, which means every post is version-controlled, diffable, and portable by default.

## Why not client-side rendering?

The tempting shortcut is to fetch markdown with JavaScript and render it in the browser — zero build, fully static. The problem is sharing: LinkedIn's link crawler doesn't execute JavaScript, so every shared post would show the same generic preview card.

Jekyll renders each post to its own URL with its own Open Graph tags at deploy time:

```html
<meta property="og:title" content="Static site, real CMS, zero servers">
<meta property="og:type" content="article">
<meta property="og:image" content="https://anthonyboffman.com/assets/og-image.png">
```

That's the difference between a link and a card.

> The best infrastructure is the kind you can explain in three bullet points and forget about for a year.

## What it costs

Nothing. GitHub Pages hosting is free, Jekyll runs inside it, and Pages CMS is free for this use case. The only maintenance surface is a single YAML config file in the repo.
