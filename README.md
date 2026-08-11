# Anlise de Cohort


# 01 - Receita Total

## Objetivo

Calcular o faturamento total da empresa considerando apenas os pedidos concluídos.

Essa consulta representa um dos principais indicadores de desempenho (KPI) de uma empresa, permitindo acompanhar o volume financeiro gerado pelas vendas.

---

## Pergunta de Negócio

> Qual foi o faturamento total da empresa considerando apenas os pedidos concluídos?

---

## Tabelas Utilizadas

| Tabela | Descrição |
|---------|-----------|
| `pedidos` | Armazena as informações dos pedidos realizados pelos clientes. |

---

## Estratégia

A consulta realiza a soma dos valores presentes na coluna `valor_total`, considerando apenas os pedidos cujo status seja **'concluido'**.

Pedidos cancelados, devolvidos ou ainda em processamento são desconsiderados, garantindo que apenas vendas efetivamente finalizadas componham o faturamento.

---

## Consulta SQL

sql
<img width="316" height="52" alt="image" src="https://github.com/user-attachments/assets/a827c6eb-ce55-4e6f-a8f2-da5249e8a06b" />


---

## Resultado Esperado

<img width="185" height="53" alt="image" src="https://github.com/user-attachments/assets/c9f8f1ad-683f-4b26-a6e0-c77511f71c01" />

---

## Explicação da Consulta

A função `SUM()` é utilizada para somar todos os valores da coluna `valor_total`.

A cláusula `WHERE` filtra apenas os pedidos com status **'concluido'**, assegurando que o cálculo represente exclusivamente as vendas efetivadas.

O resultado da consulta é uma única linha contendo o faturamento total da empresa.

---

## Conceitos SQL Utilizados

- `SELECT`
- `SUM()`
- `WHERE`
- Funções de agregação

---

## Possíveis Insights

- Faturamento total da empresa.
- Comparação do desempenho financeiro entre períodos.
- Acompanhamento de metas comerciais.
- Base para indicadores executivos.
- Apoio na análise de crescimento da receita.

---

## Aplicação no Negócio

O faturamento total é um dos indicadores mais importantes para o acompanhamento da saúde financeira de uma empresa. A partir desse valor é possível monitorar o desempenho das vendas, comparar períodos, avaliar o impacto de campanhas comerciais e fornecer informações para a tomada de decisão estratégica.

**02 - Ticket Médio**

Calcula o valor médio gasto pelos clientes em cada pedido, permitindo avaliar o comportamento de compra e identificar oportunidades para aumentar o ticket médio.
