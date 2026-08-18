# Factions

> Status: Draft — **MVP shortlist decided:** White Tower, Children of the
> Light, Aiel, Shadow (see `docs/decisions/0004-mvp-faction-shortlist.md`).
> Each entry below is a brief; full unit rosters live in `07-units.md` once
> a faction is greenlit for build.

## What makes a faction a faction here

Per pillar 2 (`00-pillars-and-pitch.md`), every faction needs a clear
answer to all four of these, or it isn't ready to design units for yet:

1. **Power source** — where does its strength come from (channeling type,
   numbers, discipline, terrain mastery, artifacts)?
2. **Strategic hook** — what does it do on the strategic layer that no
   other faction does?
3. **Tactical hook** — what does a battle led by this faction feel like
   that a battle led by another faction doesn't?
4. **Risk/cost** — every strength in this setting should come with a
   matched cost (taint, fragility, isolation, moral cost). A faction with
   no downside is a design bug.

## MVP factions (locked — `docs/decisions/0004-mvp-faction-shortlist.md`)

### White Tower (Aes Sedai)
- **Power source:** Saidar channeling, organized by Ajah specialization
  (Green = battle, Red = anti-male-channeler, Brown = knowledge/utility,
  Blue = causes/intrigue, etc.)
- **Strategic hook:** Recruits and moves by influence and politics as much
  as by gold; can act at range through Aes Sedai sent to other courts.
- **Tactical hook:** Small numbers of very powerful channelers plus modest
  conventional forces (Warders, levies) — battles are about protecting a
  handful of high-value units, not attrition.
- **Risk/cost:** Saidar burnout risk on overreach; politically fractious
  (Black Ajah subversion risk, see `03-strategic-layer.md`); relatively
  weak in raw troop numbers.

### Children of the Light (Whitecloaks)
- **Power source:** None — explicitly zero channelers, ever. Strength is
  numbers, discipline, and equipment.
- **Strategic hook:** Aggressive anti-channeler stance affects diplomacy
  and events (can trigger conflict with any channeling faction
  unprompted); draws conscripts (the Children's "Questioners") readily.
- **Tactical hook:** Disciplined, uniform infantry with strong formation
  bonuses; no magic to plan around, which makes them a useful "clean"
  tactical baseline faction and a hard, attrition-heavy matchup for
  magic-light factions.
- **Risk/cost:** No channeling means no answer to enemy channelers beyond
  numbers, positioning, and specialized anti-channeler tools/relics.

### Aiel (clans)
- **Power source:** Elite individual skill, terrain mastery, warrior
  society traditions — no cavalry, no channelers in the direct line of
  battle (Wise Ones channel but don't fight the way Aes Sedai do).
- **Strategic hook:** Doesn't hold territory the way a settled nation
  does; strategic incentives run on raiding, honor, and clan
  relationships rather than province economics.
- **Tactical hook:** Small elite forces that use terrain (forest, hills,
  broken ground) for ambush and mobility bonuses that other factions can't
  match; exposed and weak in open-ground stand-up fights.
- **Risk/cost:** Low raw numbers; strong specifically *because of* terrain,
  weak specifically *without* it — makes battlefield selection strategic.

### Shadow (Trollocs, Myrddraal, Dreadlords, Black Ajah)
- **Power source:** Numbers (Trollocs), fear (Myrddraal/Fades), corrupted
  saidin channeling (Dreadlords) — and, distinctively, **alliances**: the
  Shadow's core resource is people turned, bought, or blackmailed into
  serving it, not gold or land (see `08-economy-and-resources.md`).
- **Strategic hook:** Builds a **Darkfriend Network** — agents planted
  inside enemy provinces/factions — that can be cashed in for
  intelligence/resources or called on to trigger enemy unit/province
  defections, in addition to (and often instead of) open war from Blight
  territory. A well-developed network inside the White Tower is also the
  Shadow's pipeline to **Black Ajah**: sleeper Aes Sedai agents who can be
  activated into fieldable Shadow channeler units.
- **Tactical hook:** Horde-and-attrition play backed by fear effects that
  directly attack enemy morale, Dreadlord channeling that's more
  reckless/higher-variance than "legitimate" channeler factions, and the
  Shadow's signature battlefield gambit: with **13 Black Ajah + 13
  Myrddraal** linked around a captured, Shielded enemy channeler, the
  Shadow can permanently convert them to its side mid-battle — the
  Turning ritual (`06-magic-and-channeling.md`), unique to this faction.
- **Risk/cost:** Trolloc discipline is poor (harder to hold formation,
  more prone to breaking); Dreadlords take on taint/corruption risk faster
  than other saidin users due to how they train; the Darkfriend Network
  and Turning ritual are both slow, patient investments that can be lost
  in a single bad exchange — planted agents can be discovered and purged,
  and a Turning circle caught mid-ritual is 26 individual-scale units
  exposed and lost at once.

## Additional factions (post-MVP, Phase 5)

Briefs kept short — these get full treatment when they enter the build
queue.

- **Black Tower (Asha'man):** Saidin channeling, explicitly martial
  (trained as soldiers first, channelers second); strategic hook is
  fast-growing military power built around channeler-soldiers and
  aggressive recruitment; tactically, channelers are integrated directly
  into the battle line rather than protected in the rear — high offense,
  high risk. Taint accumulation is a constant, visible countdown; a Black
  Tower channeler pushed too hard is a long-term liability, not just a
  battlefield casualty. Deferred from the MVP shortlist (see
  `docs/decisions/0004-mvp-faction-shortlist.md`) — White Tower alone
  covers "channeling as core mechanic" for the vertical slice, but Black
  Tower is the faction that will most directly exercise the taint/madness
  mechanics in `06-magic-and-channeling.md`, so it's a strong Phase 5
  priority.
- **Seanchan (Ever Victorious Army):** Conquest-and-collar strategic hook
  (capturing enemy channelers converts them to damane); disciplined heavy
  infantry/cavalry plus damane-as-ranged-artillery tactically; exotic
  beasts (raken, grolm, corlm) as unique unit types; risk/cost is that
  damane require sul'dam handlers and are vulnerable if the handler falls.
- **Borderlands nations (Shienar, Malkier, Kandor, Arafel):** Heavy
  cavalry, Shadowspawn specialists, Warder-adjacent culture; strategic
  hook is permanent low-grade war footing against the Blight; risk/cost
  is being perpetually resource-strained from border defense.
- **Andor / southern nations:** Generalist medieval faction (knights,
  levies) — useful as a "default" baseline once the roster expands beyond
  the deliberately-asymmetric MVP set.
- **Ogier:** Rare, powerful, conflict-averse — recruit-limited hero-tier
  units rather than a standing army; Waygate access as a unique strategic
  tool; risk/cost is scarcity (you can't mass-produce Ogier support).
- **Sea Folk (Atha'an Miere):** Windfinder weather-channeling; naval
  focus — only relevant if/when naval provinces or battles enter scope
  (flagged as a scope question for whenever the map expands to the coast).
- **Forsaken:** Not a faction on their own — named, extremely powerful
  hero-tier units that can appear attached to the Shadow faction (or
  independently) as rare, campaign-defining threats. See `07-units.md` and
  `09-campaign-and-progression.md`.

## Faction design checklist

Before a faction is considered "designed" (not just "briefed"), it needs:

- [ ] The four-question answer above, filled in for real (not just this
      brief)
- [ ] A first-pass unit roster in `07-units.md`
- [ ] Its strategic-layer recruitment/resource rules specified in
      `03-strategic-layer.md` or a faction-specific addendum
- [ ] At least one thing it explicitly *cannot* do that another faction can
      — asymmetry needs a matching absence, not just a matching presence
