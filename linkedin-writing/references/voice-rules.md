# Voice rules

Derived from the Wikipedia "Signs of AI writing" list, plus what actually worked in the ten day series. Apply all of it to every draft.

## 1. Punctuation

**No em dashes. No en dashes. Ever.**

Em dash: the long one. En dash: the medium one used for ranges.

The two characters to search for are U+2014 (em dash) and U+2013 (en dash). Run a find for both before publishing.

Replace as follows:

| Pattern | Rewrite |
|---|---|
| A dash setting off an aside | A colon, a comma, or a full stop |
| A dash joining two findings | A comma |
| An en dash in a date range | The word "to" |

Hyphens in compound words are fine: `read-only`, `client-side`, `zero-trust`.

This is the single most visible AI tell and it is a hard stop. If a draft has one, the draft is not done.

## 2. Banned sentence shapes

**Negative parallelism.** The single most common pattern in AI writing, and it was the default hook of the ten day series.

- `The hardest part isn't exploiting the app. It's finding the blueprint.`
- `This isn't a bug, it's a design failure.`
- `Less about tooling, more about process.`
- `Not because it is damaging, but because it is misunderstood.`

All four are banned. If the point is that the obvious thing is not the real thing, say what the real thing is and let the contrast do the work:

> Most pentesters start with Gobuster. I started with the client bundle.

**The -ing tail.** A clause bolted onto the end of a sentence to explain its significance.

- `..., highlighting the importance of input validation.`
- `..., underscoring the need for rate limiting.`
- `..., creating a perfect storm of risk.`

Delete the tail. If the significance matters, it gets its own sentence.

**Decorative triads.** Three items where the third adds nothing.

- `Patience, methodology, and knowing exactly where to look.`
- `Fast, scalable, and secure.`

Two items, or four. Three only when the third is new information, not a rhythm.

**The false range.** `From reconnaissance to exploitation.` `Everything from X to Y.` Say the two things.

## 3. Banned vocabulary

Do not use these. They are markers, not style choices.

**Analysis words:** comprehensive, robust, seamless, holistic, multifaceted, nuanced, intricate, meticulous, pivotal, crucial, paramount, vital.

**Journey words:** delve, dive into, deep dive, unpack, explore, navigate, landscape, realm, tapestry, testament, journey, embark.

**Hype words:** leverage, harness, unlock, unleash, elevate, foster, bolster, underscore, showcase, revolutionise, transform, game-changer, cutting-edge, state-of-the-art, best-in-class, world-class, next-level, paradigm shift, groundbreaking.

**Filler phrases:** it is worth noting, it is important to note, at the end of the day, in today's fast-paced world, in an ever-evolving landscape, when it comes to, the fact of the matter is, needless to say, let us dive in.

**Empty intensifiers:** truly, incredibly, remarkably, significantly (unless a number follows), extremely.

Note: `significantly` is fine when it carries data. `Significantly slower: 4.2 seconds against 180 milliseconds.` Fine.

## 4. Sentence rhythm

AI writes at a uniform middle length. Humans do not.

Pattern to aim for: three short sentences that land, then one long one that carries the mechanism.

> The key was public. It had to be, because the browser needed it. The database trusted it anyway. So I sent one request with no token, got a 200, and watched the response body fill with the purchase table for every user on the platform.

Rules:

- Vary length deliberately. A three word sentence after a thirty word sentence is a rhythm, not an error.
- One idea per paragraph.
- Never start three consecutive paragraphs the same way.
- No sentence that exists only to transition. Delete "With that in mind" and "Building on this".

## 5. Concrete over abstract

The rule that matters most for security writing.

| Weak | Strong |
|---|---|
| several sensitive endpoints | `GET /api/admin/purchases` |
| a large wordlist | a 141,000-word wordlist |
| a short script | three lines of bash |
| exposed credentials | the Supabase anon key, in `bundle.js`, line 4,112 |
| significant data exposure | 12,400 rows, including email and phone |

If you cannot name the artefact, you do not have the finding yet.

## 6. Teaching by contrast

His strongest habit. Define by splitting.

> Authentication is WHO. Authorization is WHAT.

> Your frontend said "Logged Out." Your API disagreed.

> The scanner reported zero findings. The scanner was looking at the frontend.

This works because it gives the reader a handle they can repeat. Use it once per post. Twice reads as a tic.

## 7. Openers

Open on an object or a number. Never on a thesis, a definition, or a greeting.

- Good: `A paste-sharing app advertised AES-256 encryption. I read every paste inside it in about two hours.`
- Good: `Thirty three accounts. One request. No token.`
- Bad: `In today's digital landscape, security is more important than ever.`
- Bad: `Let me tell you about an interesting finding.`

Test: cover everything except line one. Does it still make someone want line two?

## 8. Closers

Close with something answerable, or with an offer that carries no ask.

- Good: `Have you tested the handoff separately from the reasoning?`
- Good: `Happy to write both up properly with no ask attached.`
- Bad: `Thoughts?`
- Bad: `What do you think? Let me know in the comments.`
- Bad: `Follow for more!`

A question with a one word answer converts. A question with a paragraph answer does not.

## 9. Emoji

One maximum per post. Only where it replaces a word. No strings.

The ten day series used one emoji in the hook and digit emojis in the fix list. That read fine on LinkedIn in 2025. Reuse sparingly and never in a comment or DM.

Digit emojis in a numbered list are acceptable when the list is a checklist of fixes, because they survive LinkedIn's formatting strip.

## 10. Formatting

- Every line under 90 characters.
- Blank line between blocks. LinkedIn collapses single line breaks on some clients.
- No markdown. No `**bold**`, no `#` headings, no backticks. They render as literal characters.
- No bullet characters LinkedIn might strip. Use `-` or `1.` or nothing at all.
- Hashtags: three to five, at the end, specific. `#Supabase` beats `#CyberSecurity`.

## 11. The self-check

Read the draft once for each line. Twenty seconds each.

1. Any dash that is not a hyphen?
2. Any sentence shaped "not X, but Y"?
3. Any group of three that exists for rhythm?
4. Any clause starting with a verb ending in -ing, attached to the end of a sentence?
5. Any word from the banned list?
6. Any claim with no artefact under it?
7. Does line one survive alone?
8. Does the last line invite a one word answer?
