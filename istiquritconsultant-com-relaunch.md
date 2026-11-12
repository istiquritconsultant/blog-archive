# istiquritconsultant.com Re-Launch: A Build Log for a Hand-Coded PHP Tech Diary

## TL;DR

istiquritconsultant.com Re-Launch turns a retired consulting domain into a version-controlled PHP tech diary with Markdown posts, six categories, and nine three.js mini-games — no sales pitch, just build notes.

The **istiquritconsultant.com Re-Launch** is live as of August 24, 2026, and if you're the kind of reader who wants to know what's actually running under the hood before you subscribe to anything, this post is for you. istiquritconsultant.com used to be the business domain for "Istiqur IT Consultant." That business rebranded earlier in 2026 to Remote SEO Consultant, because a person's name doesn't match what people type into a search bar when they're trying to solve a problem. Rather than let the old domain sit idle or redirect to nowhere, it got rebuilt — from the ground up — into a personal, non-commercial tech diary, written and maintained by Md. Istiqur Rahman, the same person behind Remote SEO Consultant.

This is a build-log write-up: what shipped, why, and how the stack is put together, since that's the angle this platform's readers actually care about.



## Why the Relaunch Happened

The old brand name, "Istiqur IT Consultant," described a person, not a problem. Nobody searches for a person's name when they're stuck debugging a build error at 1 a.m. — they search for the error. That mismatch pushed the business side to rebrand to Remote SEO Consultant earlier in 2026, which left the original domain, istiquritconsultant.com, without a commercial job to do.

Instead of parking it or 301-redirecting it into oblivion, the decision was to repurpose it as a dedicated reading space — a tech diary with its own identity, separate brand system, and zero commercial pressure. That repurposing went live on August 24, 2026, as the istiquritconsultant.com Re-Launch.

## What's Live Now: Categories and the First Post

The site launched with six content categories, each with its own landing page and its own themed mini-game:

- **AI** — no posts published yet, but expected to grow fastest
- **Workflow Optimization** — where the first post lives
- **Windows**
- **Linux**
- **Self-Hosting**
- **Tech Journey** — the long arc of how a pharmacist became a technologist

The first published post is **"OpenCode Not Working: Why Both CLI & Desktop Died"** (https://istiquritconsultant.com/workflow-optimization-blogs/opencode-not-working-windows-11/). It's a real incident writeup: both the OpenCode CLI and the OpenCode Desktop app refused to start after five custom subagents were added. The post walks through the exact error text, isolates the root cause down to a single misconfigured field, and documents how both the CLI and the desktop app were fixed and independently verified. If you've ever lost an hour to a tooling crash that turned out to be one field in a config file, this is the kind of post the whole site is built around.

## The Brand and the Build

Since this platform's readers are repo-and-code-literate, here's the actual stack rather than a marketing gloss:

- **Backend:** hand-coded PHP — no CMS, no framework abstraction layer sitting between the code and the content
- **Content:** Markdown-based, version-controlled, so every post has a real history
- **Current build:** 2.1.1
- **Infrastructure:** Cloudflare for DNS and performance, LiteSpeed page cache for serving speed
- **Analytics:** Google Analytics 4
- **Indexing:** IndexNow, for faster discovery by search engines
- **Fonts:** self-hosted, no third-party font CDN calls

The brand system is deliberately separate from Remote SEO Consultant's own violet identity. istiquritconsultant.com runs on Signal Emerald green (#0E8F5E as the brand color, #0D8557 as a text-safe variant, #123B2C as deep support), on a near-black dark base of #0B1215 — the site defaults to dark mode — with a soft light base of #F9FDFE available. The logo is a ribbon-bookmark mark in a "Clear Glass" treatment. Headlines run in Bodoni Moda, a serif, with body copy in Hanken Grotesk, a grotesque sans. It's a distinct visual system on purpose, so there's no confusion between the commercial brand and the personal diary.

One more build detail worth flagging for this audience: there are nine playable mini-games built with three.js scattered across the site. Six are themed to the six content categories — Signal Runner for AI, Workflow Sprint for Workflow Optimization, System Defender for Windows, Terminal Chase for Linux, Uptime Runner for Self-Hosting, and Duck Hunt for Tech Journey. The remaining three live outside the category pages: Breakout on the homepage, Journey Snake on the About page, Catch the Signal on the Contact page, and there's a bonus game embedded directly on the OpenCode post itself.

## Explicitly Not a Sales Funnel

This matters enough that it's stated directly on the homepage: "no pitch inside the posts." The posts aren't lead magnets. There's no CTA stapled to the bottom of every article pushing a service. The commercial SEO, go-to-market, and web-dev consulting work stays entirely on remoteseoconsultant.com, and it's referenced exactly once — from the About page — as a separate, clearly labeled paid engagement. Everywhere else, it's just the diary.

## The Newsletter Proof Point

As of the relaunch, the newsletter sits at 5,078+ subscribers. It's one post per send — no digest bundling, no batching multiple posts into a weekly roundup — and unsubscribing is a single click. Subscriber data is never sold or rented. For a tech-diary format, that subscriber count is a reasonable proxy for "people actually want the unfiltered build notes," which is the whole premise of the site.

## How It Connects to Remote SEO Consultant

The through-line is the author, not the brand. Md. Istiqur Rahman runs Remote SEO Consultant commercially and writes istiquritconsultant.com personally. The two are kept visually and functionally separate — different domains, different color systems, different purposes — but they're the same person applying the same build-in-public habit that shows up in client work: document the problem, document the exact fix, make it verifiable.

I walked through the whole relaunch — the brand decisions, the stack, the category structure — in a short video: [https://www.youtube.com/watch?v=_bmAXUClHVk](https://www.youtube.com/watch?v=_bmAXUClHVk). If you want the announcement in long form, it's here: [https://remoteseoconsultant.com/istiquritconsultant-relaunch/](https://remoteseoconsultant.com/istiquritconsultant-relaunch/).

## How to Start Reading istiquritconsultant.com

1. Go to [https://istiquritconsultant.com/](https://istiquritconsultant.com/) and check whether it's rendering in dark mode (#0B1215) by default — that's the intended experience.
2. Pick a category from the six on the homepage. If you're debugging a tooling issue right now, start with Workflow Optimization, since that's where the first post lives.
3. Read "OpenCode Not Working: Why Both CLI & Desktop Died" first — it's the most representative example of the site's format: real error, real root cause, real fix.
4. Try the mini-game on whichever category page you land on; each one is themed to that category's content.
5. Subscribe to the newsletter if you want future posts delivered one at a time, with a one-click unsubscribe available at any point.

## FAQs

**What is the istiquritconsultant.com Re-Launch?**
It's the relaunch of a formerly commercial domain into a personal, non-commercial tech diary, live since August 24, 2026, covering AI, Windows, Linux, Self-Hosting, Workflow Optimization, and the author's tech journey.

**Is istiquritconsultant.com trying to sell anything?**
No. The homepage states directly that there's no pitch inside the posts; commercial work stays on remoteseoconsultant.com and is linked only once, from the About page.

**What tech stack runs the site?**
Hand-coded PHP with version-controlled Markdown content, currently on build 2.1.1, served through Cloudflare and LiteSpeed cache, with IndexNow for indexing and self-hosted fonts.

**What was the first post about?**
"OpenCode Not Working: Why Both CLI & Desktop Died," a real bug report covering a crash in both the CLI and desktop app after adding five custom subagents, down to the one-field root cause.

**How many mini-games does the site have?**
Nine, built with three.js — six matched to content categories, plus Breakout on the homepage, Journey Snake on About, and Catch the Signal on Contact.

**Who writes istiquritconsultant.com?**
Md. Istiqur Rahman, who also runs Remote SEO Consultant; the two are kept as separate brands with separate visual identities.

## About the Author

**Md. Istiqur Rahman** | Postgraduate A-grade Pharmacist; Remote SEO Consultant for SaaS and eCommerce, Website Designer and Developer specialized in WordPress and Webflow, in practice for 17 years.

I am a Remote SEO Consultant for SaaS and eCommerce, specialized in leading your team to implement a precise, data-driven SEO system. I stop the wasted budget and finally deliver the targeted traffic and predictable growth your business needs to thrive.

- 150K+ Monthly Users for a Silicon Valley SaaS Startup
- 14K+ Monthly Enterprise Users for a Californian AI Startup
- $284K+/Mo for a USA Cosmetics eCommerce Brand
- Website Designer and Developer specialized in WordPress and Webflow

Commercial inquiries: [https://remoteseoconsultant.com/](https://remoteseoconsultant.com/). Relaunch announcement and backstory: [https://remoteseoconsultant.com/istiquritconsultant-relaunch/](https://remoteseoconsultant.com/istiquritconsultant-relaunch/). Video walkthrough: [https://www.youtube.com/watch?v=_bmAXUClHVk](https://www.youtube.com/watch?v=_bmAXUClHVk).
