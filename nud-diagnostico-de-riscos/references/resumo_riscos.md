# Fase 6 — Construir a aba "Resumo Riscos e Oportunidades"

Esta reference detalha como construir a aba de Resumo Riscos e Oportunidades a partir do inventário SIPOC-R já preenchido (Fase 5 concluída).

## Visão geral

A aba Resumo é a leitura **executiva** do inventário. Enquanto o Inventário traz a visão analítica (cada risco e oportunidade no contexto do seu processo), o Resumo consolida a visão transversal: quais são os riscos do conjunto, agrupados, classificados e priorizados para ação.

Formato: tabela com 8 colunas, uma linha por risco (cluster).

## Estrutura das 8 colunas

| Letra | Coluna | Conteúdo | Formato |
|---|---|---|---|
| A | ID | Identificador estável do risco | `R01`, `R02`, ... (os mesmos da aba Inventario — REUSA, nao renumera) |
| B | Risco | Nome curto e claro do risco | Texto |
| C | Nível do Risco | Gravidade isolada | `Alto` / `Médio` / `Baixo` |
| D | Classificação do risco | Categoria nominal | Texto |
| E | Oportunidade / Ação de mitigação | Lista numerada das ações | Texto |
| F | Processos impactados | Onde o risco se manifesta | `(N) Nome completo` |
| G | Tipo de impacto | Dimensões afetadas | Texto " + " |
| H | Prioridade de atuação | Ordem de ação | `P1 Crítica` / `P2 Alta` / `P3 Média` / `P4 Baixa` |

## Passo a passo da construção

### 1. Coleta

Varrer todas as linhas do Inventário (a partir da linha 6, pulando a linha 5 de exemplo). Para cada linha:
- Extrair tudo da coluna "Riscos" (cada item, com o ID R0x que ele já tem e a cor de origem).
- Extrair tudo da coluna "Oportunidades".
- Anotar o número do processo (coluna "Código/Nº") e o nome (coluna "Nome do Processo") como **origem** de cada item.

Resultado: lista crua de riscos e oportunidades, cada um com seu processo de origem.

### 2. Clusterização de riscos

Agrupar riscos parecidos. Critérios de agrupamento:

- **Mesma causa, processos diferentes** → mesmo cluster. Ex.: "Centro de custo errado propagado" aparecendo em P1 e P4 → 1 cluster.
- **Mesmo sintoma, redação diferente** → mesmo cluster. Ex.: "Equipamento atrasa" e "TI perde janela dos Correios" → 1 cluster ("Equipamento depende do AD e perde janela logística").
- **Categorias diferentes em causa, mas mesmo padrão** → avaliar. Em dúvida, manter separados.

Cada cluster recebe um nome curto e claro (1ª pessoa do impacto, não da causa: "Início sem contrato assinado", não "Falha de processo do contrato").

### 3. Atribuição de ID estável

**Reusar** os IDs `R01, R02, ..., RNN` ja atribuidos na aba Inventario (Fase 4). A Fase 6 NAO renumera — o ID e a chave de conciliacao entre as abas. Ordenações posteriores (por prioridade, por processo) preservam o ID.

### 4. Pareamento risco ↔ oportunidades de mitigação

Para cada cluster de risco, listar TODAS as oportunidades (vindas do inventário) que atacam aquele risco. Regras:

- **Várias oportunidades por risco é o esperado** — diferentes ações podem mitigar o mesmo problema. Não escolher só uma.
- **Numerar com `1)`, `2)`, `3)`...** dentro da célula. Cada item em uma linha.
- **Oportunidade que ataca múltiplos riscos:** ela aparece em CADA risco que ataca, marcada como "(mitigacao compartilhada com R0x)" para evidenciar a economia. Ex.: uma mesma mitigacao pode aparecer em R04, R08 e R12, cada uma com nota cruzada.
- **Manter o texto original quando possível** — apenas reformular para clareza, não inventar conteúdo novo.

### 5. Classificação (coluna D)

Categorizar cada risco em uma classificação principal. Categorias típicas (escolher a mais saliente):

- **Conformidade** — descumprimento de lei, norma ou regulamento (CLT, LGPD, NRs). Tem exposição legal.
- **Operacional** — erro humano, falha de sistema, retrabalho, dependência manual.
- **Qualidade** — informação incorreta, divergência entre bases, dado errado propagado.
- **Prazo** — atraso, fila, perda de janela logística, dependência externa que estoura SLA.
- **Comunicação** — informação que não chega, canais paralelos, mensagens perdidas, falta de visibilidade.
- **Reputacional** — imagem, perda de cliente/candidato, percepção ruim.
- **Custo** — desperdício, custo desnecessário, logística reversa.
- **Financeiro** — perda financeira material direta.

Acrescentar categorias do domínio quando necessário (SST, Segurança de Dados, Fiscal, etc.). Documentar no Legendas.

### 6. Nível do Risco (coluna C)

Aplicar a régua **definida para este inventário** (ver SKILL.md, princípio 7). Padrão geral:

- **Alto** — exposição legal direta, perda material/concreta de cliente ou candidato, ou trava a cadeia inteira.
- **Médio** — afeta experiência ou gera retrabalho relevante, mas é contornável.
- **Baixo** — custo localizado ou pontual.

A coluna `C` recebe formatação condicional (construida pelo Claude nesta fase via openpyxl — nao ha builder especifico para o Resumo; ver Fase 6 do SKILL.md):
- `Alto` → fill `A32B1C` (coral) + texto `F4EBE2` (bold)
- `Médio` → fill `C9A21F` (amarelo) + texto `4A3A00` (bold)
- `Baixo` → fill `2F7A4E` (verde) + texto `F4EBE2` (bold)

A formatação é por **texto exato** — sem espaços extras, sem variação de caixa. Normalizar antes de gravar.

### 7. Processos impactados (coluna F)

Listar os processos onde o risco se manifesta, no formato `(N) Nome completo do processo`. Múltiplos processos em linhas separadas dentro da mesma célula (quebra com `\n`).

Exemplo: um risco que afeta os processos 4 e 7:
```
(4) Validar Documentação, Gerar AD e Enviar Contrato (Admissão)
(7) Realizar Integração do Colaborador (Onboarding) e Suporte Pós-Onboarding
```

**Nome completo** = o texto da coluna "Nome do Processo" do inventário, sem encurtar. A referência cruzada exige fidelidade.

### 8. Tipo de Impacto (coluna G)

Combinar as dimensões afetadas com `" + "`. Padrão:

```
{Categoria1} + {Categoria2} [ ({Causa-raiz}) ]
```

Exemplos:
- `"Conformidade + CLT Art. 2º"` — duas categorias, sem causa-raiz citada
- `"Prazo + Experiência (Sequenciamento tardio)"` — duas categorias + causa-raiz entre parênteses

A causa-raiz só entra quando o diagnóstico identificou padrões estruturais nítidos (tipicamente 3-4 causas que explicam dezenas de sintomas). Se não houver causas-raiz claras, deixar apenas as categorias.

### 9. Prioridade de Atuação (coluna H)

Atribuir P1, P2, P3 ou P4. A regra geral (ajustável por contexto):

- **P1 Crítica** — risco material/estrutural: exposição legal direta OU manifestação direta de uma causa-raiz com impacto material. "Atacar primeiro."
- **P2 Alta** — afeta diretamente a experiência ou trava o processo. "Atacar logo após os P1."
- **P3 Média** — operacional contornável. Melhoria relevante, mas o processo segue sem.
- **P4 Baixa** — pontual, restrito, custo localizado.

A coluna `H` recebe **fill fixo** (não formatação condicional):
- P1 Crítica → `A32B1C` (coral — erro do Farol)
- P2 Alta → `993700` (laranja NUD)
- P3 Média → `C9A21F` (amarelo — atenção do Farol)
- P4 Baixa → `6B657A` (cinza NUD)

Texto claro `F4EBE2`, bold, centralizado — exceto no amarelo (P3), que usa tinta escura `4A3A00`. Fonte Consolas (mono NUD).

**Observação importante:** Nível ≠ Prioridade. Um risco de Nível Médio pode virar P2 ou até P1 se for manifestação de causa-raiz estrutural. Um risco Alto pode ser P2 se já estiver coberto por mitigações em andamento. A Prioridade pondera causa-raiz + estado atual; o Nível mede só gravidade isolada.

### 10. Ordenação

Ordenar a tabela final por Prioridade (P1 → P4), depois por ID (R0x crescente). Os IDs permanecem estaveis. **A aba Resumo, com as oportunidades e a ordem de criticidade, pode ser usada como base para um plano de acao estruturado.**

## Layout visual

- **Linha 1 — Título** com fill grafite `2C233D` (alinhado aos prints executivos do diagnóstico), texto claro `F4EBE2` bold size 12, Consolas.
- **Linha 2 — Legenda da prioridade** em itálico cinza `6B657A`, explicando as 3 causas-raiz e os 4 níveis P1..P4 em uma frase.
- **Linha 3 — Cabeçalho da tabela** com fill grafite `2C233D`, texto claro `F4EBE2` bold size 10, Consolas, centralizado.
- **Linhas 4+ — Dados**, alinhamento `vertical=top`, `wrap_text=True`. Bordas finas `ABA9B3` (rule NUD).
- **Freeze panes:** `A4` (mantém título + legenda + cabeçalho visíveis).
- **Gridlines:** ocultas.

## Larguras de coluna (recomendado)

- A=7, B=32, C=14, D=14, E=60, F=36, G=22, H=14

## Posicionamento da aba

A aba "Resumo Riscos e Oportunidades" vai **imediatamente após** a aba "Inventário de Processos" e antes de "Premissas". Ordem final do arquivo:

1. Inventário de Processos
2. Resumo Riscos e Oportunidades
3. Premissas
4. Legendas (Fase 7)
