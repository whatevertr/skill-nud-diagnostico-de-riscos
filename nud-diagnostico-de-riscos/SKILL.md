---
name: nud-diagnostico-de-riscos
description: "Versão estendida da skill de Inventário de Processos SIPOC-R. Use SEMPRE que o usuário pedir um inventário COM análise consolidada de riscos, ou pedir explicitamente as abas 'Resumo Riscos e Oportunidades' e 'Legendas', ou pedir clusterização/priorização/classificação de riscos, identificação de causas-raiz, ou visão executiva dos riscos. Acione também quando o usuário fornecer um inventário SIPOC-R preenchido e pedir 'consolidar riscos', 'priorizar', 'parear com mitigações', 'matriz de riscos', 'tabela de riscos com prioridade', 'visão executiva', ou expressões equivalentes. Engloba tudo o que a skill base 'nud-inventario-processos' faz (Fases 1-5) e adiciona Fases 6-7 que produzem as abas 'Resumo Riscos e Oportunidades' e 'Legendas' no padrão visual da aba Premissas. Critérios de nível de risco, classificação, tipo de impacto e prioridade NÃO são fixos — definidos conforme o contexto do processo analisado e documentados na aba Legendas do arquivo entregue."
license: CC-BY-4.0
---

# Inventário de Processos — Versão Especialista

Esta skill é a **versão estendida** da skill `inventario-processos`. Tudo o que a skill base faz, esta skill faz também — e adiciona duas etapas finais de consolidação executiva: as abas **Resumo Riscos e Oportunidades** e **Legendas**.

Use esta skill quando o usuário quer não só o inventário, mas também a leitura consolidada dos riscos do inventário (clusterização, classificação, pareamento com oportunidades de mitigação, priorização) e a documentação dos critérios usados.

## O que esta skill produz a mais

Ao final, o arquivo `.xlsx` entregue tem **4 abas** (em vez de 2):

1. **Inventário de Processos** — igual à skill base (modelo SIPOC-R, 16 colunas, intocado — a coluna "Controle / Mitigação" foi removida na v3; a mitigação virou a oportunidade simétrica). **SIPOC-R = SIPOC + Riscos** (extensão de Riscos do NUD; não é o "R" de *Requirements*).
2. **Resumo Riscos e Oportunidades** — nova aba, executiva, com uma linha por risco, suas oportunidades pareadas como ação de mitigação, processos impactados, classificação, tipo de impacto e prioridade.
3. **Premissas** — igual à skill base.
4. **Legendas** — nova aba, no mesmo layout visual da aba Premissas, documentando todos os critérios usados na aba Resumo (níveis de risco, classificações, tipos de impacto, prioridades, IDs, processos).

## Princípios desta versão (além dos da skill base)

Os 6 princípios inegociáveis da skill `inventario-processos` continuam valendo na íntegra. Esta skill adiciona mais 4:

7. **Critérios são contextuais — nunca herdados.** Os critérios de nível de risco (Alto/Médio/Baixo), classificação do risco (Operacional, Conformidade, Qualidade, etc.), tipo de impacto e prioridade de atuação **dependem da realidade do processo analisado**. Não há um conjunto universal. Exemplos do que muda por contexto:
   - Em onboarding de pessoas: "Alto" inclui exposição CLT/LGPD direta e perda de candidato.
   - Em backoffice financeiro: "Alto" provavelmente inclui perda financeira material e exposição fiscal/contábil.
   - Em produção/operação: "Alto" provavelmente inclui SST, acidente, parada de linha.
   - Em TI/segurança: "Alto" provavelmente inclui incidente de segurança, indisponibilidade, perda de dado.

   A skill NÃO traz critérios prontos. A skill traz a **estrutura** que será preenchida com critérios extraídos do contexto. Isso vale para classificação (categorias do risco), tipo de impacto (dimensões observadas no processo), e prioridade (níveis P1..P4).

8. **A aba Legendas é a memória dos critérios.** Tudo que foi usado para classificar precisa ficar escrito ali. Quem abrir a planilha sem ter participado da análise tem que conseguir entender como cada coluna foi preenchida e reproduzir a lógica. Se um critério mudou no meio da análise, atualizar a aba Legendas primeiro e depois reavaliar as linhas afetadas.

9. **A aba Legendas segue o layout visual da aba Premissas.** Mesma tipografia, mesma estrutura de seções com cabeçalho painel (`D8CDC2`) e título grafite (`2C233D`), mesmas larguras (A=32, B=95), sem gridlines. Isso é por consistência visual com o modelo.

10. **Pareamento risco↔oportunidade na linha do risco.** No Resumo, uma linha = um risco. As oportunidades que mitigam aquele risco vão **todas juntas** na coluna de mitigação, começando pela **oportunidade de ID simétrico** (R01 é mitigado por O01 — ver `inferencia.md` §3.0) e depois as demais/compartilhadas, numeradas 1, 2, 3... Quando uma mitigação atende mais de um risco, marcar como "(mitigação compartilhada com R-XX)" para evidenciar a economia de esforço.

## Fluxo de trabalho (7 fases)

As Fases 1 a 5 são idênticas à skill base (`inventario-processos`). Consulte o SKILL.md daquela skill para detalhes; o resumo está abaixo.

### Fase 1 — Identificar insumos e modo (NOVO vs INCREMENTO)
Igual à skill base. Detectar se o usuário anexou inventário em uso (modo INCREMENTO) ou está começando do zero (modo NOVO). Inclui também a decisão do **nível de granularidade (N1/N2/N3)**, sempre perguntada ao usuário com sugestão — ver «Nível de granularidade do inventário» na skill base.

### Fase 2 — Ler e extrair conteúdo dos insumos
Igual à skill base. Cada formato (.pptx, .docx, .pdf, transcrição, anotação) tem seu caminho de leitura — ver `references/leitura_insumos.md`.

### Fase 3 — Analisar com técnica de processos
Igual à skill base. Separar as linhas aplicando os critérios de granularidade conforme o **nível escolhido (N1/N2/N3)** — em N1 por gatilho/cliente/saída; em N2 por **segmento entre handoffs** (cada troca do posto responsável; um posto que reentra com outros no meio = mais de uma linha; **automação autônoma é posto e gera handoff**; **ramo de exceção corta por handoff, não vira linha genérica**; **declarar escopo incluído/excluído** para não puxar fluxo tangencial); em N3 por **função/automação** (nunca por pessoa-indivíduo). Ver «Nível de granularidade do inventário» na base e `references/tecnica_processos.md` §3B. Detalhes também em `references/mapeamento_campos.md`.

### Fase 4 — Inferir Legislação, Riscos e Oportunidades no inventário
Igual à skill base. Varredura de riscos por categoria (inspirada em FMEA, só severidade), regras conservadoras para legislação, melhorias típicas para oportunidades. Origem marcada pela COR (laranja = inferido) e IDs contínuos (E01, R01, O01), com 🍷 para repetição. Detalhes em `references/inferencia.md`.

### Fase 5 — Gerar o arquivo base (Inventário + Premissas)
Igual à skill base. Usar `scripts/builder.py`. Após esta fase, o arquivo tem 2 abas (Inventário e Premissas) — o mesmo entregável da skill base.

**Checkpoint da Fase 5:** se o usuário pediu apenas o inventário, a entrega termina aqui. Se o usuário pediu inventário **+ visão consolidada/clusterizada/priorizada de riscos**, ou explicitamente as abas Resumo/Legendas, ou se a skill detectou pelos sinais do pedido que essa é a expectativa, prossiga para Fase 6.

### Fase 6 — Construir a aba "Resumo Riscos e Oportunidades"

Esta é a primeira fase nova. Detalhes em `references/resumo_riscos.md`.

Resumo do que a Fase 6 faz:

1. **Ler todos os riscos do inventário** (coluna "Riscos") e todas as oportunidades (coluna "Oportunidades") de TODAS as linhas, mantendo qual processo origina cada item.

2. **Clusterizar riscos parecidos.** Quando o mesmo risco aparece em processos diferentes ou com pequenas variações de redação, agrupar em um único item. Cada cluster vira uma linha do Resumo.

3. **Reusar o ID da aba Inventário (R0x).** A Fase 6 NÃO renumera — usa o mesmo `R01, R02…` já atribuído no inventário. O ID é a chave de conciliação entre as abas ("ver R08"); risco que se repetiu em várias etapas já entrou com ID único (e 🍷) na Fase 4.

4. **Parear cada risco com suas oportunidades de mitigação.** Para cada cluster de risco, listar TODAS as oportunidades (do inventário e/ou inferidas) que atacam aquele risco. Várias oportunidades por risco é o esperado. Numerar com `1)`, `2)`, `3)`... dentro da célula. Quando uma oportunidade ataca mais de um risco, marcar "(mitigação compartilhada com R-XX)".

5. **Preencher as 8 colunas do Resumo:**
   - `A — ID` (R01, R02... — o mesmo ID já atribuído na aba Inventário; a Fase 6 REUSA, não renumera)
   - `B — Risco` (texto curto, claro, padronizado)
   - `C — Nível do Risco` (Alto/Médio/Baixo — com formatação condicional de cor automática)
   - `D — Classificação do risco` (categoria nominal — ver Fase 7 para definir as categorias do contexto)
   - `E — Oportunidade / Ação de mitigação` (lista numerada)
   - `F — Processos impactados` (formato `(N) Nome completo do processo`, um por linha dentro da célula)
   - `G — Tipo de impacto` (texto nominal, categorias separadas por " + "; causa-raiz entre parênteses quando aplicável)
   - `H — Prioridade de atuação` (P1 Crítica / P2 Alta / P3 Média / P4 Baixa — com fundo colorido)

6. **Ordenar por prioridade** (P1 → P4) preservando os IDs.

7. **Aplicar formatação condicional** na coluna `C` (Nível do Risco):
   - Alto → fill `A32B1C` (coral) + texto `F4EBE2`
   - Médio → fill `C9A21F` (amarelo) + texto `4A3A00`
   - Baixo → fill `2F7A4E` (verde) + texto `F4EBE2`

8. **Aplicar fundo fixo** na coluna `H` (Prioridade):
   - P1 Crítica → `A32B1C` (coral), P2 Alta → `993700` (laranja), P3 Média → `C9A21F` (amarelo, texto escuro `4A3A00`), P4 Baixa → `6B657A` (cinza); demais com texto claro `F4EBE2` bold.

**Critério para Prioridade — definir com base no contexto:** a regra geral é "ataca causa-raiz estrutural + gravidade do risco". O que conta como causa-raiz e o que conta como gravidade depende do tipo de processo analisado. A skill **não traz** uma régua pronta — a régua é construída na análise e registrada na aba Legendas (Fase 7).

### Fase 7 — Construir a aba "Legendas"

Esta é a segunda fase nova. Detalhes em `references/legendas.md`.

Resumo do que a Fase 7 faz:

A aba "Legendas" documenta **os critérios efetivamente usados** na Fase 6. Layout visual idêntico à aba Premissas: título grafite `2C233D` size 12 bold (texto claro), seções com fill painel `D8CDC2` em ambas as colunas, linhas de dado A bold size 10 / B size 10, larguras A=32 B=95, sem gridlines.

Estrutura mínima da aba (7 seções):

1. **Sobre estas legendas** — propósito, origem dos critérios (contextual ao inventário), regra de atualização.
2. **Nível do Risco (coluna C)** — definição de Alto / Médio / Baixo **conforme o tipo de processo analisado**, e nota sobre a formatação condicional automática.
3. **Classificação do Risco (coluna D)** — quais categorias foram usadas (Operacional, Conformidade, Qualidade, Prazo, Comunicação, Reputacional, Custo, etc.) e o que cada uma significa **neste inventário**.
4. **Tipo de Impacto (coluna G)** — formato (categorias com " + "), regra de uso de causas-raiz entre parênteses, exemplos retirados da própria análise.
5. **Prioridade de Atuação (coluna H)** — definição de P1, P2, P3, P4 **neste contexto**, e nota explicando por que Nível ≠ Prioridade (Nível mede gravidade isolada do risco; Prioridade considera também se o risco ataca causa-raiz).
6. **Códigos R-XX (coluna A)** — formato e estabilidade do ID, regra de referência cruzada.
7. **Os processos do inventário (referência rápida)** — listagem `(N) Nome completo` dos processos cobertos, e nota de como aparecem no Resumo.

**Regra crítica:** os textos de cada seção devem ser preenchidos com a lógica **realmente aplicada** naquele inventário. Não copiar genericamente. Se neste inventário "Alto" passou a incluir "perda concreta de candidato", a aba Legendas tem que dizer isso explicitamente.

## Critérios contextuais — orientação prática

Como decidir os critérios para cada inventário:

**Para definir Nível do Risco (Alto/Médio/Baixo):**
- Olhar o conjunto de riscos coletados. Identificar a pior consequência observável no domínio (exposição legal? perda financeira material? acidente? indisponibilidade?). Essa consequência ancora "Alto".
- "Baixo" ancora no risco mais leve observado (custo pontual, retrabalho de 1 pessoa, incômodo restrito).
- "Médio" é o que sobra entre os dois.

**Para definir Classificação do Risco (categorias):**
- Categorias clássicas: Operacional, Conformidade, Qualidade, Prazo, Comunicação, Reputacional, Custo, Financeiro.
- Acrescentar categorias específicas do domínio quando relevante: SST (em produção), Segurança de Dados (em TI), Fiscal (em contábil), etc.
- Não inventar categoria nova para um único risco — agregar.

**Para definir Tipo de Impacto:**
- É a soma das dimensões afetadas (Operacional + Reputacional, Prazo + Conformidade...).
- Quando o diagnóstico identificar causas-raiz estruturais, anotá-las entre parênteses no fim (ex.: "(Sequenciamento tardio)"). Isso conecta o risco isolado a um padrão maior.

**Para definir Prioridade de Atuação:**
- A regra geral é: gravidade do risco + ataque a causa-raiz = prioridade.
- P1 Crítica costuma ser: exposição legal direta OU manifestação de causa-raiz com impacto material.
- P2 Alta: afeta experiência/cliente diretamente OU trava o processo.
- P3 Média: operacional contornável.
- P4 Baixa: pontual e restrito.
- Esses textos são pontos de partida — ajustar à realidade do processo.

## Anti-padrões adicionais desta versão

Além dos anti-padrões da skill base, evitar:

- ❌ **Copiar critérios prontos de um inventário anterior** sem reavaliar se cabem no contexto novo. Cada inventário tem sua régua.
- ❌ **Deixar a aba Legendas com texto genérico.** Cada definição deve refletir o que de fato foi aplicado nas linhas do Resumo.
- ❌ **Reordenar o Resumo destruindo o ID.** Os R-XX são estáveis; ordenar por prioridade muda a ordem visual das linhas mas mantém o ID que cada risco recebeu na primeira numeração.
- ❌ **Misturar formatação condicional com fundo fixo na mesma coluna.** Nível do Risco usa formatação condicional (cor sai do texto). Prioridade usa fill fixo (texto e fill são gravados em conjunto).
- ❌ **Mais de 1 risco por linha do Resumo.** Se um cluster ficou grande demais, dividir em dois clusters — não consolidar.
- ❌ **Esquecer de mover a aba Legendas para o final** (depois de Premissas). Ordem das abas: Inventário → Resumo → Premissas → Legendas.

## Quando pedir confirmação ao usuário

Além dos pontos de checkpoint da skill base, parar e perguntar quando:

1. **A escala de Nível do Risco não está clara para o contexto.** Mostrar a proposta de Alto/Médio/Baixo e pedir validação antes de classificar 20+ riscos.
2. **As causas-raiz não emergem espontaneamente da análise.** Não inventá-las só para preencher a coluna "Tipo de Impacto". Se forem 3-4 causas estruturais nítidas, registrá-las. Se não, deixar a Prioridade ancorada só na gravidade e explicitar isso na aba Legendas.
3. **Conflito Nível × Prioridade em mais de 30% das linhas.** Se quase todo risco Médio virou P1, a régua de Prioridade está frouxa — recalibrar com o usuário.

## Resumo da entrega

Toda execução desta skill termina com:

1. Arquivo `.xlsx` em `/mnt/user-data/outputs/` com 4 abas (Inventário, Resumo Riscos e Oportunidades, Premissas, Legendas), apresentado via `present_files`.
2. Resumo curto em texto: quantos processos no inventário, quantos riscos consolidados no Resumo, distribuição por prioridade (quantos P1, P2, P3, P4), e quais inferências (em laranja / com 🍷) ficaram para validação.

**Recado obrigatório:** ⚠️ Tudo em LARANJA é inferência da IA e tudo com 🍷 é repetição de ID inferida — precisam de conferência humana. A aba Resumo, com as oportunidades e a ordem de criticidade, **pode ser usada como base para um plano de ação estruturado**.
3. Recomendação de próximos passos: validar a aba Legendas (é a primeira coisa que precisa ser revisada pelo usuário), revisar os P1 (ações mais urgentes), e ajustar mitigações compartilhadas.

## Documentos de referência

Esta skill usa os mesmos arquivos de referência da skill base (já presentes em `references/`) e adiciona dois novos:

- `references/tecnica_processos.md` — herdado da skill base (Fase 3)
- `references/mapeamento_campos.md` — herdado da skill base (Fase 3)
- `references/leitura_insumos.md` — herdado da skill base (Fase 2)
- `references/inferencia.md` — herdado da skill base (Fase 4)
- `references/guia_riscos_criticidade.md` — herdado da skill base: tipo de risco × criticidade, matriz Probabilidade × Impacto (apoio às Fases 4, 6 e 7; os critérios finais são contextuais, ver Princípio 7)
- `references/builder.md` — herdado da skill base (Fase 5)
- **`references/resumo_riscos.md`** — NOVO, detalhes da Fase 6 (construção do Resumo)
- **`references/legendas.md`** — NOVO, detalhes da Fase 7 (construção da aba Legendas)
- `assets/Modelo_Inventario_Processos.xlsx` — molde-base do inventário que o `builder.py` semeia na Fase 5 (herdado da skill base; linhas 1-5 preservadas, dados a partir da linha 6)
- `assets/Modelo_Diagnostico_Riscos.xlsx` — exemplo da **entrega completa**: as 4 abas (Inventário + Resumo Riscos e Oportunidades + Premissas + Legendas) com dados fictícios ("Loja Aurora") para ilustrar o resultado final da skill
