# Fase 7 — Construir a aba "Legendas"

Esta reference detalha como construir a aba "Legendas" que documenta os critérios efetivamente usados na aba "Resumo Riscos e Oportunidades".

## Por que esta aba existe

A aba Legendas é a **memória dos critérios** usados na análise. Sem ela, qualquer pessoa que abra a planilha depois (ou o próprio autor, 3 meses depois) não consegue:

- Entender por que um risco foi classificado como Alto e outro como Médio.
- Reproduzir a lógica para classificar novos riscos no futuro.
- Auditar a coerência das classificações.

Por isso, **tudo que foi usado para classificar precisa ficar escrito ali**. Critérios genéricos não servem — o conteúdo precisa refletir a realidade do contexto analisado.

## Princípio fundamental: critérios contextuais

A skill **não traz critérios prontos**. Cada inventário tem sua régua. Exemplos do que muda:

| Contexto do inventário | O que ancora "Alto" |
|---|---|
| Onboarding de pessoas | Exposição CLT/LGPD direta, perda concreta de candidato |
| Backoffice financeiro | Perda financeira material, exposição fiscal/contábil |
| Produção / chão-de-fábrica | SST, acidente, parada de linha, NR violada |
| TI / segurança | Incidente de segurança, indisponibilidade, perda de dado |
| Atendimento ao cliente | Reclamação grave, perda de cliente, dano de imagem |
| Compliance / Jurídico | Risco regulatório, exposição em processo |

A pessoa que executa a skill **deduz a régua do conjunto de riscos coletados** e a documenta na aba Legendas. Não é criatividade — é leitura do que está ali.

## Layout visual (idêntico à aba Premissas)

A aba Legendas usa **exatamente o mesmo formato visual** da aba Premissas do modelo:

| Elemento | Estilo |
|---|---|
| Título (linha 1, col A) | Consolas 12 bold, texto `F4EBE2`, fill grafite `2C233D` |
| Cabeçalho de seção (col A + col B na mesma linha) | Consolas 10 bold, texto `191128`, fill painel `D8CDC2` |
| Chave (col A, linhas de dado) | Consolas 10 bold, sem fill |
| Valor (col B, linhas de dado) | Consolas 10 regular, sem fill |
| Alinhamento das linhas de dado | `wrap_text=True`, `vertical=top` |
| Larguras | A=32, B=95 |
| Gridlines | Ocultas |

Não usar cores adicionais, não inserir bordas, não usar formatação condicional. O visual tem que ser indistinguível da aba Premissas.

## Estrutura mínima (7 seções)

A ordem e nomes das seções devem ser preservados para consistência entre inventários. O **conteúdo** de cada seção é específico ao contexto.

### Seção 1 — Sobre estas legendas

Itens fixos:
- **Propósito** — frase explicando que esta aba documenta os critérios usados na aba Resumo.
- **Origem dos critérios** — frase deixando claro que os critérios foram definidos conforme a realidade do(s) processo(s) analisado(s), e que NÃO devem ser copiados cegamente para inventários de outras áreas.
- **Atualização** — regra: quando o critério mudar, atualizar esta aba primeiro e depois reavaliar as linhas afetadas no Resumo.

### Seção 2 — Nível do Risco (coluna C)

Definir Alto / Médio / Baixo **com texto específico ao contexto**. Cada definição em 1-2 frases concretas.

Exemplo para inventário de onboarding:
- **Alto** — exposição legal direta (CLT/LGPD), perda concreta de candidato ou trava a cadeia inteira.
- **Médio** — afeta a experiência, gera retrabalho relevante ou atraso na cadeia, mas é contornável.
- **Baixo** — custo localizado ou pontual; impacto restrito a um processo.

Acrescentar item:
- **Regra de cor** — a coluna C tem formatação condicional automática: Alto = coral, Médio = amarelo, Baixo = verde (Farol NUD). Ao editar o texto, a cor se ajusta sozinha.

### Seção 3 — Classificação do Risco (coluna D)

Listar as categorias usadas neste inventário e o que cada uma significa **neste contexto**. Não copiar lista universal; trazer apenas as categorias que realmente apareceram nas linhas do Resumo.

Categorias comuns (selecionar e adaptar):
- **Conformidade** — risco de descumprimento de lei, norma ou regulamento. Tem exposição legal.
- **Operacional** — erro humano, falha de sistema, retrabalho, dependência manual.
- **Qualidade** — informação incorreta, divergência entre bases, dado errado propagado.
- **Prazo** — atraso, fila, perda de janela logística.
- **Comunicação** — informação que não chega, mensagens perdidas.
- **Reputacional** — imagem, perda de cliente/candidato.
- **Custo** — desperdício, custo desnecessário.
- **Financeiro** — perda financeira material direta.
- **SST** (em produção) — risco à saúde e segurança do trabalhador.
- **Segurança de Dados** (em TI) — risco de incidente, vazamento, indisponibilidade.

Cada categoria que aparece no Resumo deve estar documentada aqui. Categoria que não aparece, não documentar.

### Seção 4 — Tipo de Impacto (coluna G)

Documentar:
- **Formato** — texto nominal, categorias separadas por " + ". Causa-raiz entre parênteses no final quando aplicável.
- **Exemplo 1** — um exemplo real retirado do Resumo, com tradução.
- **Exemplo 2** — outro exemplo real, dessa vez com causa-raiz entre parênteses.
- **Causas-raiz reconhecidas** — listar as causas-raiz estruturais que emergiram do diagnóstico (se houver). Cada uma com 2-5 palavras (ex.: "Sequenciamento tardio · Dados de origem inconsistentes · Canais não integrados").

Se o diagnóstico não identificou causas-raiz, simplificar: dizer "Neste inventário não foram identificadas causas-raiz estruturais; o campo traz apenas as dimensões do impacto."

### Seção 5 — Prioridade de Atuação (coluna H)

Definir P1, P2, P3, P4 **neste contexto**, com 1-2 frases cada.

Padrão (ajustável):
- **P1 Crítica** — risco material ou estrutural com exposição legal direta OU manifestação direta de uma causa-raiz com impacto material. Atacar primeiro.
- **P2 Alta** — afeta diretamente a experiência ou trava o processo, mesmo sem exposição legal.
- **P3 Média** — operacional contornável.
- **P4 Baixa** — pontual e restrito; atacar quando os anteriores estiverem encaminhados.

Acrescentar item crítico:
- **Diferença Nível × Prioridade** — frase explicando que nem todo Alto vira P1 e nem todo Médio vira P2, porque a Prioridade considera também se o risco ataca causa-raiz estrutural. Sem essa nota, leitor confunde as duas colunas.

### Seção 6 — Códigos de identificação (coluna A — R-XX)

Documentar:
- **Formato** — R-XX, numeração sequencial.
- **Estabilidade** — o ID é fixo; reordenar/filtrar não muda. É a chave para citar o risco em reuniões e documentos.
- **Referência cruzada** — quando uma mitigação atende mais de um risco, a referência aparece como "(mitigação compartilhada com R-XX)".

### Seção 7 — Os processos do inventário (referência rápida)

Listar os processos cobertos pelo inventário, no formato:
- `(1)` → nome completo do processo 1
- `(2)` → nome completo do processo 2
- ... e assim por diante.

Acrescentar item:
- **Como aparecem no Resumo** — a coluna F usa o formato `(N) Nome completo do processo`. Múltiplos processos aparecem em linhas separadas dentro da mesma célula.

## Posicionamento da aba

A aba Legendas vai **por último** no arquivo, depois de Premissas. Ordem final do arquivo:

1. Inventário de Processos
2. Resumo Riscos e Oportunidades
3. Premissas
4. **Legendas**

## Anti-padrões

- ❌ Copiar a aba Legendas de outro inventário sem revisar. Cada inventário tem critérios próprios.
- ❌ Deixar definições genéricas tipo "Alto = grave". Tem que dizer o que é "grave" naquele contexto.
- ❌ Documentar uma categoria que não aparece em nenhuma linha do Resumo.
- ❌ Esquecer a nota "Diferença Nível × Prioridade" — ela é o que evita interpretação errada das duas colunas.
- ❌ Inserir cores, bordas ou estilos diferentes do padrão Premissas. O visual deve ser idêntico.

## Validação final

Antes de entregar, conferir:

1. As definições de Nível, Classificação, Tipo de Impacto e Prioridade refletem o que de fato foi aplicado no Resumo (passar olho linha a linha).
2. Toda categoria usada na coluna D (Classificação) do Resumo está documentada na Seção 3.
3. Toda causa-raiz citada entre parênteses na coluna G (Tipo de Impacto) está listada na Seção 4.
4. A listagem de processos da Seção 7 corresponde 1:1 ao que está no Inventário.
5. O visual é indistinguível da aba Premissas (zoom out lado a lado).
