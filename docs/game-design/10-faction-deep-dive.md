# Faction Deep Dive — Discussion Questions

> Status: Draft — this is a working discussion tool, not a spec. Nothing
> here is decided; it exists to be argued through. As questions get
> resolved, fold the answers back into `05-factions.md`,
> `06-magic-and-channeling.md`, `07-units.md`, `08-economy-and-resources.md`
> and (for anything contested or non-obvious) a new ADR in
> `docs/decisions/`, the same way `01-open-questions.md` has been handled.

## How to use this doc

Each MVP faction (`05-factions.md`) gets a full pass across the same six
lenses, so no faction accidentally gets shallower thought than another.
Post-MVP factions get a shorter set of forward-looking questions — enough
that when they enter the Phase 5 build queue, the hard branching decisions
are already flagged instead of discovered cold.

Recommend working one faction to a sitting rather than skimming all of
them in one pass — these are meant to be argued through, not checklisted.

### The six lenses (applied to every MVP faction)

1. **Identity & fantasy** — what does playing this faction actually feel
   like, in one sentence a player would say?
2. **Strategic layer specifics** — what does a turn actually consist of
   for this faction? Recruitment, unique actions, win-condition flavor.
3. **Tactical layer specifics** — roster wishlist, signature units,
   doctrine (how do they use terrain, formations, tempo?).
4. **Channeling & rituals interaction** — how does this faction touch
   Shielding/Circles/Rituals (`06-magic-and-channeling.md`) and
   Capture/Prisoners, including if the answer is "it doesn't, and here's
   what they do instead"?
5. **Relationships** — who do they naturally clash or ally with on the
   map, and does the strategic AI need a personality lean to reflect it?
6. **Risk/cost, pressure-tested** — is the downside from `05-factions.md`
   actually as concrete as the upside, or does it need sharper teeth?

---

## White Tower (Aes Sedai)

> **Roster shape resolved:** the all-individual-scale-army balance
> concern that kicked off this discussion is answered by
> `docs/decisions/0008-white-tower-warder-tiers.md` — a four-tier roster
> (Tower Guard, Warder Company, Aes Sedai, optional Bonded Warder
> upgrade). See `07-units.md`'s White Tower worked example. This resolves
> most of §3 below; the remaining §3 bullets (Ajah-differentiated combat
> stats) are still open.

### 1. Identity & fantasy
- What's the one-sentence pitch? Something like "a political-magical
  superpower where your units are rare and precious, and your real
  battlefield is influence, not infantry" — does that feel right, or is
  the fantasy actually more about protecting a handful of irreplaceable
  people through a hostile world?
- **Resolved (0009):** neither — the Ajah Lean is tied to whichever Ajah
  the sitting Amyrlin Seat came from (a Siuan-Sanche-and-the-Blue-Ajah
  pattern), with a matched bonus/detriment against a rival Ajah, rather
  than a static player pick or a full set of parallel sub-faction
  rulesets. See `05-factions.md`'s Internal politics section.

### 2. Strategic layer specifics
- Recruitment: **resolved (0009)** — runs through the alliance network.
  Allied nations send novices into the training pipeline alongside gold
  tribute and borrowed levies, so a bigger alliance web compounds into
  faster long-term growth, not just immediate income.
- **Resolved (0009):** the Amyrlin Seat is a unique Hero/Commander unit
  whose home Ajah sets the faction-wide Lean. Losing her (death, capture,
  Stilling, retirement) triggers a succession event that can change the
  Lean entirely.
- **Resolved (0009):** yes — **Unity** is the aggregate-Favor stability
  stat, and a badly resolved succession (or a succession while Unity is
  already low) can trigger a **Tower schism**, splitting the faction into
  two rival Amyrlins rather than just weakening it. A low-Favor Ajah is
  also a preferential Darkfriend Network target, tying White Tower's
  internal politics directly to the Shadow's existing subversion mechanic.
- **Resolved (0008):** Bonded Warders are an optional upgrade, not every
  Aes Sedai's default, and losing one does cut both ways — a real
  mutual-loss penalty on the pair, not just a stat loss on one side.

### 3. Tactical layer specifics
- **Resolved (0008):** roster is four tiers — Tower Guard, Warder
  Company (squad-scale, elite-tagged, the actual line-holding answer),
  Aes Sedai (individual-scale), and the optional Bonded Warder upgrade —
  not the thin two-piece roster originally sketched. See `07-units.md`'s
  White Tower worked example for the composition target.
- Should some Ajahs fight more directly than others (Green historically
  battle-oriented) while others (Brown, White) are almost never on a
  front line without heavy protection? If so, does that mean different
  Ajah-flavored Aes Sedai units have meaningfully different combat stats,
  not just different weave lists?

### 4. Channeling & rituals interaction
- White Tower is the "home institution" for Stilling/Gentling in the
  fiction — should they get a mechanical edge at assembling a
  Stilling circle (faster to link, shorter cast window) since it's
  literally their function, distinct from any other faction attempting
  the same generic Ritual?
- Should there be a White-Tower-flavored strategic action — "Try a
  Darkfriend" — that runs Stilling on a captured Black Ajah/Darkfriend
  prisoner specifically, narratively distinct even if mechanically
  identical to the generic Ritual?

### 5. Relationships
- Obvious rival: the Shadow. Should there also be a built-in ideological
  friction with the **Seanchan** specifically (collaring channelers as
  damane is close to the White Tower's worst nightmare) that the
  strategic AI leans into — e.g., White Tower AI prioritizes opposing
  Seanchan expansion even at the cost of other goals?

### 6. Risk/cost, pressure-tested
- Current stated risk: burnout, weak raw numbers. Is "weak raw numbers"
  actually enforced by the roster answer in §3, or does it need a harder
  cap (e.g., a strategic-layer limit on how many Aes Sedai can exist at
  once, tied to the training-pipeline question above)?
- **Resolved (0009):** "political fracture risk" is now a concrete
  mechanic (Favor/Unity/schism), not just a stated theme — see §2. Still
  open: exact Favor/Unity numbers and decay rates, and the exact
  succession-resolution formula (Favor-weighted lottery vs. player-driven
  contest vs. hybrid) — both Phase 6 balance questions.
- New from this round, still open: the **win condition** ("Unite the
  Bound," `09-campaign-and-progression.md`) needs its exact
  alliance-coverage threshold defined, and it's worth checking whether it
  actually rewards the political playstyle enough relative to a
  conquest-focused White Tower run, once both are prototyped.

---

## Children of the Light (Whitecloaks)

### 1. Identity & fantasy
- One-sentence pitch: "the faction with no magic answer but the best
  mundane army in the game, and a chip on its shoulder about
  channelers" — does the zealotry need its own double-edged mechanic
  (e.g., a Zealotry meter that boosts combat stats but risks provoking
  unwanted wars or unrest in occupied non-Whitecloak provinces), or is
  "no channelers, ever" already enough identity on its own?

### 2. Strategic layer specifics
- Recruitment: straightforward Gold/numbers-focused mass conscription
  ("Questioners"/rank-and-file "Children")? Is this deliberately the
  simplest economy in the game, as a contrast to every magic-touched
  faction?
- Is there a unique **Inquisition** strategic action — investigating a
  province or enemy army for hidden channelers/Darkfriends — that can
  surface a Black Ajah agent or set up a Capture opportunity? This would
  give Whitecloaks their own counter-play against the Shadow's Darkfriend
  Network, which currently has no explicit counter anywhere in the docs.
- Should the strategic AI give Whitecloaks an automatic hostility lean
  against any channeling faction they border, even absent normal
  provocation — i.e., is anti-channeler war their default posture, not
  just a flavor option?

### 3. Tactical layer specifics
- Roster: heavy disciplined infantry (confirmed), plus cavalry (Whitecloaks
  fielded cavalry in canon) and what for ranged — do they have a
  signature "Questioner" unit built specifically around the anti-channeler
  toolkit, distinct from plain men-at-arms?
- What does the anti-channeler toolkit from `06-magic-and-channeling.md`'s
  open items actually **do**? Candidate mechanics to react to: reduces
  enemy Power reserve regeneration in an area; bonus damage/attack
  priority against the Channeler archetype specifically; a
  non-magical item that helps set up a Capture even without a friendly
  Shielder present.

### 4. Channeling & rituals interaction
- Whitecloaks have zero channelers, but Capture doesn't require the
  capturer to be one (per `04-tactical-battle-layer.md`) — worth
  confirming that explicitly, since Whitecloaks are the faction most
  likely to *want* prisoners.
- Should Whitecloaks have their own dark-mirror strategic action for a
  captured channeler — an **Execution/Burning** ritual, distinct from
  Stilling (mercy, removes the threat, keeps them alive) and Turning
  (converts them)? This would give a third faction (alongside Shadow's
  Turning and White Tower's institutional Stilling) its own unique
  prisoner-processing action, which is a strong asymmetry pattern worth
  deliberately extending here.

### 5. Relationships
- Should attacking a channeling faction (White Tower, Black Tower, Shadow)
  carry different diplomatic/event weight for Whitecloaks than attacking a
  non-channeling faction (Aiel, Borderlands) — i.e., is their doctrine
  specifically anti-channeler, not anti-everyone, and does the game
  reflect that distinction anywhere besides flavor text?

### 6. Risk/cost, pressure-tested
- "No channeling means no answer to enemy channelers beyond numbers,
  positioning, and specialized tools" is the current stated risk — once
  §3's toolkit is designed, does that risk still hold, or does the
  toolkit risk quietly turning Whitecloaks into a soft counter-channeler
  faction rather than a genuinely magic-less one? Worth checking once the
  toolkit exists.

---

## Aiel clans

### 1. Identity & fantasy
- One-sentence pitch: "small, elite, terrain-bound raiders who are
  lethal on their own terms and vulnerable on anyone else's" — does that
  land, or is the real fantasy more about **honor** (ji'e'toh) as a
  constraint the player has to play around, not just a flavor label?
- Should **ji'e'toh** be a real mechanic — units that refuse certain
  orders (won't retreat past a point, won't attack a yielded/surrendered
  foe) in exchange for morale/combat bonuses — making Aiel the one
  faction where the player doesn't have full tactical freedom over their
  own units? That's a genuinely distinctive, setting-authentic
  constraint, but it cuts against the "no reflex/no forced decisions"
  battle-layer pillar in a different way (a decision made *for* the
  player, not under time pressure) — worth discussing explicitly.
- Do individual clans (Taardad, Shaarad, Nakai, Reyn, etc.) matter
  mechanically at MVP, or is "Aiel" one unified faction for now with
  clan identity reserved as later-Phase flavor/variants?

### 2. Strategic layer specifics
- Since Aiel don't hold territory the way settled nations do (already
  stated), what does an actual Aiel turn consist of? Raiding for
  resources, honor-based recruitment, periodic clan gatherings that
  convert accumulated honor/raiding gains into something concrete?
- Should there be a slow-building **aggregation** mechanic — isolated
  clan war-bands gradually consolidating into a much larger, unified
  war-host — mirroring the books' actual structure (scattered clans →
  the Aiel invasion)? This could double as the "soft campaign clock"
  texture for an Aiel-adjacent campaign, similar to the Shadow-rising
  clock already floated in `09-campaign-and-progression.md`.

### 3. Tactical layer specifics
- Roster: Aiel Spear (sketched), Aiel bowmen (skirmisher), Maidens of the
  Spear (elite/scout?), Wise Ones (channelers who traditionally don't
  fight directly — support/utility archetype rather than offense?),
  fast runners/couriers for mobility since there's no cavalry.
- How is "no cavalry" compensated for mechanically — extra Move on
  foot units, ignoring terrain movement penalties that slow everyone
  else, both?

### 4. Channeling & rituals interaction
- Wise Ones channel but don't fight the way Aes Sedai do — are they a
  Channeler-archetype unit with a narrower, utility-only weave list (no
  offense), and can they still participate as Circle/Ritual participants
  if allied with a channeling faction, or are they mechanically walled
  off from that entirely?

### 5. Relationships
- Do Aiel start isolated beyond the Waste (consistent with the Q5
  recommended default anchor point) with a scripted trigger for when they
  cross into the rest of the map — tying into the campaign "soft clock"
  idea from §2 and from `09-campaign-and-progression.md`?

### 6. Risk/cost, pressure-tested
- Low numbers, terrain-dependent, weak in the open — is attrition also
  unusually *permanent* for Aiel (slow to reinforce, small population),
  making them a glass-cannon faction across a whole campaign and not just
  within a single battle? Worth stating explicitly if so, since it
  changes how a player should treat every Aiel casualty.

---

## Shadow (Trollocs, Myrddraal, Dreadlords, Black Ajah)

### 1. Identity & fantasy
- Current pitch (from `05-factions.md`/ADR 0004/0007): win through
  patient corruption and horde numbers rather than economy or magic
  finesse, where a single mistake (a discovered agent, a broken Turning
  circle) can cost everything built up slowly. Does that still feel like
  the right one-sentence hook after the Darkfriend Network work, or has
  the emphasis shifted more toward "the infiltration game" than "the
  horde game"?

### 2. Strategic layer specifics
- Does Blight-controlled territory **auto-generate** Trolloc numbers over
  time (a "spawning" economy unlike every gold-recruiting faction), and
  if so, does that make holding Blight territory itself a core Shadow
  strategic goal distinct from ordinary province value?
- Darkfriend Network mechanics, one level deeper: how is planting an
  agent actually paid for (a one-time spend, an ongoing drain), and is
  there a **discovery risk** other factions can invest against (tying
  into Whitecloak Inquisition from that faction's §2)?
- How dramatic/frequent should a province or army "flipping" to Shadow
  control via accumulated Darkfriend influence be, balance-wise? Too rare
  and the resource feels pointless; too common and it reads as a rug-pull
  to the faction losing it without a battle to react to.

### 3. Tactical layer specifics
- Roster: Trolloc (line, poor discipline, numerous — one generic unit at
  MVP, or several Trolloc-band flavors later), Myrddraal (fear-aura
  hero/commander — do they fight directly, or purely lead/terrify?),
  Dreadlord (channeler, high variance), Black Ajah (channeler, likely a
  *stronger* baseline weave list than a typical Dreadlord since they're
  White-Tower-trained — worth confirming that asymmetry deliberately).
- Fear mechanic, concretely: does a Myrddraal impose a morale penalty in
  an aura, or force a morale check specifically when an enemy unit
  becomes adjacent to it? Needs a concrete answer even if the exact
  numbers are a Phase 6 question.

### 4. Channeling & rituals interaction
- Already the deepest-built faction mechanically (Turning ritual,
  Darkfriend Network). One open thread: can the Shadow run
  Stilling/Gentling defensively — e.g., stilling their own Dreadlord who's
  gone irrecoverably mad from taint, as a mercy/control action — or is
  Stilling purely something done *to* the Shadow by others?
- Should a **failed** Turning attempt carry real backlash (the target
  dies; or a participating Dreadlord/Black Ajah goes irrecoverably mad)
  to keep the gambit appropriately terrifying rather than just "a wasted
  turn"?

### 5. Relationships
- Forsaken and Dreadlords canonically undercut each other — should there
  be an **internal rivalry** mechanic where fielding multiple hero-tier
  Shadow units at once carries its own friction/risk, mirroring
  White Tower's internal-unity question in the opposite direction (their
  risk is losing people to the Shadow; the Shadow's risk could be losing
  people to *each other*)?

### 6. Risk/cost, pressure-tested
- Already the most thoroughly specified risk profile in the doc set
  (poor Trolloc discipline, faster Dreadlord taint, exposed 26-unit
  Turning circles, discoverable agents). Does anything here need to be
  *harder* once the Darkfriend Network's exact numbers exist, so the
  Shadow's slow-build strength doesn't end up strictly better than a
  faster, more legible faction like Whitecloaks?

---

## Black Tower (Asha'man) — post-MVP, but worth full depth now

Deferred from the MVP shortlist (`docs/decisions/0004-mvp-faction-shortlist.md`)
but flagged as the faction that most directly exercises the taint/madness
mechanics — worth thinking through now so Phase 5 isn't starting cold.

### 1. Identity & fantasy
- One-sentence pitch: "fast-growing, aggressive, and running out the
  clock against its own success — every battle your Asha'man fight in
  brings the Tower closer to losing them to madness." Does that framing
  hold up, or is there a more hopeful angle worth keeping too (the Black
  Tower as the first real institution for male channelers instead of a
  death sentence)?

### 2. Strategic layer specifics
- Recruitment: explicitly faster/cheaper than White Tower (per the
  existing brief) — what's the actual lever? Lower Gold cost per new
  Asha'man, a shorter training pipeline than White Tower's Accepted
  process, or both?
- Should there be a Tower-wide taint-risk strategic event — past some
  faction-average taint threshold, an Asha'man defects or turns on a
  friendly province — mirroring the books' fear of the Black Tower
  "turning" as a whole?

### 3. Tactical layer specifics
- Roster: Asha'man Soldier (sketched), a stronger Asha'man tier
  (Dedicated-equivalent — more powerful weaves, faster taint accrual?),
  and — do they field *any* non-channeler infantry, or is the whole
  faction unusually magic-dense and numerically small as a result?
- Should Black Tower channelers get access to combat-oriented weaves
  White Tower doesn't typically use (reflecting martial-first training),
  making their weave list diverge from White Tower's in kind, not just in
  taint risk?

### 4. Channeling & rituals interaction
- Is a high-taint Black Tower channeler an explicitly *easier* Stilling
  target for enemies (a house-rule variance from Aes Sedai, reflecting
  how visibly unstable they are), making Black Tower a faction that has
  to actively protect its own most valuable/most dangerous units from a
  13-circle more than any other faction does?

---

## Post-MVP factions — forward-looking questions only

Full depth deferred to when each enters the Phase 5 build queue
(`05-factions.md`), but flagging the branching questions now so they're
not discovered cold later.

### Seanchan (Ever Victorious Army)
- Should collaring a captured channeler into a damane be its own
  Prisoner-processing action — parallel to Shadow's Turning and (if built)
  Whitecloak Execution — making Seanchan the third faction with a unique
  answer to "what do you do with a captured channeler"?
- Exotic beasts (raken, corlm, grolm): a new archetype tag, or folded
  into the existing Beast/Shadowspawn archetype with Seanchan-specific
  flavor?

### Borderlands nations (Shienar, Malkier, Kandor, Arafel)
- One unified "Borderlands" faction, or eventually split into distinct
  playable nations? Affects roster size ambitions and ties to the Q6 map
  scope decision.
- Passive combat bonus specifically vs. Shadowspawn units, reflecting
  generations of border war?

### Andor / southern nations
- Deliberately the generalist "fewest asymmetric rules to learn" faction
  — should this be the game's recommended first/tutorial faction once
  built?

### Ogier
- Rare and conflict-averse enough that "playable faction with almost no
  standing army" might be the wrong shape entirely — should Ogier instead
  be primarily a recruitable elite unit-source/ally usable *by* other
  factions, rather than a faction in their own right? Worth deciding
  before any Ogier-specific content work starts.

### Sea Folk (Atha'an Miere)
- Entirely gated on whether naval provinces/battles ever enter scope —
  worth an explicit yes/no before Phase 5, since "no" collapses Sea Folk
  down to a non-playable ally/trade mechanic rather than a full faction.

### Forsaken
- How many exist at launch, and are they unique per campaign (only one
  player or AI faction can have a given Forsaken active at a time, world
  wide)?
- Do they each carry bespoke, individually-authored abilities outside the
  generic Channeler weave list — effectively a mini-ruleset per Forsaken,
  the way Ter'angreal items are individually bespoke — rather than being
  built from the standard Hero/Commander template?
