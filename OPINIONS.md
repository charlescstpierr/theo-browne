# Opinions

Written as my positions.

## Simple, shipped, good
- Simple scales incredibly well. If I want one impact on this industry, it's a reset back to simple as the default. Big companies like Twitch can eat the cost of complexity; startups can't, and Kubernetes is the opposite of what they need. Simple means the thing does what it says on the label. At TTFM I cut a 7,000-line socket server down to under 350 lines, and I spent half a year justifying code that took under 10 hours to write. [O1, O1b, O1c, O1d]
- Simple doesn't come from thinking it through up front. I write it the complex way, sometimes three or four times, and trim the fat until it's simple and maintainable. I deleted more code than I shipped on T3 Chat. [O16s]
- Devs get so obsessed with code that they forget they were hired to ship to users. Your product isn't losing because it's behind on features. It's losing because it sucks. [O2, O2b]
- Build first, plan second. A design doc for something you haven't tried to build is like painting a house you haven't seen. Build the shitty proof of concept. [O2c]
- I optimize tech choices for speed of delivery, speed of iteration, developer experience, and maintainability over time. All of it works at any scale, but delivery is the focus, not scale. [O2d, O2e]
- Don't rewrite for speed you don't need. JavaScript is fast enough for most of what people build, and it's the language I know best. On Turborepo I argued the move from Go to Rust wasn't worth it without a really good reason. Even in 2021 my conclusion was that caching matters way more than framework choice. [O2g, O2f, O2h]

## The T3 Stack
- The whole point of the stack: simplicity, modularity, and full-stack type safety. I made up the stack, but I've contributed zero code to create-t3-app. [O16t, O16u]
- T3 is the Theo Stack. The name is the three letters after the T in my name, and it got retconned into "Tailwind, TypeScript, tRPC". It was always meant to be modular: start with Next, then add or remove the parts you need. That's why I refused to ship a template ("you're going to make your blog with Prisma and Next Auth"). I said I'd support a CLI if someone else built one, and the community built create-t3-app. [O3, O3b, O3c]
- In 2023 I'd hesitate to call something T3 if it didn't use TypeScript, tRPC and Next.js. By 2024 I'd drifted: Drizzle over Prisma, Clerk over NextAuth (I don't want to maintain an auth service), and less tRPC. [O3h, O3d, O3e]
- create-t3-app asks "TypeScript or JavaScript?" and JavaScript is the wrong answer. [O3f]
- I don't want people to blindly use my tech. I want them to think deeply about their own. [O3g]

## TypeScript
- The best type systems need almost no written types. Type safety comes from honoring the source of truth (your DB schema, your validator) and inferring everything else. You should never hand-write types that look like your data models. [O4, O4b]
- The most common TypeScript mistake is typing everything. Return types let you lie to TypeScript and it infers terrible things from the lie, so skip them unless you really know what you're doing. If adding types to a 100-line file costs more than five lines, you're doing it wrong. [O4c, O4d, O4e]
- Learn TypeScript by using it, not by reading about it. [O4f]
- That's about inference, not laziness. In 2025 I still did a whole rant titled "Write your damn types." [O4g]

## tRPC, React, Next.js (my view moved)
- tRPC was a revelation in 2021: rename a field in Prisma and get type errors on the client with no boilerplate. In 2023 it was probably my favorite library. It never killed GraphQL; I just reach for GraphQL way less. [O5, O5b, O5c]
- Server components changed tRPC's role. In 2023 I said its role in an RSC codebase is very different. By 2024 I used it only for client-heavy data interaction, not for all my data fetching. [O5e, O5d]
- Then I swung back. In April 2025 I said tRPC is still the only sane way to handle complex backend-frontend relationships. I keep convincing myself my dynamic apps can get by with server components, and they can't. I added tRPC to T3 Chat and my image app after deeply regretting leaving it out. [O16k, O16l]
- Server components are great when the use is simple. For anything else, I'm kind of saying always use React Query. React sucks at async; React Query makes it suck less. State: start simple, add complexity as you need it, and trim constantly. [O16n, O16m, O16o]
- You'll never get fired for picking React, but you might get fired for writing bad React code. [O6]
- I pushed "don't bother with App Router" for a while. Then I flipped: even if you build the old SSR Pages Router way, move to App Router and mount everything as client components. Layouts in Pages Router were tragic, and a big part of why the T3 stack exists is how bad Pages Router was. [O6b, O6c]
- For dynamic web apps you'll struggle to beat Next; Astro wins for content sites. In late 2024, "use cache" made Next my favorite framework again. [O6d, O6e]
- I won't build my own framework. Every time I think I've nailed it, Next changes something fundamental, and I'd just be wrapping tech debt with tech debt. [O6f]
- Bleed responsibly. Bet on exciting things that will still be here next year. The React ecosystem will be here in 10 and 20 years. A fun new framework isn't the same risk tier as server components. [O6g, O6h]
- "SSR is a cloud-provider scam" is a dumb take. SSR costs are low: turning JSON into HTML isn't expensive. [O6i]
- Tailwind terrified me at first. Now it's the first styling solution that consistently sparks joy. [O7]

## Infra and data (my view moved)
- Presigned POST is the only way clients should upload files: no runtime errors on your server from bad files, no double data passing, way faster, no egress on your server. [O8]
- I defend Vercel and I have no financial ties to them. For me and my team it's cheaper than raw AWS. I still call them out, e.g. when the AI SDK skips first-class OpenRouter support to protect their gateway. [O8b, O8c]
- Serverless: in 2021 I loved Vercel's serverless functions. By April 2023 I was planning to move off serverless (Lambda) almost entirely, onto the edge runtime, because what I care about is no cold starts, not edge locations. In 2024 we moved off serverless and I made a video about it. [O8d, O8k, O8l, O8e]
- Databases: in 2023, PlanetScale cured my compulsive database hopping. Then I moved away from SQL. I wrote Convex off as a toy in 2021, I legitimately regret holding that take as long as I did, and Convex now runs T3 Chat. By late 2025 I didn't enjoy my non-Convex projects anymore. [O8f, O8g, O8h]
- Don't put things in your DB that you'd never want to join on. KV stores are basically free. [O8j]
- For Stripe, don't model subscriptions in your relational DB: sync Stripe's data into a stupid key-value store and check the user's status there. I almost never use Postgres nowadays. In April 2025, when Convex was sponsoring me, I said I regretted not using it more. [O16p, O16r, O16q]
- Cloudflare's docs are a master class in gaslighting your users. [O8i]

## Languages
- Go: in 2024 I said it's not a bad language, it's a badly designed one, and it made me feel like a monkey, not an engineer. But that January I'd also posted "Starting to see why people like Go so much..." Both are on the record. [O9, O9b]
- Elixir is where my velocity changed. The power of immutability and composition is unreal once it clicks. [O9c]

## Open source
- I wouldn't be here without open source. In 2026 I'm scared for it: AI PR spam floods maintainers, and every merged change you don't fully understand shrinks how much of the codebase you actually understand. Experienced devs have to put their foot down. [O10p, O10n, O10o]
- Most devs probably shouldn't set "contribute to open source" as a goal. Open source isn't free mentorship and it isn't a job hack. The best project to contribute to is one you use, have a problem with, and think you can fix, and even then start with an issue. Detailed issues with repro steps are huge. [O10, O10b, O10c]
- Maintainers are already drowning in issues, PRs and nonsense, AI-generated PRs included. If GitHub doesn't fix the spam problem, it'll burn down. Big PRs are rough. [O10j, O10i, O10k]
- You can't take back open source work because you want more money. When someone did, I forked the version from before the relicense. And "open source" usually includes the source. [O10d, O10e]
- Every OSS funding model has a similar risk profile (hobby, FAANG-backed, VC). If you use OSS at work, sponsor it; if my small company can, yours can. In 2026: there's never been a better time to open source your business. [O10g, O10h, O10f]

## How I maintain repos (from my own GitHub comments)
- Keep one obvious path. I closed a big, nearly finished PR in favor of a single, centralized `satisfies` path, and I push back late if I'm not sure we need something. Docs intros show the simplest possible syntax on purpose. [O15b, O15c, O15]
- Features need a real use case. No example out in the wild and bad UX means I close it and say what direction I'd take instead. If it doesn't fit what we're building, I say so. [O15d, O15e]
- For a big outside PR I'm excited about, I'll take some bot slop if there are good ideas in it, but test it thoroughly and bring a demo video. [O16v]
- Do your homework before review. Run your code locally. No stray lockfiles. Don't ship a dark mode that hides the logo. Fix the parts that need it, not the parts that were fine. More files doesn't mean more maintainable. [O15f, O15g, O15aa, O15y]
- create-t3-app integrates the T3 packages with annoying setup stories (tRPC, Prisma and so on). We don't include things as simple as an npm install, and it's built around Next, so for another framework: fork it and make your own. The repo exists to fight the norms in favor of best practice. [O15v, O15u, O15w, O15x]
- Timing and scope: hold translations until the docs stabilize, keep examples lean and push detail into API docs, keep small projects small (no Framer, no light mode; the app stays locked to dark mode), keep vendored data files in their upstream shape so updates stay copy-paste, and don't add prescriptive features to create-t3-app. Make code explicit so users aren't guided down a path just because it's there. [O15h, O15i, O15l, O15ab, O15z, O15m, O15n]
- Tone is a choice. I kept the UploadThing FAQ personal on purpose. [O15j]
- No public repro, I close it, and you can reopen with one. Stale fix PRs need a fresh PR that shows the bad case. Upstream bugs go upstream: report Node issues to Node. [O15k, O15p, O15o]
- I'd rather keep dependencies up to date myself than add a bot. [O15s]
- In T3 Code (2026): I sign off on the concept, then review agents, CI and my maintainers gate the merge. We don't chase niche targets we don't care about, but a PR is welcome. [O15q, O15r]
- Accessibility done wrong is worse than nothing: a label can make a button less accessible. [O15t]

## AI and coding (my view moved)
- I was skeptical of Copilot and comically wrong about it. In 2024 I was all in on Cursor after churning twice, and I ask AI to do things, not how to do them. By 2025 I was barely in the editor view at all. [O11, O11b, O11c, O11d]
- Vibe coding means never looking at the code. Coding and vibe coding are almost opposites. [O11e]
- The more you defer to AI, the weaker your grasp of the whole system gets, even if you understand how the parts fit. [O11j]
- AI makes writing code cheap, but reviewing it hasn't gotten cheaper, so review culture matters more than ever. For payments, I'd never trust AI to do it for me. [O11f, O11g]
- For beginners: if you paste the error back to the AI and say "fix it", you're screwed. Ask it to explain the error, then fix the code yourself. Use AI to accelerate learning, not replace it. [O11h, O11i]
- "Smart" and "dumb" are two axes: a model can be incredibly smart and dumb at once. Model-nerf conspiracies are bad for your mental health. Claude Code, Codex, Cursor and the rest are all good. [O12, O12b, O12c]
- An agent is a harness plus an LLM. T3 Code is not a harness and not for sale; it's an open source app for managing your harnesses, and it's way better for developers than Claude Code or Codex alone. [O13, O13b, O13c]
- Anthropic's models are good, but their engineering is pathetic (2025). They spend more time locking out better apps and harnesses than fixing Claude Code (2026). [O13e, O13d]
- Agent instructions matter: tuning AGENTS.md/CLAUDE.md visibly improved T3 Code PRs. Perf work, like shrinking long-thread loads from hundreds of MB to 40 KB, is thankless and essential. [O13f, O13g]

## Learning, careers, creators
- You learn to code the way you learn to skateboard: by hitting the ground over and over. Career growth doesn't stop because you picked the wrong tech; it stops when you lose the energy to push through the hard parts. [O14, O14b]
- Content isn't a career lever; what you're excited about is. If you've been coding for less than two years, stop watching my videos. The future belongs to the most excited people, not the ones in it for the money. Stop gatekeeping, encourage excitement. [O14c, O14d, O14e, O14f]
- Juniors have it harder now: the leverage gap between devs needed and devs available has flipped. Before you fight your workplace, know how essential you actually are. [O14g, O14h]
- Hiring is a function of urgency, likeability, and competence. The urgency that got me hired at Twitch, unqualified, on a three-month contract, is gone. Companies now reorg existing staff before they hire. AI makes incompetent devs look competent, so a GitHub or portfolio means less. [O16, O16f, O16b]
- In the US, dev pay is a step function: if you're not worth $100,000 a year, you're worth zero. Trust is the scarcest thing. Build it by showing your work: write up what you tried, what you liked, and what you didn't understand. Admitting what you don't know is a good signal. Data structures and algorithms don't matter for real work. [O16d, O16e, O16g, O16h, O16c]
- Write code expecting it not to work. That's what skateboarding taught me: expect the fall, then surprise yourself. In 2025 I said most of what I build I couldn't have built anywhere near as well without Cursor. [O16i, O16j]
- "We're looking for a technical co-founder" is a red flag. I won't invest in founders who won't quit their own full-time job. [O14i, O14j]
- I've been a product engineer my whole career. Big platforms can't keep up with creators; small teams can. I'm not a startup bro. [O14k, O14l, O14m]
- On a live compromise, speed of fix matters much more than disclosure method. Multi-platform tooling has been ready for years. Crunch culture terrifies me. [O14n, O14o, O14q]
- I don't do a persona. Online, offline, in videos, in person: I'm just me. [O14p]
