# PMCS-1151-W1 · Week 1 Orientation

The **public** week-one page for **PMCS (EMI)** — *Introduction to Project Management and Career Strategy as a Product Manager in the AI Era* — semester 1151, Prof. Shihmin Lo, National Chi Nan University, General Education.

**Live:** https://lolopodcast.github.io/PMCS-1151-W1/

One self-contained HTML file. React, Tailwind and DOMPurify load from pinned CDN versions; there is no build step.

## What this page is for

It has two jobs, and they pull in the same direction: tell a student what the course actually costs, and give whoever stays everything they need to hand in on the first day. The course is capped at 36 and general-education places are balloted, so a student who discovers in week five that they cannot keep up leaves a seat nobody can fill. The conditions therefore go at the top of the page, in the statistics band, not buried at the end.

| Section | Contents |
|---|---|
| 0 · What this course does | The endpoint (a live morning-brief agent), the four conditions as statistics, the countdown, and a contents list |
| 1 · Three shifts | The umbrella claim plus three tensions — who is buying, which work changes first, will the job still look like that — with an SVG map |
| 2 · Three questions, by hand | Part A, and why the first assignment bans AI |
| 3 · One-minute intro | The 4Q, the not-graded/not-public promise, 23:59 that day, and what happens if it is missed |
| 4 · Three checks | Date, primary source, dissent — the filter used every week from here |
| 5 · How the course runs | The four conditions in full, the weekly rhythm, adding the class, and what W2 unlocks |
| 6 · Interactive Lab | Self-check, deadline countdown, one-minute timer with 4Q prompts, three-checks practice |
| 7 · Resources | Daily Brief, the self-introduction practice page, the platform comparison, the workshop hub |
| 8 · Your progress | Local-only progress, with no identity fields at all |

## Notes for maintenance

- **This page collects nothing.** It is public and will be indexed, so the usual Analytics module — group, department, student number, name, CSV export — is deliberately absent. There is not a single `<input>` on the page. What the progress section keeps (time, clicks, quiz accuracy, cards read) lives in `localStorage` under `PMCS_W1_progress`, carries no identifier, and is stated as such on the page itself. Do not add an identity form here; if per-student data is ever needed, it belongs behind the passphrase in the hub.
- **Nothing links to the gated material.** No hub URL, no worksheet index, no passphrase. The bridge is a sentence: the passphrase is handed out in the W2 class. A test asserts that none of those strings appear in the built file.
- **The calendar is derived from four constants.** `W1_DATE`, `W2_DATE`, `DEADLINE` and `CLASS_TIME` sit at the top of the script. The countdown, the deadline copy and the dated language all read from them. Changing the term start means editing those, nothing else.
- **Read-aloud chunks long sentences, not just paragraphs.** Splitting only on sentence boundaries lets a single long English sentence through at 387 characters, and Chrome silently stops part-way through an over-long utterance. `hardSplit` breaks any segment over the limit at the nearest comma, semicolon, dash or space (Chinese: at 、，；：), falling back to a hard cut. Limits are 140 characters for Chinese and 190 for English. The same three Chrome defences as the hub are in place: a strong reference to the live utterance, an eight-second keep-alive, and a watchdog — and every teardown calls `resume()` before `cancel()`, because cancelling while paused wedges the engine.
- **The root uses `overflow-x: clip`, never `hidden`.** `hidden` turns the element into a scroll container and silently breaks the sidebar's `position: sticky`. A test asserts the sidebar still sticks after scrolling 1200px.
- **Contrast is checked, not eyeballed.** Both themes measure zero WCAG AA failures across every section, with translucent backgrounds composited properly before the ratio is taken. Two things to know if you re-check it: the local `verify/tw.css` must be regenerated whenever a new utility class is introduced, or the measurement silently reads the wrong colour; and `text-slate-500` on the light background lands at 4.33, just under the 4.5 threshold, which is why body-secondary text is `text-slate-600 dark:text-slate-400` throughout.
- **The three shifts name no company, no product and no number.** That is the point of section 4 — specifics expire, so the page teaches the checks instead. Resist the temptation to add a topical example; it dates the page and undercuts the argument the page is making.
- **Answers are obfuscated,** XOR plus Base64 under `_SALT`, so the quiz keys are not sitting in the source as plain integers. Options are shuffled per question, and questions are drawn two at a time from the remaining pool.
- The page enforces a **domain lock** (`lolopodcast.github.io`, `localhost`, `127.0.0.1`) and busts out of iframes. There is deliberately **no passphrase** — this one is meant to be open.
- **Default language is English and the default theme is dark,** matching the other course units. This is an EMI course and the page is itself a filter.

© Prof. Shihmin Lo. For educational use in this course.
