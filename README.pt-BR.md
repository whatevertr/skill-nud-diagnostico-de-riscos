<p align="right"><a href="README.md">🇺🇸 English</a></p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-night.png">
  <img alt="nud-diagnostico-de-riscos — de um inventário SIPOC-R ao diagnóstico consolidado de riscos e oportunidades" src="assets/banner-day.png">
</picture>

# nud-diagnóstico-de-riscos

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

Uma **skill para Claude** (Anthropic) que parte de um Inventário de Processos SIPOC-R e produz a
**análise consolidada de riscos**: matriz priorizada, causa-raiz, pareamento com mitigações e
**visão executiva**. É o par analítico da skill **[nud-inventário-processos](https://github.com/whatevertr/skill-nud-inventario-processos)**.

Faz parte do **NUD | Constellation Method**, de Thainá Ramos.

> **Compatibilidade:** empacotada como **Claude Skill** (formato Agent Skills da Anthropic — aciona sozinha no Claude Code / claude.ai). O **método é agnóstico de modelo**: o mesmo conteúdo funciona em **qualquer LLM de chat** colando o `SKILL.md` + `references/` como contexto, e o `builder.py` roda em **qualquer Python** (ex.: Code Interpreter do ChatGPT).

---

## O que ela faz

Engloba tudo o que a skill base **nud-inventário-processos** faz (montar o inventário) e acrescenta:

- **Aba "Resumo de Riscos e Oportunidades"** — os riscos do inventário consolidados, com nível,
  classificação, tipo de impacto e **prioridade de atuação**.
- **Aba "Legendas"** — os critérios de nível, classificação e prioridade, **definidos conforme o
  contexto do processo** (não são fixos) e documentados no próprio arquivo.
- Clusterização, priorização e identificação de **causa-raiz** dos riscos.
- Pareamento de cada risco com a **mitigação** correspondente.

Quando usar só o mapa (sem a análise de risco), use a skill base
**[nud-inventário-processos](https://github.com/whatevertr/skill-nud-inventario-processos)**.

## Estrutura

```
nud-diagnostico-de-riscos/
├── SKILL.md                         # instruções da skill
├── assets/
│   ├── Modelo_Inventario_Processos.xlsx   # molde-base que o builder semeia (Fase 5)
│   └── Modelo_Diagnostico_Riscos.xlsx     # exemplo da entrega: 4 abas (Inventário + Resumo + Premissas + Legendas)
├── references/                      # técnica, mapeamento, inferência, builder, resumo de riscos, legendas
└── scripts/
    └── builder.py
```

## Como instalar

Copie a pasta `nud-diagnostico-de-riscos/` para o diretório de skills do seu Claude
(`.claude/skills/`) e a skill passa a ser acionada pelos gatilhos descritos no `SKILL.md`.

## Exemplo

O `Modelo_Diagnostico_Riscos.xlsx` traz um exemplo fictício — **"Loja Aurora"** — com as quatro
abas preenchidas, para você ver a entrega completa (Inventário + **Resumo de Riscos e
Oportunidades** + Premissas + **Legendas**) antes de rodar com o seu próprio inventário.

## Licença

[CC-BY-4.0](LICENSE). Uso livre, com atribuição.

---

*NUD (Constellation Method) — método de Thainá Ramos (Nud by Whatevertr) · <https://github.com/whatevertr> · Licenciado sob CC-BY-4.0.*
