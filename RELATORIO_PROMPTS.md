# RELATORIO_PROMPTS.md

# Relatório de Uso e Avaliação de IA

## 1. Identificação

| Campo | Informação |
|---|---|
| Projeto | [Nome do projeto] |
| Data | [DD/MM/AAAA] |
| Responsável | [Nome] |
| IA utilizada | [ChatGPT / Claude / Gemini / etc.] |
| Modelo | [Nome/versão do modelo] |
| Finalidade | [Descrição objetiva da tarefa] |

---

## 2. Objetivo do Uso da IA

Descrever o que a IA foi utilizada para realizar.

Exemplo:

> A IA foi utilizada como apoio à implementação do requisito X,
> especialmente para análise do código, identificação de inconsistências
> e sugestão de correções.

A IA não foi considerada fonte normativa. As decisões finais foram
validadas em relação ao CDU e aos Critérios de Aceite definidos para
o projeto.

---

## 3. Contexto e Insumos Fornecidos à IA

Foram fornecidos à IA os seguintes elementos:

- [ ] Descrição do requisito
- [ ] CDU / regra de negócio
- [ ] Critérios de Aceite
- [ ] Código-fonte
- [ ] Estrutura do projeto
- [ ] Exemplos de entrada e saída
- [ ] Erros identificados
- [ ] Outros: [descrever]

---

## 4. Prompts Utilizados

### Prompt 01 — Análise inicial

**Objetivo:** [objetivo do prompt]

**Prompt enviado:**

> [Inserir o prompt exatamente como enviado]

**Resultado obtido:**

[Resumo da resposta ou referência ao artefato gerado.]

---

### Prompt 02 — Validação contra o CDU

**Objetivo:** verificar se a solução proposta estava de acordo com o CDU.

**Prompt enviado:**

> [Inserir o prompt exatamente como enviado]

**Resultado obtido:**

[Resumo.]

---

### Prompt 03 — Correção

**Objetivo:** corrigir os problemas identificados na resposta anterior.

**Prompt enviado:**

> [Inserir o prompt exatamente como enviado]

**Resultado obtido:**

[Resumo.]

---

## 5. Avaliação das Respostas da IA

### 5.1 Erros identificados

| ID | Resposta | Erro | Regra do CDU relacionada | Impacto | Corrigido? |
|---|---|---|---|---|---|
| E01 | Prompt 01 | [Descrição] | CDU-X | Alto | Sim |
| E02 | Prompt 01 | [Descrição] | CDU-Y | Médio | Sim |
| E03 | Prompt 02 | [Descrição] | CDU-Z | Baixo | Sim |

### 5.2 Detalhamento dos erros

#### E01 — [Nome do erro]

**O que a IA fez:**

[Descrição objetiva.]

**O que o CDU determina:**

[Regra aplicável.]

**Por que a resposta estava incorreta:**

[Explicação.]

**Correção solicitada à IA:**

> [Prompt usado para solicitar a correção]

**Resultado após a correção:**

[Descrição do resultado.]

**Validação:**

- CDU atendido: Sim/Não
- Critério de Aceite atendido: Sim/Não
- Necessitou intervenção manual: Sim/Não

---

## 6. Histórico de Correções

| Iteração | Problema | Ação solicitada | Resultado | Status |
|---|---|---|---|---|
| 1 | [Problema] | [Ação] | [Resultado] | Corrigido |
| 2 | [Problema] | [Ação] | [Resultado] | Corrigido |
| 3 | [Problema] | [Ação] | [Resultado] | Corrigido |

---

## 7. Estratégia de Correção

As correções foram conduzidas de forma iterativa:

1. Identificação do comportamento produzido pela IA.
2. Comparação da resposta com o CDU.
3. Identificação da divergência.
4. Formulação de um novo prompt explicitando a regra violada.
5. Nova geração da solução.
6. Validação contra o CDU.
7. Validação dos Critérios de Aceite.
8. Revisão manual da solução final.

---

## 8. Critérios de Aceite

| ID | Critério de Aceite | Resultado | Evidência | Status |
|---|---|---|---|---|
| CA01 | [Critério] | [Resultado observado] | [Teste/evidência] | ✅ |
| CA02 | [Critério] | [Resultado observado] | [Teste/evidência] | ✅ |
| CA03 | [Critério] | [Resultado observado] | [Teste/evidência] | ❌ |
| CA04 | [Critério] | [Resultado observado] | [Teste/evidência] | ✅ |

---

## 9. Autoavaliação

Escala:

- **5** — Atendeu completamente
- **4** — Atendeu com pequena ressalva
- **3** — Atendeu parcialmente
- **2** — Atendeu de forma insuficiente
- **1** — Não atendeu

| Critério | Nota | Justificativa |
|---|---:|---|
| Clareza da solução | 5 | [Justificativa] |
| Aderência ao CDU | 4 | [Justificativa] |
| Atendimento aos Critérios de Aceite | 5 | [Justificativa] |
| Correção técnica | 4 | [Justificativa] |
| Tratamento dos erros | 5 | [Justificativa] |
| Necessidade de intervenção manual | 4 | [Justificativa] |

**Nota final:** X/5

---

## 10. Resultado Final

### Situação inicial

[Descrever o estado antes da utilização da IA.]

### Problemas encontrados

[Resumo dos principais problemas.]

### Resultado após as iterações

[Descrever o resultado final.]

### Conformidade

- CDU: **Conforme / Parcialmente conforme / Não conforme**
- Critérios de Aceite: **Atendidos / Parcialmente atendidos / Não atendidos**
- Validação manual: **Realizada**
- Necessidade de correção humana: **Sim / Não**

---

## 11. Conclusão

A IA foi utilizada como ferramenta de apoio ao desenvolvimento,
não como autoridade para interpretação do CDU.

As respostas foram submetidas a validação e, quando identificadas
divergências em relação às regras estabelecidas, novos prompts foram
utilizados para direcionar as correções.

A solução final foi considerada [conforme/parcialmente conforme]
após a verificação dos Critérios de Aceite.