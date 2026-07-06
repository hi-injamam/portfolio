---
title: "How I built this site: Jekyll, a CMS, and a Cloudflare relay"
date: 2026-07-06 09:00:00 +0600
tag: "Tooling"
excerpt: "The story behind this portfolio — a scrollytelling CV, a headless CMS I can edit from the browser, and the OAuth relay that quietly holds it all together."
---

I wanted a portfolio that read less like a résumé and more like a walk through the work. The result is the site you're on: a single scrolling story, editable from a browser, hosted for free, on my own domain. Here's how the pieces fit — and where they fought back.

## Start with the story, not the stack

The homepage is built around one idea: a career drawn as a single line you scroll down, with each role landing as you go. That decision came before any technology choice. Everything after it — the fonts, the palette, the little cursor effects — exists to serve that spine, not to show off.

Building it as one self-contained page first was the right move. No framework, no build step, just HTML, CSS, and vanilla JavaScript I could reason about end to end. When something looked wrong, there was exactly one place to look.

## Turning a page into a site

A single file is great until you want to *edit* it without touching code. So the next job was converting it into a proper Jekyll site: content pulled out into a data file, the layout templated, a blog folder added, and the whole thing wired to build automatically. GitHub Pages compiles it on every push and serves it — no server for me to run, nothing to patch at 2am.

The lesson that kept repeating: separate the content from the presentation early. Once the copy, the roles, and the case studies lived in their own data file, the page became something I could feed rather than rewrite.

## The part that earns its keep: a CMS I can actually use

Editing raw files is fine for a developer and miserable for everyone else — including future me on a phone. So the site runs a headless CMS. I open a dashboard, change words in normal form fields, hit publish, and it commits the change and redeploys on its own. No terminal, no git, no YAML.

The catch is authentication. The CMS needs permission to write to the repository, and that handshake can't happen safely from a static site alone — there's no server to hold the secret half of the login. The usual answer is a hosted service that does it for you. I didn't want a dependency I couldn't see into.

## A tiny relay, doing one honest job

The fix was a small piece of code running on Cloudflare's edge — a worker whose entire purpose is to stand between the CMS and GitHub during login. The CMS sends a visitor to it, it adds the credentials it's holding, forwards them to GitHub's authorization screen, and hands the resulting token back. Perhaps forty lines of logic. Free to run. Mine to inspect.

Getting it live was the humbling stretch. The build tooling swapped package managers underneath me, a config file existed only as a template that had to be copied into place, the public URL shipped switched off by default, and — the one that cost the most time — the login kept sending a blank credential to GitHub. That last one looked like a code bug and turned out to be the login secrets not binding to the deployed version until they were removed and re-added in the right order. A clean delete, a clean re-add, and the authorization screen finally appeared.

## What the whole thing taught me

Three things stuck.

First, the boring layer is the one that breaks. The story, the design, the writing — those went smoothly. It was package managers, config templates, and credential binding that ate the hours. Infrastructure doesn't care how good your idea is.

Second, read the error, not your assumptions. The blank-credential failure looked like one thing and was another. Every real fix in this project started with reading the actual log line instead of guessing from the symptom.

Third, owning the small pieces is worth it. I could have handed the login off to a managed service and saved an afternoon. But now nothing in this site is a black box to me, and when it breaks again — it will — I'll know exactly where to look.

The site is live, it costs nothing to run, and I can change every word of it from a browser. That was the whole point.
