---
title: About this course
author: S. Le Boulanger
date: 2026-09-07
description: "What this Polish course covers, who it is for, how it is sequenced, how it aligns to the CEFR, and what it deliberately leaves out."
---

## What this is

**PFL** is a free, openly-licensed Polish course for adults and older teenagers
working in English. It runs from a short pre-A1 primer on sounds and spelling
through the CEFR levels **A1, A2, B1 and B2**. Every page is a static HTML
document served from a public repository: no account, no tracking of
individuals, no advertising, nothing behind a paywall. Teaching content is
licensed **CC BY-SA 4.0** and the site code is MIT, so a teacher may print a
worksheet, cut it up, translate it or rebuild the whole site under the same
terms.

The course exists because Polish is badly served by open material at this
production standard. It is among the most widely taught Slavic languages in
Europe, with a large diaspora and a steady inbound migration for work and
study, and yet the freely available resources thin out sharply above A2. It is
also a useful stress test for the shared boulingua template, which until now
has carried only Germanic and Romance languages.

## Who it is for

Adult and older-teen beginners through upper-intermediate learners, working
from English. Three groups in particular:

- people who have moved, or are about to move, to Poland for work or study, and
  need the language of offices, landlords, shops and clinics before they need
  the language of literature;
- heritage learners who understand more than they can produce, and who
  typically need the writing system and the case endings rather than the
  vocabulary;
- teachers and tutors looking for classroom-ready, reusable material with
  answer keys, printable worksheets and a defensible curriculum mapping.

The metalanguage is English throughout. A German-facing edition would serve a
large Polish–German learner population and is a plausible later project, but it
is out of scope for this first edition.

## How it is sequenced

Three features of Polish dominate the pacing, and the course is arranged around
them rather than around a topic list.

**The seven cases.** Nominative, genitive, dative, accusative, instrumental,
locative and vocative, across three singular genders and the virile/non-virile
plural split. Cases are introduced **one function at a time** — the accusative
when you order something, the instrumental when you say what you are, the
genitive when you say what there is not — and the full paradigm is assembled
only once several of a case's uses are already in use. Consolidation of the
whole system belongs to B1, not to A1.

**Verbal aspect.** The perfective/imperfective pairing runs through every tense
from the first units onward and has no clean equivalent in English or German.
It is treated as a recurring thread with its own descriptor coverage rather
than as a single unit that can be ticked off, and vocabulary is presented in
pairs from the moment the past tense appears.

**Sounds and spelling.** Polish uses the Latin alphabet with diacritics
(ą ć ę ł ń ó ś ź ż) and a set of digraphs (sz cz rz dz dź dż). The system is
regular and can be learned in a few sittings, but it must be learned *first*,
which is why the course opens with a pre-A1 stage rather than with greetings.
Stress falls on the penultimate syllable with a small, listable set of
exceptions.

Two further threads are deliberately spread rather than dropped into a single
unit: **numeral government** (the 2–4 versus 5-and-above split, and the
genitive of quantity), and the **formal/informal address** distinction —
*pan*/*pani* with the third person versus *ty*. In Polish the latter is not
politeness trivia that can be appended at B1; it decides the verb form in the
first conversation a learner has, so it appears at A1.

## Curriculum alignment

The course maps to the CEFR through the shared
[boulingua curriculum framework](https://github.com/boulingua/curriculum),
which assigns stable identifiers of the form `{LEVEL}.{DOMAIN}.{SCALE}.{SEQ}`
to Can-Do statements derived from the CEFR Companion Volume (2020). Each unit's
front matter carries the descriptor identifiers it implements, and a machine-
readable conformance manifest records, scale by scale, what is covered and
what the Companion Volume simply does not describe at that level.

The declared target is **`core` conformance across A1–B1**: every in-scope
scale that has an official descriptor at those levels is implemented, and cells
the Companion Volume leaves empty are recorded as `no-official-descriptor`
rather than quietly filled in. **B2 is declared as a partial extension** beyond
`core` — it is authored in full, but `core`'s successor level also mandates C1,
which this edition does not attempt. Mediation and plurilingual scales are the
thinnest part of the coverage and are declared partial where that is the honest
description. Overclaiming coverage would be the only real conformance failure.

C1 and C2 are out of scope for this edition. Signing competences receive no
identifiers, per the framework.

## What comes with each unit

Each unit is one page with the same five moves — **objectives, input, practise,
produce, reflect** — and carries a slide deck and a worksheet as PDFs, both
generated from the shared branded LaTeX templates and committed to the
repository, together with native-voice audio and full transcripts. Exams are
first-class pages of the same kind, one model exam per level, with a printable
PDF and a stated duration, point total and pass mark.

Audio is synthesised with the shared [audiogen](https://github.com/boulingua/audiogen)
pipeline. For Polish this is subject to an explicit quality gate: nasal vowels,
the palatalised ś/ć/ź/dź series, ł and the consonant clusters are exactly where
text-to-speech fails, so a diagnostic set is auditioned before any voice is
adopted. Where a voice mispronounces a segment, that segment ships as a
transcript only until a suitable voice or a licensed native recording exists.
The decision is recorded in each unit's audio manifest rather than left
implicit.

## A recurring cast

Units share a small ensemble so that vocabulary, register and situations
accumulate rather than reset: **Kasia**, a student in Kraków; **Tomek**, her
friend; and a newcomer to Poland who arrives in the first A1 unit and learns
alongside the reader. The cast exists to make the formal/informal distinction
concrete — the same speaker addresses a friend and a landlord differently in
the same week — and to let a dialogue in unit ten assume what unit three
introduced.

## What this is not

It is not a certification course and has no relationship with any examination
board. The model exams are the author's own didactic adaptations, written to
resemble the publicly documented shape of CEFR-aligned examinations; they
confer nothing. It is not a reference grammar, though the
[appendices](/appendices/) carry the tables you will want beside you. And it is
not finished: see the
[roadmap](https://github.com/boulingua/pfl/blob/main/ROADMAP.md) for what is
written, what is being written, and in what order.

## Corrections

Errors in a language course are inevitable and worth reporting. The fastest
route is an issue in the
[repository](https://github.com/boulingua/pfl/issues); contact details are on
the [Impressum](/impressum/).
