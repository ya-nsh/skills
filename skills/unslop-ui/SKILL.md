---
name: unslop-ui
description: Strip the AI-generated look out of a UI in one pass, so it looks like it was designed for this product instead of averaged from every other one.
disable-model-invocation: true
argument-hint: "[optional page, component or concern to focus on]"
---

Start a thorough redesign of this UI and complete it to the end.

Treat this as a goal.

**Why do this at all?**

- **People notice:** users have seen the purple gradient a thousand times. They read it as "nobody cared", and trust the product less.
- **It's forgettable:** a UI built from defaults looks like every other product, so nobody remembers yours.
- **It's harder to use:** when everything is decorated, nothing stands out, so people can't tell what to do first.
- **It's harder to change:** a hundred one-off values means every new screen invents its own look.

**1. Ask**

Besides unslopping the UI, there are two other things you may do:

| Addition | What it does |
| --- | --- |
| **Copy** | Rewrite copy that could describe any product, using only facts from the codebase and from the user. |
| **Fake proof** | Remove made-up stats, testimonials, ratings and customer logos. |

List these (with their exact descriptions) for the user and ask which ones to do. Then do only those.

Also ask who the product is for and what it does, in one sentence, if the codebase doesn't make that obvious. Everything else follows from the answer.

**2. List every problem**

Don't change anything yet.

Screenshot every page at 1440px and 375px wide. Then go through the UI asking one thing: **was this chosen for this product, or is it what every product gets?** Write down every place the answer is "every product", as in the [decision log example](#decision-log-example). There are only three ways to get it wrong.

**Defaults:** choices nobody made.

- Indigo, violet or purple-to-pink gradients, on buttons, backgrounds or text.
- Gradient text in the headline.
- Glass cards: translucent white, a blur, a 1px white border.
- Blurred glowing orbs or blobs behind the hero.
- Emoji used as icons, or an icon in a tinted circle above every card.
- The same template: centered hero, logo strip, three or six feature cards, three testimonials, three pricing tiers, gradient CTA band.
- One font at one weight, with sizes picked per element instead of from a scale.
- `rounded-2xl` and `shadow-lg` on everything.

**Noise:** decoration that doesn't help anyone do anything.

- Animation that doesn't say anything: fade-up on scroll, cards that lift on hover but aren't clickable, pulsing badges.
- A pill above the headline ("🚀 Now in beta").
- Sparkles, glows, gradient borders, dividers between things that are already apart.
- More than one accent color, so none of them means anything.
- An icon next to every label.

**Generic copy:** words that would fit any product.

- "Supercharge", "unlock the power of", "seamless", "effortless", "built for the modern…", "next-level", "game-changing".
- Feature titles that are an adjective and a noun: "Lightning-Fast Performance", "Enterprise-Grade Security".
- Headlines that say how the user will feel instead of what the product does.
- Numbers and quotes that nobody can back up: "10K+ teams", "99.9% uptime", "Sarah J., CEO at TechCorp".

Also write down every **one-off**: a value used in one place instead of coming from the system.

- A hard-coded color
- A font size, spacing, radius or shadow used once
- A button or card styled differently from its siblings
- An `!important`
- A breakpoint fix for one element

Each one is a decision the design system never made, so use them to work out what the system needs to be.

**3. Redesign from first principles**

Work out the design as if you'd started from the product instead of from a template. Answer these first, and write the answers at the top of the decision log:

- **Who uses it, and where?** A line cook checking shifts on a cracked phone is not a CFO on a 27" monitor.
- **What should the eye land on first?** Usually the product itself, not a slogan about it.
- **What does this product's world look like?** Take the palette, type and texture from the domain (kitchens, trading floors, field notebooks, airport signage), not from other SaaS sites.

Then define the system, as small as it can be:

- One or two typefaces, and a type scale.
- Neutrals plus one accent, and a rule for when the accent is allowed.
- A spacing scale, a radius and at most one elevation.
- A rule for motion: things move only to show a change of state.

Don't swap one default for another. A cream background with a serif headline, or black and white with one neon accent, are defaults too. Don't copy another product's look either.

Write each fix above the problems it solves, as in the [decision log example](#decision-log-example). Look for the one fix behind several problems.

**4. Fix everything on the list**

Put the system into tokens (CSS variables, the Tailwind theme, or whatever the codebase already uses), then move every component onto them. Delete before you add: most of the fix is removing things.

Keep every behavior: links, forms, states, routes, accessibility labels. Keep or improve contrast. This is a redesign, not a rewrite.

If the user chose Copy:

- Replace every claim with a specific one: what the product does, for whom, and how. Get the facts from the code (what features exist, what integrations are wired up, what the pricing page charges) and from the user.
- Use the words the users use. Restaurants say "covers" and "86'd", not "customers" and "unavailable".
- Never invent a feature, number or quote. If a fact is missing, ask.

If the user chose Fake proof:

- Remove stats, testimonials, ratings and logos that the code or the user can't back up.
- Replace them with the product itself: a real screenshot, a live example, a real number, or nothing.

**5. Check, and repeat until done**

Have subagents screenshot every page at both widths and look for defaults, noise, generic copy and one-offs. **Do not stop until there is nothing worth fixing left.**

You're done when:

- **As few one-offs are left as possible.** A search for raw colors, pixel sizes and shadows outside the tokens is the best measure of how close you are.
- Cover the logo, and you can still tell which product it is.
- Each screen has one thing the eye lands on first.
- Nothing moves unless something changed.
- Subagents have no issues left that are worth fixing.
- Every page works as before, at 375px and 1440px. Test this at the end.

**Tips**

- **Screenshot before you touch anything:** you'll want the before and after, and so will the user.
- **Count the system:** script a count of distinct colors, font sizes, radii and shadows in use, from computed styles. Rerun it as you go. Every number should drop.
- **Start with type:** it carries most of a UI's identity, and most slop is one font at random sizes.
- **Show the product:** the strongest hero is usually the real UI, not an illustration of it.
- **Delete first:** remove the noise before you restyle what's left. There's less to restyle.
- **Keep a decision log:** compaction is less of a problem that way.

<a id="decision-log-example"></a>**Decision log example**

The list of problems:

```md
- `app/page.tsx:12` hero has a violet-to-fuchsia gradient background with two blurred orbs.
- `app/page.tsx:18` headline "Supercharge your observability" with gradient text on "Supercharge".
- `app/page.tsx:24` pill "✨ Now with AI insights" above the headline.
- `components/FeatureCard.tsx:8` six glass cards, each with an emoji in a gradient circle.
- `components/FeatureCard.tsx:15` cards lift on hover but aren't links.
- `components/Stats.tsx:5` "10K+ teams", "99.99% uptime": no source anywhere in the repo.
- `components/Testimonials.tsx` three quotes from "Alex R., CTO".
- `app/dashboard/Chart.tsx:41` hard-coded `#8b5cf6`, not in the theme.
- `app/dashboard/Table.tsx:19` font sizes 13px, 13.5px and 14px for the same kind of cell text.
- 34 distinct colors, 17 font sizes, 9 radii, 12 shadows in use.
```

Then with the fixes:

```md
Who: on-call engineers, at 3am, usually on a laptop. First thing: is anything on fire.
World: terminals and status boards. Dense, monospace numbers, color only for state.

- Use a type system of one grotesk and one mono, with a 6-step scale. Numbers are always mono.
  - `app/dashboard/Table.tsx:19` font sizes 13px, 13.5px and 14px for the same kind of cell text.
  - 17 font sizes in use.
- Make the palette neutrals plus state colors (ok, degraded, down), with no brand gradient. Color only ever means state.
  - `app/page.tsx:12` hero has a violet-to-fuchsia gradient background with two blurred orbs.
  - `app/page.tsx:18` headline with gradient text.
  - `app/dashboard/Chart.tsx:41` hard-coded `#8b5cf6`, not in the theme.
  - 34 distinct colors in use.
- Replace the hero with a live status board of a demo service, so the first thing on the page is the product.
  - `app/page.tsx:18` headline "Supercharge your observability".
  - `app/page.tsx:24` pill "✨ Now with AI insights".
  - `components/Stats.tsx:5` "10K+ teams", "99.99% uptime".
  - `components/Testimonials.tsx` three quotes from "Alex R., CTO".
- Turn the six feature cards into a plain list of what it does, each with a one-line example.
  - `components/FeatureCard.tsx:8` six glass cards, each with an emoji in a gradient circle.
  - `components/FeatureCard.tsx:15` cards lift on hover but aren't links.
```
