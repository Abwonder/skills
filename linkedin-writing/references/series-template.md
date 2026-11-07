# Series template

Built from the ten day pentest run published roughly three months ago. Ten posts, one per day, each between 2,600 and 2,990 characters. Launch post on the Sunday, then Day 1 through Day 10.

## What the run actually did

| Part | Title | Length |
|---|---|---|
| Launch | 8 CRITICAL vulnerabilities. Complete Privilege Escalation. Total PII Exposure. | short |
| Day 1 | Reconnaissance & The Exposed Blueprint | 2,961 |
| Day 2 | Mapping Authentication & Initial Initial Access | 2,991 |
| Day 3 | The BaaS Trap, Bypassing the Premium Paywall | 2,911 |
| Day 4 | The Privilege Escalation Chain | 2,604 |
| Day 5 | The JWT Trust Fall, Forging Admin Claims | 2,906 |
| Day 6 | The Payoff, Dumping the Entire User Database | 2,892 |
| Day 7 | Follow the Money, Leaking the Transaction History | 2,727 |
| Day 8 | The Silent Client-Side Hijack | 2,798 |
| Day 9 | The "Secure" Frontend Illusion, Broken Session Management | 2,679 |
| Day 10 | Building is Easy. Defending is an Art. The Remote MSSP Vision | 2,890 |

Engagement on the launch: 33 reactions, 3 comments, 1,197 impressions.

## The skeleton, as used

1. `DAY n: Title`, with a second line after a colon.
2. Hook: a claim and its consequence, one or two lines, one emoji.
3. Bridge: what most people think, then what actually happened.
4. Sections inside box drawing dividers, up to five per post.
5. Arrow bullets for the exploit chain.
6. A numbered "The Fix" list with digit emojis.
7. `Follow so you don't miss Day n.`
8. Six hashtags.
9. Cross reference to the previous day near the top.
10. Day 10: recap of all ten, then a close.

## What to keep

- **One post per day, same time.** The schedule was the product.
- **The day number in the first line.** It created a reason to come back.
- **The cross reference.** "Read Day 1 to understand this" kept people in sequence.
- **The Fix section.** This is what separated it from every other pentest story on the platform. Concrete remediation, numbered.
- **The recap on the last day.** One line per part, with the arrow.
- **The overflow comment on Day 5.** When a post runs past the ceiling, move the tail into comment one and say so.
- **The artefact habit.** Paths, wordlist counts, line counts, status codes.

## What to rebuild

- **The dividers.** `─── SECTION ───` is a visual tic and it eats characters. Use a plain capitalised line, or no divider at all.
- **The subtitle after the colon.** The title should stand alone. Two clauses in a title means neither one is sharp.
- **The emoji in every hook.** One per post maximum, and only where it replaces a word.
- **The negative parallelism hook.** This was the default and it is now the strongest AI tell. Open on the object instead.
- **The self referential close.** "Follow so you don't miss Day 2" is fine on Day 1. By Day 6 it reads as a subscription pitch. Use it on the first and last post only.
- **Six hashtags.** Three to five.

## Rebuilt Day 1, same content, new surface

> DAY 1: The repo was public
>
> The .git folder was reachable from the internet. That is where I started.
>
> A React frontend, a Node backend, a Supabase database, Cloudflare in front. The kind of stack that looks finished from the outside.
>
> I ran Gobuster first, because that is what everyone runs first. A 141,000-word list, three hours, and it returned the usual: admin panels that 403, asset directories, a robots.txt nobody meant to ship.
>
> Then I requested /.git/HEAD.
>
> 200, and a commit hash.
>
> From there it is mechanical. Fetch /.git/config, get the remote. Walk the object store, rebuild the tree, check out the working copy. Twenty minutes later I had the source, the .env, and the service key that the frontend never needed and the deploy pipeline never rotated.
>
> The scanner reported nothing here. Scanners do not walk git objects.
>
> The Fix:
>
> 1. Block `/.git/` at the edge. One Cloudflare rule, matches URI path, contains `.git`, action block.
> 2. Strip `.git` in the build step. `rm -rf .git` before the artefact is packaged. If the folder is in the image, you shipped it.
> 3. Rotate every secret that was ever in a commit. Not the ones you think are exposed. All of them. The history is the exposure.
>
> Day 2 is the part that mattered more: the anon key was doing far more than it was designed to do.
>
> #PenetrationTesting #DevSecOps #Supabase #AppSec

That is roughly 1,600 characters. Shorter than the original because the scaffolding is gone, and it still carries the same four beats: the object, the miss by standard tooling, the mechanism, the fix.

## Series plan template

Before writing part one, fill this in. Ten rows, no more.

| Day | Claim | Artefact | Fix |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

Rules for the plan:

- Every day needs a distinct artefact. If two days share one, merge them.
- The claim is a sentence, not a topic. "The anon key was doing more than it was designed to" is a claim. "Authentication" is a topic.
- Order by the reader's discovery path, not by severity. Severity order makes part one the best post and the rest denouement.
- Decide the count before publishing. Ten means ten.

## Launch post rules

- State the outcome first, in numbers.
- Name the stack. Readers self select on stack.
- Give one line per part of the chain, no more.
- Promise the exact number of parts.
- Ask a question the audience can answer from their own experience, not about your post.
