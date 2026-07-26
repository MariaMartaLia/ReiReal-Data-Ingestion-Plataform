# KPIs de Negócio

## Objetivo

Este documento apresenta os principais indicadores de negócio (KPIs) que serão gerados pelo pipeline do **ReiReal Data Ingestion**.

Os KPIs serão produzidos a partir dos dados processados na camada **Gold**, servindo como base para análises, consultas SQL e dashboards.

---

# Visão Geral

Os indicadores estão organizados por domínio de negócio:

- Vendas
- Produtos
- Categorias
- Estoque
- Clientes
- Operação
- Qualidade

---

# Vendas

## Venda Diária

**Objetivo**

Apresentar o faturamento total por dia.

**Dados necessários**

- Data da venda
- Valor total da venda

**Fórmula**

```
SUM(valor_total)
GROUP BY data
```

---

## Venda Semanal

**Objetivo**

Apresentar o faturamento por semana.

**Dados necessários**

- Data da venda
- Valor total

---

## Venda Mensal

**Objetivo**

Apresentar o faturamento consolidado por mês.

**Dados necessários**

- Data da venda
- Valor total

---

# Produtos

## Produto Mais Vendido

**Objetivo**

Identificar os produtos com maior volume de vendas.

**Dados necessários**

- Produto
- Quantidade vendida

---

## Produto Menos Vendido

**Objetivo**

Identificar produtos com baixa saída.

**Dados necessários**

- Produto
- Quantidade vendida

---

## Produtos Sem Saída

**Objetivo**

Identificar produtos que não registraram vendas no período analisado.

**Dados necessários**

- Produto
- Histórico de vendas

---

# Categorias

## Categoria Mais Vendida

**Objetivo**

Identificar as categorias com maior volume de vendas.

**Dados necessários**

- Categoria
- Quantidade vendida

---

## Categoria Menos Vendida

**Objetivo**

Identificar categorias com menor desempenho.

**Dados necessários**

- Categoria
- Quantidade vendida

---

# Estoque

## Giro de Estoque

**Objetivo**

Medir a velocidade com que os produtos deixam o estoque.

**Dados necessários**

- Produto
- Quantidade vendida
- Quantidade em estoque

---

## Tempo Médio em Estoque

**Objetivo**

Calcular quanto tempo, em média, um produto permanece armazenado antes da venda.

**Dados necessários**

- Data de entrada
- Data de saída

---

## Produtos Parados

**Objetivo**

Identificar produtos sem movimentação durante um período.

**Dados necessários**

- Produto
- Data da última venda

---

# Clientes

## Ticket Médio

**Objetivo**

Calcular o valor médio gasto por venda.

**Dados necessários**

- Valor total da venda
- Quantidade de vendas

**Fórmula**

```
SUM(valor_total) / COUNT(venda)
```

---

## Clientes Recorrentes

**Objetivo**

Identificar clientes que realizaram mais de uma compra.

**Dados necessários**

- Cliente
- Histórico de vendas

---

## Novos Clientes

**Objetivo**

Identificar clientes que realizaram sua primeira compra no período analisado.

**Dados necessários**

- Cliente
- Data da primeira compra

---

# Operação

## Horário de Maior Movimento

**Objetivo**

Identificar os horários com maior volume de vendas.

**Dados necessários**

- Hora da venda

---

## Horário de Menor Movimento

**Objetivo**

Identificar períodos de baixa movimentação.

**Dados necessários**

- Hora da venda

---

## Dia da Semana com Maior Faturamento

**Objetivo**

Determinar o dia da semana com melhor desempenho em vendas.

**Dados necessários**

- Data da venda
- Valor total

---

# Qualidade

## Reclamações

**Objetivo**

Mensurar o volume de reclamações registradas.

**Dados necessários**

- Tipo da ocorrência
- Data

---

## Elogios

**Objetivo**

Mensurar os elogios recebidos.

**Dados necessários**

- Tipo da ocorrência
- Data

---

## Motivos Mais Frequentes

**Objetivo**

Identificar os principais motivos de reclamações e elogios.

**Dados necessários**

- Categoria da ocorrência
- Descrição

---

# Origem dos Dados

Os KPIs serão gerados a partir dos datasets da camada **Gold**, utilizando informações provenientes das seguintes fontes:

- PostgreSQL
- Arquivos CSV
- Arquivos JSON
- APIs REST

---

# Consumo

Os indicadores poderão ser utilizados em:

- Consultas SQL
- Dashboards
- Relatórios gerenciais
- Estudos analíticos
- Apoio à tomada de decisão