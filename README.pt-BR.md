<p align="right"><a href="README.md">🇺🇸 English</a></p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-night.png">
  <img alt="whatevertr-diagnostico-de-riscos — de um inventário SIPOC-R à análise consolidada de riscos e oportunidades" src="assets/banner-day.png">
</picture>

# whatevertr-diagnóstico-de-riscos

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

Esta é uma **skill que eu fiz para o Claude** (Anthropic) que parte de um Inventário de Processos SIPOC-R e produz a **análise consolidada de riscos e oportunidades**: matriz priorizada, pareamento com mitigações e **visão executiva**. É o par analítico da skill **[whatevertr-inventário-processos](https://github.com/whatevertr/skill-whatevertr-inventario-processos)** — fiz as duas para o meu próprio trabalho de processos e uso juntas.

Faz parte do **NUD | Constellation Method**, de Thainá Ramos.

> **Como eu uso & compatibilidade:** empacotei como **Claude Skill** (formato Agent Skills da Anthropic, então aciona sozinha no Claude Code / claude.ai). É **projetada para ser agnóstica de modelo** — o método é só `SKILL.md` + `references/`, então também colo como contexto em outros LLMs de chat, e o `builder.py` é Python puro. Tudo que precisa pra instalar e rodar está neste repositório, e eu sigo melhorando isso pra ficar fácil de pegar.
>
> **Sobre evidência, com honestidade:** o que eu garanto é o meu uso — funciona pra mim. Você consegue reproduzir a saída a partir do repositório. O quanto o *método* generaliza além dos meus casos é algo que eu ainda estou aprendendo, e eu ia adorar teu retorno se você testar.

---

## O que ela faz

Engloba tudo o que a skill base **whatevertr-inventário-processos** faz (montar o inventário) e acrescenta:

- **Aba "Resumo de Riscos e Oportunidades"** — os riscos do inventário consolidados, com nível,
  classificação, tipo de impacto e **prioridade de atuação**.
- **Aba "Legendas"** — os critérios de nível, classificação e prioridade, **definidos conforme o
  contexto do processo** (não são fixos) e documentados no próprio arquivo.
- Clusterização e priorização dos riscos.
- Pareamento de cada risco com a **oportunidade de melhoria** correspondente.

Quando usar só o mapa (sem a análise de risco), use a skill base
**[whatevertr-inventário-processos](https://github.com/whatevertr/skill-whatevertr-inventario-processos)**.

## Estrutura

```
whatevertr-diagnostico-de-riscos/
├── SKILL.md                         # instruções da skill
├── assets/
│   ├── Modelo_Inventario_Processos.xlsx   # molde-base que o builder semeia (Fase 5)
│   └── Modelo_Diagnostico_Riscos.xlsx     # exemplo da entrega: 4 abas (Inventário + Resumo + Premissas + Legendas)
├── references/                      # técnica, mapeamento, inferência, builder, resumo de riscos, legendas
└── scripts/
    └── builder.py
```

## Como instalar

Copie a pasta `whatevertr-diagnostico-de-riscos/` para o diretório de skills do seu Claude
(`.claude/skills/`) e a skill passa a ser acionada pelos gatilhos descritos no `SKILL.md`.

## Exemplo

O `Modelo_Diagnostico_Riscos.xlsx` traz um exemplo fictício — **"Loja Aurora"** — com as quatro
abas preenchidas, para você ver a entrega completa (Inventário + **Resumo de Riscos e
Oportunidades** + Premissas + **Legendas**) antes de rodar com o seu próprio inventário.

## Licença

[CC-BY-4.0](LICENSE). Uso livre, com atribuição.

---

*NUD (Constellation Method) — método de Thainá Ramos (Nud by Whatevertr) · <https://github.com/whatevertr> · Licenciado sob CC-BY-4.0.*
