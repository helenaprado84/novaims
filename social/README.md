# Time de agentes de social media — Pine PR

Seis agentes que funcionam como uma equipe de mídias sociais para os perfis
institucionais da Pine PR no **LinkedIn**, no **Instagram** e no **site**.
Funcionam no **Claude Code** e no **GitHub Copilot** (VS Code), com o mesmo texto.

## O time

| Agente | Papel | Entrega | Altera arquivos? |
|---|---|---|---|
| `social-estrategista` | define pauta, pilar, canais e calendário | `briefing.md`, `calendario-AAAA-MM.md` | sim |
| `social-pesquisador` | busca dados em fontes verificadas e checa os textos | `fontes.md` | sim |
| `social-redator` | escreve para site, LinkedIn e Instagram | `site.md`, `linkedin.md`, `instagram.md` | sim |
| `social-designer` | briefing visual e peças no Canva | `visual.md` | sim |
| `social-revisor` | confere marca, fontes, canal e risco jurídico | veredito na conversa | **não** |
| `social-analista` | lê métricas reais e recomenda ajustes | `relatorio-AAAA-MM.md` | sim |

## O fluxo

```
estrategista → pesquisador → redator → designer → pesquisador (checagem) → revisor → aprovação humana
      ↑                                                                        │
      └──────────── analista (relatório mensal ajusta a próxima pauta) ◄───────┘
```

A skill **`producao-social`** conduz esse fluxo de ponta a ponta. **Nada é
publicado automaticamente**: a publicação continua sendo decisão humana.

## Antes do primeiro uso

1. **Preencha `social/marca-pine.md`.** Os agentes não inventam nada sobre a
   Pine: onde houver `[PREENCHER]`, eles param e perguntam. Os campos mais
   importantes: pilares, tom de voz com 2–3 posts reais de exemplo, quem aprova
   e quais clientes podem ser citados.
2. Complete os campos `[PREENCHER]` e `[CONFERIR]` de `social/canais.md`.
3. (Opcional) Autorize o Canva nos conectores do claude.ai para o designer
   criar as peças. Sem ele, o designer entrega só o briefing visual.

## Como usar

### Claude Code

Os agentes estão em `.claude/agents/` e a skill em `.claude/skills/`.

- Fluxo completo: *"Use a skill producao-social para uma pauta sobre
  [tema] no LinkedIn e no site."* (ou `/producao-social [tema]`)
- Um agente só: *"Peça ao social-pesquisador para checar os dados deste
  texto: …"*
- Relatório: *"Peça ao social-analista o relatório de outubro com este CSV."*

### GitHub Copilot (VS Code)

Os agentes estão em `.github/agents/` e a skill em `.github/skills/`.
Mude o chat para o modo **Agent** e escolha o agente na lista. Ao terminar,
cada agente mostra um botão de **handoff** para passar a pauta ao próximo
(ex.: estrategista → "Pesquisar e checar dados").
Os nomes de ferramentas (`search`, `fetch`, `edit`…) podem variar conforme a
versão do VS Code. Se um agente não aparecer, veja "Custom agents missing" no
README principal.

## Regras que todos seguem

- `social/regras-de-fonte.md`: só fontes verificadas (científicas, imprensa
  de referência, consultorias reconhecidas), ficha para cada dado,
  inconsistências sempre apontadas, nada inventado.
- `social/canais.md`: limites das plataformas **com fonte e data de
  conferência**, porque eles mudam. Exemplo: o Instagram baixou o máximo de
  hashtags de 30 para 5 em dez/2025.

## Alterar um agente

Edite o texto em `social/gerar_agentes.py` e rode:

```bash
python social/gerar_agentes.py
```

Os dois formatos (`.claude/agents/` e `.github/agents/`) são regravados
juntos. Não edite os `.md` gerados à mão, ou as versões vão divergir. A skill
`producao-social` fica em duas cópias; se mudar uma, copie para a outra.

## Onde ficam as entregas

```
social/entregas/
  2026-11-20-confianca-na-imprensa/
    briefing.md  fontes.md  site.md  linkedin.md  instagram.md  visual.md
  calendario-2026-12.md
  relatorio-2026-11.md
```
