# PMCS-1151-W1 · Week 1 Orientation

The **public** week-one page for **PMCS (EMI)** — *Introduction to Project Management and Career Strategy as a Product Manager in the AI Era* — semester 1151, Prof. Shihmin Lo, National Chi Nan University, General Education.

**Live:** https://lolopodcast.github.io/PMCS-1151-W1/

One self-contained HTML file. React, Tailwind and DOMPurify load from pinned CDN versions; there is no build step.

## What this page is for

It has two jobs, and they pull in the same direction: tell a student what the course actually costs, and give whoever stays everything they need to hand in on the first day. The course is capped at 36 and general-education places are balloted, so a student who discovers in week five that they cannot keep up leaves a seat nobody can fill. The conditions therefore go at the top of the page, in the statistics band, not buried at the end.

| Section | Contents |
|---|---|
| 0 · What this course does | The endpoint (a live morning-brief agent), the four conditions as statistics, the countdown, and a contents list |
| 1 · See the World | The macro level: family, university, society-and-industry, ringed by government policy and global PESTEL |
| 2 · Understand Industry | Four categories, the chain industry → company → department → position → JD, and K/S/A |
| 3 · Shape Yourself | Coursework, everything outside class, people — feeding a career foundation, driven by PBL and SDL |
| 4 · Become a Product Manager | Where the three levels meet: five competencies and the courses that map to them |
| 5 · Three shifts | The 2026 update layer: one premise, three tensions, each landing on one of the earlier levels |
| 6 · Due on day one | Part A (three handwritten questions) and Part B (the one-minute authentic video), both at 23:59 |
| 7 · Three checks | Date, primary source, dissent — the filter used every week from here |
| 8 · How the course runs | The four conditions in full, the weekly rhythm, adding the class, and what W2 unlocks |
| 9 · Interactive Lab | Self-check, deadline countdown, one-minute timer with 4Q prompts, three-checks practice |
| 10 · Resources | The two orientation videos, Daily Brief, the self-introduction practice page, and more |
| 11 · Your progress | Local-only progress, with no identity fields at all |

## Notes for maintenance

- **Progress state is migrated on load, not trusted.** `TOTAL` changed once (nine sections became twelve), and the arrays already sitting in returning students' `localStorage` were still nine long — so `time[9] += 1` produced `undefined + 1`, and the summary tiles showed `NaN`. `migrate()` now rebuilds every array to `TOTAL` on load, coercing anything non-finite to 0 and anything non-boolean to false. Keep it whenever the section count changes again; the stale copy in a returning browser is the case that breaks.
- **The course carries its full name in both languages on every view.** `course_zh`, `course_en`, `course_code`, `dept` and `teacher` are identical in both dictionaries, so the Chinese title appears on the English page and vice versa — a general-education elective is shopped by students from every department, and the English-only title alone does not tell a first-year Chinese-literature student what the course is.
- **This page collects nothing.** It is public and will be indexed, so the usual Analytics module — group, department, student number, name, CSV export — is deliberately absent. There is not a single `<input>` on the page. What the progress section keeps (time, clicks, quiz accuracy, cards read) lives in `localStorage` under `PMCS_W1_progress`, carries no identifier, and is stated as such on the page itself. Do not add an identity form here; if per-student data is ever needed, it belongs behind the passphrase in the hub.
- **Nothing links to the gated material.** No hub URL, no worksheet index, no passphrase. The bridge is a sentence: the passphrase is handed out in the W2 class. A test asserts that none of those strings appear in the built file.
- **The calendar is derived from four constants.** `W1_DATE`, `W2_DATE`, `DEADLINE` and `CLASS_TIME` sit at the top of the script. The countdown, the deadline copy and the dated language all read from them. Changing the term start means editing those, nothing else.
- **Read-aloud chunks long sentences, not just paragraphs.** Splitting only on sentence boundaries lets a single long English sentence through at 387 characters, and Chrome silently stops part-way through an over-long utterance. `hardSplit` breaks any segment over the limit at the nearest comma, semicolon, dash or space (Chinese: at 、，；：), falling back to a hard cut. Limits are 140 characters for Chinese and 190 for English. The same three Chrome defences as the hub are in place: a strong reference to the live utterance, an eight-second keep-alive, and a watchdog — and every teardown calls `resume()` before `cancel()`, because cancelling while paused wedges the engine.
- **Read-aloud keep-alive is desktop-only.** Desktop Chrome goes silent after about fifteen seconds unless something pause/resumes it, so a keep-alive interval runs there. On a phone that same interval is the bug: `pause()` fired from a timer is not a user gesture, iOS Safari does not reliably honour the `resume()` that follows, and read-aloud stops after a few seconds. `IS_TOUCH` (`(hover: none) and (pointer: coarse)` — capability, not user-agent sniffing) switches the keep-alive off on touch devices. The watchdog also had to change: on a phone the gap between two utterances is much longer, and the old code treated any gap as "finished" and cancelled. It now waits longer on touch devices and, if chunks remain, re-kicks `speakNext()` instead of giving up — up to eight times, then it really does stop. A `visibilitychange` handler resumes speech when the page comes back to the foreground.
- **The root uses `overflow-x: clip`, never `hidden`.** `hidden` turns the element into a scroll container and silently breaks the sidebar's `position: sticky`. A test asserts the sidebar still sticks after scrolling 1200px.
- **Contrast is checked, not eyeballed.** Both themes measure zero WCAG AA failures across every section, with translucent backgrounds composited properly before the ratio is taken. Two things to know if you re-check it: the local `verify/tw.css` must be regenerated whenever a new utility class is introduced, or the measurement silently reads the wrong colour; and `text-slate-500` on the light background lands at 4.33, just under the 4.5 threshold, which is why body-secondary text is `text-slate-600 dark:text-slate-400` throughout.
- **Sections 1 to 4 are the original course material, not a paraphrase.** They follow *[PMCS] World-Industry-Yourself_SML 20250816a* — the three levels and the PM at their intersection — including its own vocabulary (macro level, the four industry categories, the industry→JD chain, K/S/A, PBL and SDL). Section 5 is a 2026 update **layered on top**, and each of its three tensions is explicitly tied back to the level it disturbs. If the source document is revised, sections 1–4 and the four diagrams are what has to move with it.
- **Every diagram is inline SVG built from the source material,** not an image: `MacroMap`, `IndustryChain`, `PersonalMap`, `PMMap` and `TensionMap`, keyed by module in `SVG_OF`. They use the shared `SvgFrame`/`SvgBox` helpers, carry both themes through Tailwind `fill-`/`stroke-` classes, print, and scroll horizontally inside their own container on a phone. `SvgFrame` derives the credit line's y from the viewBox height, so changing a diagram's height does not push the credit onto the content.
- **Quiz options are length-balanced, and the build checks it.** Left unchecked, the correct answer ends up the longest option almost every time — the first draft of this page scored 23/23 in Chinese and 22/23 in English, meaning a student could score full marks by always picking the longest option without reading. `quizcheck.py` runs in `build_w1.sh` and fails the build if the correct answer is the unique longest in more than 25% of questions (the rate you would get by guessing) or if any question's longest option is more than 1.6× its shortest. Current: 16% and 23%, no length outliers.
- **The three shifts name no company, no product and no number.** That is the point of section 7 — specifics expire, so the page teaches the checks instead. Resist the temptation to add a topical example; it dates the page and undercuts the argument the page is making.
- **Answers are obfuscated,** XOR plus Base64 under `_SALT`, so the quiz keys are not sitting in the source as plain integers. Options are shuffled per question, and questions are drawn two at a time from the remaining pool.
- The page enforces a **domain lock** (`lolopodcast.github.io`, `localhost`, `127.0.0.1`) and busts out of iframes. There is deliberately **no passphrase** — this one is meant to be open.
- **Default language is English and the default theme is dark,** matching the other course units. This is an EMI course and the page is itself a filter.

© Prof. Shihmin Lo. For educational use in this course.
