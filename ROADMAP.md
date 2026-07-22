# PFL — Polish course roadmap

Status: **coming soon** (empty scaffold — LICENSE, README, brand icons only).
This roadmap is the build plan to take `pfl` from scaffold to an active course on
the boulingua world map, conforming to the `pagegen` template, the `curriculum`
framework, and the VG Wort standard. Course code: **`pfl`**. Signature accent:
**`#AD701F`** (already registered in `pagegen/data/accents.yaml`).

---

## 1. Overview

**What this is.** A free, CEFR-aligned, open (CC BY-SA 4.0) Polish course for
self-learners and teachers, built on the shared boulingua Hugo template. Units,
exams, materials (slide decks + worksheets) and native-voice audio, all
committed, all statically hosted on GitHub Pages.

**Target learners.** Adult and older-teen beginners through upper-intermediate,
predominantly English- or German-speaking (interface/metalanguage in English,
matching `languageCode = "en"`), including heritage learners and people
relocating to Poland for work or study.

**Realistic CEFR scope.** **A1–B2**, plus a short **pre-A1 orthography &
pronunciation onboarding** stage. C1–C2 are explicitly out of scope for the
first edition (freely-available OER rarely reaches C1 for Polish, and the
mediation/plurilingual descriptor material is thin — see §4).

**Why Polish.** A large, in-demand Slavic language with almost no polished free
OER at this production standard; strong diaspora and inbound-migration demand;
and a genuinely instructive test of the template against a heavily inflected
language (the existing courses are Germanic/Romance).

**The 3–5 defining challenges.**
1. **Seven-case declension.** Nominative, genitive, dative, accusative,
   instrumental, locative, vocative — across three singular genders and the
   virile/non-virile plural split. This is the dominant grammar load and dictates
   pacing: cases must be introduced one function at a time, not as a paradigm dump.
2. **Verbal aspect.** The perfective/imperfective pairing pervades every tense
   from A1 onward; there is no clean English/German mapping, so it needs its own
   recurring thread and its own `language_awareness` descriptor coverage.
3. **Orthography & phonology.** Latin script *plus* diacritics (ą ć ę ł ń ó ś ź ż),
   digraphs (sz cz rz dz dź dż), nasal vowels, and palatalisation. Learnable in
   days, but needs an explicit onboarding stage and reliable native audio.
4. **Native TTS quality.** Piper Polish voices must be auditioned before we commit
   to a synthesis pipeline (diacritics, palatalised consonants, nasal vowels are
   where TTS fails); a fallback decision is required (§2, §6).
5. **Number & quantifier agreement.** Polish numeral government (2–4 vs 5+,
   genitive of quantity) is a recurring stumbling block that must be threaded
   deliberately rather than dropped into one unit.

---

## 2. Language & localisation decisions

Concrete, opinionated choices — one recommendation each.

- **Writing system.** Latin + Polish diacritics. **No** custom script handling
  needed; the concern is font coverage, not shaping. **Decision:** keep the
  hugo-coder defaults but verify the body/heading stack renders the full Polish
  Latin-Extended-A set (ą ć ę ł ń ó ś ź ż and uppercase) with correct ogonek/kreska
  placement; if any glyph falls back, pin a self-hosted, SIL/OFL-licensed face with
  verified Polish coverage (e.g. a libre sans with Latin Extended-A). Verify the
  ł and the combining ogonek specifically.
- **Direction.** LTR. **No RTL work.**
- **Variant / register.** Standard literary Polish (*język ogólnopolski*); no
  dialect branch. **Decision:** teach the standard, but make the **formal vs
  informal address** distinction (pan/pani + 3rd person vs *ty*) a first-class,
  early sociolinguistic thread — it is not optional politeness trivia in Polish.
- **Pre-A1 onboarding stage.** **Decision: yes, include one.** A compact
  `get-started` pronunciation & orthography primer (alphabet, diacritics,
  digraphs, nasal vowels, stress-on-penult rule) rendered as a normal section with
  audio — *not* a full CEFR level. It carries `preA1` `LING`/`PRAG` descriptor
  coverage where the CV has descriptors and `no-official-descriptor` otherwise.
- **Native voice / TTS.** **Decision:** default to the boulingua `audiogen`/Piper
  pipeline using a Polish Piper voice (e.g. `pl_PL-darkman-medium` /
  `pl_PL-gosia-medium`), **contingent on an audition gate**: synthesize a
  diagnostic set (nasal vowels, palatalised series ś/ć/ź/dź, ł, consonant clusters,
  numeral agreement phrases) and human-verify. If quality is inadequate, fall back
  to (a) a different Piper voice, or (b) ship transcripts-only for the affected
  segments until a better voice or licensed native recordings are available. Never
  ship audio that mispronounces diacritics — record the decision in the audio
  manifest.

---

## 3. Instantiation from pagegen

Stand up the buildable site first; author content second.

1. **Copy the template.** Instantiate `boulingua/pfl` from `pagegen` (template
   files only — not `public/`, and start `data/vgwort.yaml` empty).
2. **Edit `hugo.toml`** — change only the marked values:
   - `baseURL = "https://boulingua.github.io/pfl/"`
   - `title = "PFL — Polish"` , `languageCode = "en"` , `defaultContentLanguage = "en"`
   - `[params] navTitle = "Polski"` (brand), `description` + `keywords` (Polish, CEFR, OER),
   - `params.code = "pfl"` (selects the `#AD701F` accent from `data/accents.yaml`),
   - `[[params.social]] url = "https://github.com/boulingua/pfl"`,
   - `[params.plausible] domain = "boulingua.github.io/pfl"` (keep this block **last** — TOML sub-table trap),
   - `[[menu.main]]` sections mirroring `content/pfl-*/` (see §5): Get started, A1, A2, B1, B2, Materials, About, Legal.
3. **Regenerate brand.** Run `python brand/make_icon.py` to regenerate the
   pentagon icon + favicons from the `pfl` accent. Confirm the swatch matches
   `#AD701F` / hover `#865618` / dark `#E7B97E`.
4. **Confirm accent.** `data/accents.yaml` already carries `pfl` — verify, don't
   re-add.
5. **Legal.** Fill the ⟨…⟩ placeholders in `impressum` / `datenschutz` /
   `haftungsausschluss`; disclose VG Wort METIS counting in `datenschutz`.
6. **First green build.** `hugo --minify --gc` locally; push; confirm the
   `build-deploy.yml` gate battery passes and GitHub Pages serves the site.
   Acceptance: home + one placeholder level section render with the correct accent
   and pentagon favicon.

---

## 4. Curriculum conformance target

**Declared conformance level: `core` (A1–B1), fully.** B2 is authored as a
**declared partial extension** beyond `core` (not `full`, since `full` also
mandates C1). This is the honest instantiation posture the framework expects
(`curriculum/docs/conformance.md`): declare the gap, don't lower the framework.

- **Fully implement** (per `core`): every **in-scope** scale that has an official
  A1/A2/B1 descriptor across REC, PROD, INT, MED, PLUR, LING, SOC, PRAG. Cells the
  CV leaves empty are recorded as `no-official-descriptor` — a silently missing
  scale is the only conformance failure.
- **Realistically thin, declared partial at B1 and across B2:** the mediation
  (`MED`) sub-scales and plurilingual (`PLUR`) scales — mediation OER is scarce.
  Implement the mediation/plurilingual descriptors we can genuinely support and
  mark the rest honestly.
- **Out of scope, no IDs minted:** `SIGN` (per framework); C1–C2 for this edition.
- **Mapping plan.** Each unit's front-matter `curriculum` block uses
  `framework: cefr` with `cefr_level` and `cefr_can_do: [...]` referencing
  descriptor IDs of the form `{LEVEL}.{DOMAIN}.{SCALE}.{SEQ}` drawn from
  `curriculum/levels/*.md` (e.g. `A1.INT.information-exchange.01`,
  `A2.LING.grammatical-accuracy.02` for a case unit).
- **Machine-readable scope manifest.** Publish a `conformance.yml` (modelled on
  `curriculum/examples/de-a1/conformance.yml`): `framework_version`,
  `language: pl`, `declared_conformance`, and per-scale `levels covered vs
  no-official-descriptor`, plus `realizations:` mapping each `implements_id` to its
  Polish realisation. **Every `implements_id` must resolve** so that
  `curriculum/scripts/id-audit.sh` passes (format, uniqueness, in-scope scale,
  level agreement). Add a CI step that runs the id-audit against our manifest.

---

## 5. Content creation plan

Recurring cast & theme (continuity aid): a small ensemble — e.g. **Kasia** (a
student in Kraków), **Tomek**, and an international newcomer — reused across units
so vocabulary, register (pan/pani vs ty) and situations build cumulatively.

Content model (per `pagegen/docs/front-matter-fields.md`): page bundles under
`content/<section>/units/<unitNN-slug>/index.md`; exams as **first-class sibling
bundles** (`<unitNN-slug>-exam/` or per-level model exams), linked by `unit_nr`;
section landings via **shortcodes only** (`hero`, `kicker`, `lead`, `card-grid`,
`card`, `callout`, `details`, `downloads`) — never raw HTML.

Effort tags: **S** ≈ ≤1 day · **M** ≈ 2–4 days · **L** ≈ ≥1 week per bundle.

| Phase | Section | Units | Focus | Effort |
|---|---|---|---|---|
| 0 | `get-started` (pre-A1) | 3–4 primer pages | Alphabet, diacritics, digraphs, nasal vowels, penultimate stress, greetings | **M** |
| 1 | A1 | ~12 units | Introductions, nominative + first accusative, present tense, aspect intro, numbers 1–20, family, food, place | **L** |
| 2 | A2 | ~12 units | Genitive/dative/instrumental/locative in function, past tense + aspect pairs, motion verbs intro, shopping, health, travel | **L** |
| 3 | B1 | ~14 units | Full case system consolidation, aspect in narration, conditional, numeral government, work/study, opinions | **L** |
| 4 | B2 (partial extension) | ~12–14 units | Register nuance, abstract topics, participles, reported speech, argument, mediation tasks | **L** |

**Exams.** One model exam per level as a first-class sibling bundle
(`…-exam/index.md`, `page_type: exam`) with `duration_min`, `total_points`,
`notenschluessel`, and a committed PDF under `static/downloads/<level>/`; optional
per-unit quick-checks. Exams carry their own `curriculum` block and skills modules.

**Appendices** (`content/appendices/<slug>/`): (a) **case tables** overview,
(b) **aspect pairs** reference, (c) **verb conjugation** patterns, (d) **numeral
agreement** cheatsheet, (e) **pronunciation & orthography** reference, (f)
**glossary**, (g) **common errors** for English/German speakers.

**Acceptance criteria per phase.** For each phase: every unit has the five-part
body (Objectives / Input / Practise / Produce / Reflect), a filled `curriculum`
block whose IDs pass id-audit, `skills_focus` set, committed slide deck +
worksheet (thumbnails rendered), audio (or a recorded transcripts-only decision),
a VG Wort mark if ≥1800 chars (§7), and a green build with no new coverage
warnings. A level is "phase-done" when all its units + its model exam meet this.

---

## 6. Website & materials

- **Section landings.** Each section `_index.md` (`page_type: section`) uses the
  shortcode kit: `hero`/`kicker`/`lead` intro + `card-grid`/`card` unit index.
  Mirror sections in `[[menu.main]]`.
- **Materials pipeline.** Generate decks and worksheets locally from the branded
  `slidegen`/`sheetgen` LaTeX templates via `scripts/build_materials_latex.py`;
  **commit** the PDFs under `static/materials/{presentations,worksheets}` and
  downloadable bundles under `static/downloads/`. CI **only verifies** presence +
  attribution (`verify_downloads.py`) — no TeX Live in the deploy path. Ensure the
  LaTeX toolchain has a font with Polish diacritic coverage.
- **Thumbnails.** `scripts/render_thumbs.py` produces per-deck/worksheet
  thumbnails; wire them into the unit front-matter `presentation`/`worksheet`
  `{file, thumbnail}`.
- **Audio.** `scripts/build_audio.py` (Piper) extracts vocab/dialogue/text
  segments, synthesizes OGG/Opus, writes `data/audio/<slug>.json`, and the unit
  layout renders an accessible "Listen" section with transcripts. **Polish
  decision:** gate on the §2 audition; ship transcripts-only for any segment where
  TTS mispronounces diacritics/palatalisation until a suitable voice/native
  recordings exist. Record the voice + decision in each manifest.
- **Downloads.** Exam PDFs and printable packs under `static/downloads/<level>/`,
  surfaced with the `downloads` shortcode; all attributed (CC BY-SA 4.0).

---

## 7. VG Wort — pixel assignment for ALL content pages

**Required and non-skippable.** Every content page that is an original creative
text of **≥ 1800 rendered characters** gets exactly one VG Wort Zählmarke, per
`pagegen/docs/vgwort-standard.md`. This covers **every unit, every exam, every
appendix, and every editorial page** (about, course overview, the pre-A1 primer
pages where ≥1800 chars). It does **not** cover navigation surfaces (home,
`/materials/`, tag/section indexes, paginated continuations) or the **templated
legal pages** (Impressum/Datenschutz/Haftungsausschluss).

Procedure for each qualifying page:
1. Draw a **fresh public code** (32-hex Öffentlicher Identifikationscode) from the
   author's **T.O.M.** account — never invent, never reuse a code already assigned,
   never expose the private code.
2. Register it in `data/vgwort.yaml`, matched by `url:` (base-stripped
   RelPermalink) or `path:`, with `pixel_url` / `public_id`, `min_chars: 1800`,
   `author`, `registered_at`.
3. It renders via the **shared resolver** (`layouts/_partials/vgwort/url.html`) →
   `<head>` preload + eager body `<img>` on `https://vg09.met.vgwort.de/na/<code>`
   — one GET per view, JS-free, no consent gate.
4. Record the mark in the **private usage registry** (kept outside the repo):
   Used, Projekt=`pfl`, Sprache=Polish, Niveau, Kurstitel, URL, Pixel_URL.
5. Gates: **coverage** (`verify_vgwort_coverage.py`, warns on unregistered ≥1800
   pages), **render verify** (`verify_rendered_pixels.py`, blocking — one mark per
   URL, present on its page), **hub guard** (`met.vgwort.de` absent from
   `/materials/`). Exclude `vgwort.de` from link-checkers.

**Estimated total marks needed.** Units ≈ 12+12+14+14 = **52**; model exams
**4** (+ optional per-unit checks); appendices **~7**; editorial (about, course
overview, pre-A1 primer pages ≥1800) **~4–6**. → **≈ 65–75 Zählmarken** for the
full A1–B2 edition; draw them in per-phase batches, not all up front.

---

## 8. Milestones & sequencing

**M0 — Scaffold live (S–M).** §3 complete: template copied, `hugo.toml` set,
brand regenerated, legal filled, first green build on GitHub Pages. Site shows
correct accent + favicon. *Still "coming soon" on the map.*

**M1 — Conformance skeleton (M).** Publish `conformance.yml` mapping the A1
in-scope descriptors; wire the id-audit CI step; confirm it passes.

**M2 — MVP: pre-A1 primer + A1 live (L).** `get-started` stage + all A1 units +
A1 model exam, with materials, audio (or recorded decision), and VG Wort marks.
First learner-usable slice.

**M3 — A2 complete (L).** Depends on M2 cast/vocabulary continuity.

**M4 — B1 complete → `core` conformance met (L).** With B1 done, the declared
`core` (A1–B1) conformance target is satisfied across all in-scope scales.

**M5 — B2 partial extension (L).** Upper-intermediate units + exam; update
`conformance.yml` to declare B2 partial.

**Dependencies.** §3 → everything. Audio audition (§2) gates M2's audio. Case
sequencing threads M2→M4. Materials/audio pipelines are per-unit and can run in
parallel with authoring.

**Definition of done — ready to flip from coming-soon to active.**
- Scaffold + brand + legal complete; CI green including VG Wort render gate.
- At minimum **M2 (pre-A1 + full A1 + A1 exam)** shipped end-to-end — ideally
  through **M4 (`core`/B1)** before flipping — with materials, audio decision,
  and VG Wort marks on every ≥1800-char page (coverage warnings at 0).
- `conformance.yml` published and passing id-audit; declared level accurate.
- No ⟨…⟩ placeholders remain; downloads present + attributed.
- World-map entry updated from "coming soon" to active with the correct link.

---

## 9. Open decisions & risks (language-specific)

- **Piper Polish voice quality** — primary risk. Nasal vowels, palatalised
  ś/ć/ź/dź, ł and clusters are where TTS breaks. *Mitigation:* audition gate;
  transcripts-only fallback; possible licensed native recordings later.
- **Case-introduction ordering** — pedagogical, not settled. Function-first
  (introduce each case by what it *does*) vs paradigm-first. *Recommendation:*
  function-first, spread across A1–B1; decide the exact sequence before M2.
- **Aspect as a thread** — how much to formalise at A1 vs let it accrete. Needs a
  consistent `language_awareness` descriptor mapping so it isn't orphaned.
- **Numeral government** — where to place the genitive-of-quantity / 2–4-vs-5+
  rules without overloading an early unit.
- **Metalanguage** — English interface confirmed; consider a German-facing
  variant later (large PL↔DE learner population) but out of scope for edition 1.
- **Font diacritic coverage** — must be verified in both the web stack and the
  LaTeX materials toolchain before M2; a missing ł/ogonek glyph is a blocker.
- **Mediation/plurilingual thinness** — declared-partial honestly per §4; risk is
  overclaiming coverage. Keep the manifest truthful.
