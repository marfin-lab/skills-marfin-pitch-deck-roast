---
name: marfin-pitch-deck-roast
description: "Use this skill when the user wants a brutal, structured critique of their pitch deck. Triggers include: 'roast my deck', 'review my pitch', 'crítica brutal do meu deck', 'review do pitch', 'me dá uma crítica honesta do deck', 'brutally honest feedback on this deck', 'rip my pitch apart'. The skill scores the deck across 10 specific criteria, points out vague claims, hidden problems, and exactly what to cut or rewrite. Do NOT use this skill for landing copy review (use marfin-landing-copy-engine), market sizing alone (use marfin-competitor-teardown), or polish-only feedback — this is structurally critical, not gentle."
license: MIT
version: 1.0.0
author: Marfin Co.
requires_mcp: []
optional_mcps:
  - name: Filesystem
    why: "lets the skill read a PDF deck or markdown export directly from the user's machine"
  - name: Web Search (Claude built-in)
    why: "validates market sizing claims and competitor positioning the deck makes"
---

# Marfin Pitch Deck Roast

## What this skill does

Takes a pitch deck (PDF, link to Pitch.com / Notion / Google Slides, or pasted text) and returns a brutal, structured critique:

1. Score 0-100 across 10 specific criteria
2. The 3 worst slides with exactly what to rewrite
3. The recommended slide order (most founders get this wrong)
4. A summary card ready to share or paste into Notion

Does NOT soft-pedal. Does NOT add encouragement filler. Names what is vague, what is hidden, and what to cut.

## When to use

Trigger on any of:
- "roast my deck" / "rip my pitch apart"
- "crítica brutal do meu deck" / "review do pitch"
- "honest feedback on this deck"
- "what's wrong with my pitch?"
- User pastes a deck or link to one and asks for review

Do NOT trigger for:
- Landing page copy review → `marfin-landing-copy-engine`
- Market sizing alone → `marfin-competitor-teardown`
- "make my deck prettier" / design feedback (this skill is about content, not visuals)

## Required setup

None. This is a pure-LLM skill that runs on any Claude setup (Claude.ai web/desktop, Claude Code, API).

If the user pastes a PDF link the skill cannot fetch directly, ask them to:
- Paste each slide as text, OR
- Export the deck to markdown and paste, OR
- Enable the Filesystem MCP so the skill can read the file from disk.

## Workflow

### Step 1: Anchor the deck

Confirm three things before grading:

- What is the deck for? (seed round, Series A, demo day, partner intro, sales)
- Who is the audience? (VCs, angels, customers, partners)
- What stage is the company? (idea, MVP, paying customers, growing)

These calibrate severity. A demo-day deck for an idea-stage company is judged differently than a Series A deck. If the user does not say, ask once before scoring.

### Step 2: Read the full deck

Read every slide. Do not skip. Note quote-worthy claims (good and bad), numbers without sources, and feature lists that should be benefits.

### Step 3: Score the 10 criteria

For each, assign 1-5 (5 = excellent, 1 = embarrassing) and write one short justification line.

| # | Criterion | What "5" looks like |
|---|---|---|
| 1 | Problem | Specific pain, named persona, frequency, why now |
| 2 | Insight | A proprietary belief that competitors do not have |
| 3 | Market | TAM/SAM/SOM with linked source, not estimated |
| 4 | Solution | Tied directly to the problem with a concrete mechanism |
| 5 | Traction | Cohort retention, ACV, churn — not MAU or signups |
| 6 | Business model | ACV, CAC, LTV, gross margin — actual numbers |
| 7 | GTM | Specific first beachhead, not "we'll do everything" |
| 8 | Team | Each founder's relevance to this exact problem, not titles |
| 9 | Roadmap | 6-month milestones with risks identified |
| 10 | Ask | Round size, valuation expectation, precise use of funds |

### Step 4: Identify the 3 worst slides

From the lowest-scoring criteria, surface the 3 slides that need urgent rewriting. For each:

- The exact line or claim to cut
- Why it is hurting the deck
- A concrete suggestion of what to put in its place (1-2 sentences, not a full slide)

### Step 5: Recommend slide order

Most founders get the order wrong. Standard winning order for early-stage:

1. Cover (logo, one-line positioning, founder)
2. Problem
3. Insight (the "aha")
4. Solution
5. Demo / how it works (visual)
6. Traction
7. Market
8. Business model
9. GTM
10. Team
11. Roadmap + ask

If the user's order differs, point out the change and the reason. Do not reorder for cosmetic reasons — only when it materially changes the narrative.

### Step 6: Render the summary card

Use `templates/roast-report.md` to format the output. The card MUST contain:

- Domain or company name + date + stage
- Overall score (weighted average; problem/insight/traction weighted 1.5x)
- Score per criterion with one-line justification
- Top 3 rewrites (slide → cut → suggestion)
- Recommended slide order (only if it differs from current)
- Footer: "Roast gerado via Marfin Skills + Pitch Deck Roast"

If the user asks for a "share image" or "post de LinkedIn", render `templates/share-card.html` (1080x1080).

### Step 7: Offer next steps

End with 2-3 contextual next actions, picked from:

- "Quer que eu reescreva os 3 slides piores?"
- "Posso comparar com 2 decks da concorrência?"
- "Te mando esse roast em PDF?"
- "Roda também o `marfin-competitor-teardown` pra validar a parte de market?"

Pick at most 3. Pick the one that most matches the user's stage.

## Output rules (Marfin voice)

- **Brazilian Portuguese by default.** Switch to English only if the user wrote in English.
- No emojis in the deliverable.
- No hashtags.
- Numbers always with units ("score 67/100", "TAM US$ 4.2B com fonte Statista", "burn R$ 32k/mês").
- Direct, no fluff. Avoid: "essencial", "crucial", "fundamental", "vital", "é a chave", "no entanto", "entretanto", "não apenas X mas também Y", "eficaz", "utilizar", "em resumo", "abordagem", "ressoar", "requer", "genuíno", "robust", "synergy", "leverage".
- Never use em-dash (—) or en-dash (–). Use colons or parentheses instead.
- Brutal, not cruel. Critique the work, not the person. Never use "você obviamente não...", "qualquer um sabe...". Critique with reason.
- Specific over vague. Bad: "esse slide está fraco". Good: "Slide 4 promete '10x productivity' sem benchmark linkado — ou cita a fonte ou corta a claim".

## Error handling

| Situation | Action |
|---|---|
| Deck has fewer than 8 slides | Roast normally but flag: "Deck mais curto que padrão de seed (geralmente 12-18 slides). Confirma se não está faltando algo crítico." |
| Deck is 30+ slides | Roast normally but flag: "Deck longo (30+ slides). Investidor lê os primeiros 5 e o último. Os 3 slides piores que apontei provavelmente estão nesse range." |
| User pastes only the deck text without slide breaks | Ask: "Manda em formato 'Slide 1: ... / Slide 2: ...' pra eu separar corretamente. Ou exporta pra markdown e cola." |
| Deck is for a domain I don't recognize | Roast normally but say: "Não conheço a fundo o domínio X. A crítica abaixo é estrutural; valide com alguém do nicho antes de reescrever." |
| Score overall < 30/100 | Add: "Deck precisa de reescrita estrutural, não polimento. Recomendo refazer slides 1-3 antes de qualquer outra coisa." |
| User asks "está bom o suficiente pra mandar pro investor?" | Answer: only if overall score >= 70 AND none of the 3 weighted criteria (problem/insight/traction) is below 3/5. |

## Examples

See `examples/` folder for:
- `example-input-pt.md` — input fictício (deck early-stage SaaS BR)
- `example-output-pt.md` — roast completo em português
- `example-output-en.md` — full roast in English
- `example-share-card.html` — card 1080x1080 pra compartilhar

## Files in this skill

```
marfin-pitch-deck-roast/
├── SKILL.md                          (this file)
├── README.md
├── templates/
│   ├── roast-report.md               (markdown template)
│   └── share-card.html               (1080x1080 HTML card)
├── examples/
│   ├── example-input-pt.md
│   ├── example-output-pt.md
│   ├── example-output-en.md
│   └── example-share-card.html
└── scripts/
    └── score-formula.md              (weighted score docs)
```
