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

<img width="319" height="54" alt="image" src="https://github.com/user-attachments/assets/81218f78-4654-4bf3-b764-558c2b1f7099" />

---

## Resultado Esperado

<img width="319" height="54" alt="image" src="https://github.com/user-attachments/assets/8ea07ced-fc58-4d8a-8b91-c39b60407b36" />

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


--------------------------------------------------


# 02 - Ticket Médio

## Objetivo

Calcular o valor médio gasto pelos clientes por pedido concluído.

O ticket médio é um dos principais indicadores comerciais, utilizado para avaliar o comportamento de compra dos clientes e medir a eficiência das estratégias de vendas.

---

## Pergunta de Negócio

> Qual é o valor médio gasto pelos clientes em cada pedido concluído?

---

## Tabelas Utilizadas

| Tabela | Descrição |
|---------|-----------|
| `pedidos` | Armazena as informações dos pedidos realizados pelos clientes. |

---

## Estratégia

A consulta calcula a média dos valores da coluna `valor_total`, considerando apenas os pedidos com status **'concluido'**.

Ao excluir pedidos cancelados, devolvidos ou em processamento, o indicador representa apenas compras efetivamente realizadas.

---

## Consulta SQL

<img width="434" height="478" alt="image" src="https://github.com/user-attachments/assets/08f4ee2b-e180-450e-a57e-5ce315ecdd98" />


---

## Resultado Esperado

<img width="667" height="55" alt="image" src="https://github.com/user-attachments/assets/a4aabc5f-04cb-4217-b4fc-c0d9b905cc35" />


---

## Explicação da Consulta

A função `AVG()` calcula a média dos valores presentes na coluna `valor_total`.

A cláusula `WHERE` filtra somente os pedidos concluídos, garantindo que o cálculo represente o valor médio das compras efetivamente finalizadas.

O resultado da consulta é uma única linha contendo o ticket médio da empresa.

---

## Conceitos SQL Utilizados

- `SELECT`
- `AVG()`
- `WHERE`
- Funções de agregação

---

## Possíveis Insights

- Valor médio gasto por compra.
- Comparação do ticket médio entre períodos.
- Avaliação do impacto de promoções e descontos.
- Identificação de oportunidades para aumentar o valor médio dos pedidos.
- Apoio na definição de estratégias de vendas e marketing.

---

## Aplicação no Negócio

O ticket médio é um indicador amplamente utilizado para acompanhar o comportamento de compra dos clientes. Seu monitoramento permite avaliar a efetividade de campanhas promocionais, estratégias de cross-selling e up-selling, além de identificar oportunidades para aumentar a receita sem a necessidade de adquirir novos clientes.


--------------------------------------------------


# 02 - Ticket Médio por Região

## Objetivo

Calcular o ticket médio dos pedidos concluídos para cada estado e identificar a região que apresenta o maior valor médio por pedido.

Essa consulta permite analisar as diferenças de comportamento de compra entre as regiões atendidas pela empresa.

---

## Pergunta de Negócio

> Qual região possui o maior ticket médio considerando apenas os pedidos concluídos?

---

## Tabelas Utilizadas

| Tabela | Descrição |
|---------|-----------|
| `clientes` | Armazena as informações dos clientes, incluindo o estado onde estão localizados. |
| `pedidos` | Armazena as informações dos pedidos realizados pelos clientes, incluindo o valor total e o status do pedido. |

---

## Estratégia

A consulta relaciona as tabelas `clientes` e `pedidos` por meio da coluna `cliente_id`.

Em seguida, considera apenas os pedidos com status **'concluido'** e calcula o ticket médio de cada estado utilizando a função `AVG()` sobre a coluna `valor_total`.

Por fim, os estados são ordenados de forma decrescente pelo ticket médio, permitindo identificar a região com o maior valor médio por pedido.

---

## Consulta SQL

<img width="422" height="151" alt="image" src="https://github.com/user-attachments/assets/44634671-83d9-4f4e-8358-44e0a8b19ede" />

---

## Resultado Esperado

<img width="304" height="361" alt="image" src="https://github.com/user-attachments/assets/24a18980-6024-4718-aba4-9a1ff7d8407c" />

---

## Explicação da Consulta

O `INNER JOIN` relaciona cada pedido ao respectivo cliente por meio da coluna `cliente_id`.

```sql
INNER JOIN pedidos p
    ON p.cliente_id = c.cliente_id
```

A cláusula:

```sql
WHERE p.status = 'concluido'
```

garante que somente os pedidos concluídos sejam considerados no cálculo.

A função `AVG()` calcula o valor médio dos pedidos de cada estado:

```sql
AVG(p.valor_total)
```

O agrupamento:

```sql
GROUP BY c.estado
```

permite calcular um ticket médio individualmente para cada estado.

Por fim:

```sql
ORDER BY ticket_medio DESC
```

ordena os estados do maior para o menor ticket médio, enquanto `TOP 1` retorna somente o estado com o maior resultado.

---

## Conceitos SQL Utilizados

- `SELECT`
- `TOP`
- `INNER JOIN`
- `WHERE`
- `AVG()`
- `GROUP BY`
- `ORDER BY`
- Funções de agregação
- Alias de coluna

---

## Possíveis Insights

- Identificação das regiões com maior valor médio de compra.
- Comparação do comportamento de consumo entre estados.
- Identificação de regiões com maior potencial comercial.
- Apoio na definição de estratégias de vendas e marketing.
- Identificação de oportunidades para aumentar o ticket médio em regiões de menor desempenho.

---

## Aplicação no Negócio

O ticket médio por região permite identificar diferenças no comportamento de compra dos clientes em diferentes estados.

A partir dessa análise, a empresa pode direcionar estratégias comerciais específicas para cada região, como campanhas promocionais, ofertas de produtos complementares e estratégias de aumento do valor médio das compras.


--------------------------------------------------


# 03 - Taxa de Recompra

## Objetivo

Calcular a taxa de recompra dos clientes, identificando o percentual de clientes que realizaram uma nova compra após o primeiro pedido concluído.

Essa análise permite avaliar o nível de fidelização dos clientes e entender a capacidade da empresa de transformar compradores ocasionais em clientes recorrentes.

---

## Pergunta de Negócio

> Qual é a taxa de recompra dos clientes considerando apenas os pedidos concluídos?

---

## Tabelas Utilizadas

| Tabela | Descrição |
|---------|-----------|
| `clientes` | Armazena as informações dos clientes cadastrados. |
| `pedidos` | Armazena os pedidos realizados pelos clientes, incluindo a data e o status da compra. |

---

## Estratégia

A consulta identifica a primeira compra concluída de cada cliente e, posteriormente, verifica quais clientes realizaram pelo menos uma nova compra.

Para isso, são consideradas apenas as compras com status **'concluido'**.

A taxa de recompra é obtida dividindo a quantidade de clientes que realizaram uma segunda compra pela quantidade total de clientes que realizaram a primeira compra.


::contentReference[oaicite:0]{index=0}


---

## Consulta SQL

<img width="434" height="478" alt="image" src="https://github.com/user-attachments/assets/9548e64d-af3e-4e69-9a14-0f245bf80d67" />

---

## Resultado Esperado

<img width="667" height="55" alt="image" src="https://github.com/user-attachments/assets/8af4d16e-6fd8-42fe-b95a-83163ae0cd27" />

---

## Explicação da Consulta

A primeira CTE, `compras`, identifica a data da primeira compra concluída de cada cliente utilizando a função `MIN()`.

```sql
MIN(data_pedido)
```

O agrupamento por `cliente_id` garante que seja encontrada uma única primeira compra para cada cliente.

A segunda CTE, `clientes_que_recompram`, identifica os clientes que realizaram pelo menos uma nova compra após a primeira.

```sql
p.data_pedido > pc.primeira_compra
```

O `GROUP BY` nessa etapa evita que um mesmo cliente seja contado várias vezes caso tenha realizado múltiplas compras.

Por fim, a consulta compara a quantidade de clientes que realizaram uma recompra com a quantidade total de clientes que realizaram uma primeira compra.

O resultado é apresentado em percentual.

---

## Conceitos SQL Utilizados

- `WITH`
- CTE (Common Table Expression)
- `MIN()`
- `COUNT()`
- `INNER JOIN`
- `LEFT JOIN`
- `GROUP BY`
- `WHERE`
- `CASE`
- Operadores de comparação
- Cálculo percentual

---

## Possíveis Insights

- Percentual de clientes que retornam para realizar uma nova compra.
- Nível de fidelização da base de clientes.
- Eficiência das estratégias de retenção.
- Identificação de oportunidades para campanhas de relacionamento.
- Avaliação da recorrência dos clientes ao longo do tempo.

---

## Aplicação no Negócio

A taxa de recompra é um importante indicador de retenção e fidelização de clientes.

Uma taxa elevada pode indicar que os clientes possuem uma boa experiência com a empresa e apresentam maior propensão a realizar novas compras.

Por outro lado, uma taxa baixa pode indicar oportunidades de melhoria em estratégias de relacionamento, pós-venda, campanhas de fidelização e experiência do cliente.


--------------------------------------------------


