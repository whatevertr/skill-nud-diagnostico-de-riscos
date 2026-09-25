<p align="right"><a href="README.pt-BR.md">🇧🇷 Português</a></p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-night.png">
  <img alt="nud-diagnostico-de-riscos — a SIPOC-R inventory into a consolidated risks and opportunities diagnosis" src="assets/banner-day.png">
</picture>

# nud-diagnostico-de-riscos

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

A **skill for Claude** (Anthropic) that starts from a SIPOC-R Process Inventory and produces the **consolidated risk analysis**: prioritized matrix, root cause, pairing with mitigations and an **executive view**. It is the analytical counterpart of **[nud-inventario-processos](https://github.com/whatevertr/skill-nud-inventario-processos)**.

Part of the **NUD | Constellation Method**, by Thainá Ramos.

> **Compatibility:** packaged as a **Claude Skill** (Anthropic's Agent Skills format — it triggers on its own in Claude Code / claude.ai). The **method is model-agnostic**: the same content works in **any chat LLM** by pasting `SKILL.md` + `references/` as context, and `builder.py` runs on **any Python** (e.g. ChatGPT's Code Interpreter).

---

## What it does

It covers everything the base skill **nud-inventario-processos** does (building the inventory) and adds:

- **"Risks and Opportunities Summary" tab** — the inventory's risks consolidated, with level, classification, impact type and **action priority**.
- **"Legends" tab** — the criteria for level, classification and priority, **defined according to the process context** (not fixed) and documented in the file itself.
- Clustering, prioritization and **root-cause** identification of the risks.
- Pairing each risk with its matching **mitigation**.

When you only need the map (without the risk analysis), use the base skill **[nud-inventario-processos](https://github.com/whatevertr/skill-nud-inventario-processos)**.

## Structure

```
nud-diagnostico-de-riscos/
├── SKILL.md                         # skill instructions
├── assets/
│   ├── Modelo_Inventario_Processos.xlsx   # base model the builder seeds from (Phase 5)
│   └── Modelo_Diagnostico_Riscos.xlsx     # example of the full delivery: 4 tabs (Inventory + Summary + Premises + Legends)
├── references/                      # technique, mapping, inference, builder, risk summary, legends
└── scripts/
    └── builder.py
```

## Install

Copy the `nud-diagnostico-de-riscos/` folder into your Claude skills directory (`.claude/skills/`) and the skill starts triggering on the cues described in `SKILL.md`.

## Example

`Modelo_Diagnostico_Riscos.xlsx` ships a fictional example — **"Loja Aurora"** — with the four tabs filled in, so you can see the full delivery (Inventory + **Risks and Opportunities Summary** + Premises + **Legends**) before running it with your own inventory.

## License

[CC-BY-4.0](LICENSE). Free to use, with attribution.

---

*NUD (Constellation Method) — a method by Thainá Ramos (Nud by Whatevertr) · <https://github.com/whatevertr> · Licensed under CC-BY-4.0.*
