# marfin-pitch-deck-roast

Crítica brutal e estruturada do seu pitch deck em 60 segundos, dentro do Claude.

## O que essa Skill faz

- Lê seu deck (texto colado, link de Pitch.com / Notion / Slides, ou PDF)
- Avalia 10 critérios objetivos (problema, insight, mercado, tração, etc)
- Devolve score 0-100 ponderado
- Aponta os 3 slides com pior score e o que reescrever
- Sugere ordem ideal dos slides (a maior parte dos founders erra aqui)
- Gera card visual 1080x1080 pra compartilhar nas redes

Não amacia. Não adiciona elogio filler. Aponta o que está vago, escondido ou redundante.

## Demo

Pergunta no Claude: *"roast meu deck"* + cole as slides

Resposta em ~60s: [veja exemplo completo](examples/example-output-pt.md)

## Como instalar

### Opção 1: Claude Code (one-liner)

```bash
curl -sSL https://raw.githubusercontent.com/marfin-lab/skills/main/install.sh | sh -s pitch-deck-roast
```

Esse comando clona o repo pra `~/.claude/skills/marfin-pitch-deck-roast`. O Claude Code detecta automaticamente.

### Opção 2: Claude Code (manual)

```bash
git clone https://github.com/marfin-lab/skills-marfin-pitch-deck-roast.git ~/.claude/skills/marfin-pitch-deck-roast
```

### Opção 3: Claude.ai (web/desktop)

Baixe o [zip](https://github.com/marfin-lab/skills-marfin-pitch-deck-roast/archive/refs/heads/main.zip) e suba como skill personalizada na sua conta.

## Pré-requisitos

- Nenhum obrigatório. Skill funciona em qualquer setup do Claude.
- **Recomendado:** Filesystem MCP (lê PDF direto do disco) e Web Search (valida claims de mercado).

## Quando usar

- Antes de mandar o deck pro primeiro investor
- Quando você está achando que está bom (combate viés)
- Pré-demo day pra ensaiar a história
- Pra responder "por que estou perdendo deals?" se vende via deck

## Quando NÃO usar

- Polish de copy (use [marfin-landing-copy-engine](https://github.com/marfin-lab/skills-marfin-landing-copy-engine))
- Validar tese de mercado isolada (use [marfin-competitor-teardown](https://github.com/marfin-lab/skills-marfin-competitor-teardown))

## Os 10 critérios

1. **Problema** — específico, persona, frequência
2. **Insight** — aposta proprietária
3. **Mercado** — TAM/SAM/SOM com fonte
4. **Solução** — mecanismo, não feature dump
5. **Tração** — cohort, ACV, churn (não vanity)
6. **Modelo** — números reais
7. **GTM** — beachhead específico
8. **Time** — relevância pra esse problema
9. **Roadmap** — milestones com riscos
10. **Ask** — round, valuation, uso preciso

Score final é média ponderada. Problema, Insight e Tração contam 1.5x. Veja [scripts/score-formula.md](scripts/score-formula.md) pra detalhes.

## Roadmap

- [x] V1: roast + reescritas + card 1080x1080
- [ ] V2: comparação com 2-3 decks de concorrentes na mesma execução
- [ ] V3: integração com `marfin-cold-email-engine` pra gerar email de follow-up pós-call de investor

## Licença

MIT. Use, modifique, redistribua. Cite a Marfin se publicar derivada.

## Outras Skills da Marfin

| Skill | O que faz |
|---|---|
| [marfin-cold-email-engine](https://github.com/marfin-lab/skills-marfin-cold-email-engine) | Cold email personalizado com 3 variações |
| [marfin-competitor-teardown](https://github.com/marfin-lab/skills-marfin-competitor-teardown) | Teardown público de concorrente |
| [marfin-weekly-review](https://github.com/marfin-lab/skills-marfin-weekly-review) | Weekly review pra founder solo |
| [marfin-prd-writer](https://github.com/marfin-lab/skills-marfin-prd-writer) | PRD a partir de ideia bruta |

Catálogo completo: https://marfin.co/skills

---

Feito por [Marfin Co.](https://marfin.co) — venture builder de produtos com IA.
