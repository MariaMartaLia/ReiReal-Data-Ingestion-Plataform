# Camadas Bronze, Silver e Gold

## Objetivo

Este documento descreve a organização das camadas **Bronze**, **Silver** e **Gold** utilizadas no projeto **ReiReal Data Ingestion**.

A arquitetura em camadas tem como objetivo separar as diferentes etapas do processamento dos dados, garantindo rastreabilidade, qualidade e disponibilidade para consumo analítico.

Cada camada representa um estágio específico da evolução dos dados dentro do pipeline.

---

# Visão Geral

```
             Fontes de Dados

PostgreSQL • CSV • JSON • API REST

                │
                ▼

             Ingestão

                │
                ▼

            Validação

                │
                ▼

        🟤 Bronze (Raw Data)

                │
                ▼

         Transformações

                │
                ▼

        ⚪ Silver (Clean Data)

                │
                ▼

      Regras de Negócio

                │
                ▼

        🟡 Gold (Analytics)

                │
                ▼

SQL • Dashboards • Indicadores
```

---

# Camada Bronze

## Objetivo

A camada Bronze é responsável por armazenar os dados exatamente como foram recebidos da fonte de origem.

Nenhuma regra de negócio é aplicada nesta etapa.

Seu principal objetivo é preservar os dados originais para garantir rastreabilidade e possibilitar reprocessamentos futuros.

---

## Características

- Dados brutos.
- Sem transformações.
- Sem agregações.
- Histórico completo.
- Alta rastreabilidade.
- Base para todas as etapas seguintes.

---

## O que acontece nesta camada?

Após a ingestão e as validações básicas, os dados são armazenados na Bronze mantendo sua estrutura original.

Exemplos:

- Arquivos CSV
- Arquivos JSON
- Dados extraídos do PostgreSQL
- Respostas de APIs

---

## Estrutura

```
bronze/

├── postgres/
│   ├── products.parquet
│   ├── customers.parquet
│   └── sales.parquet
│
├── csv/
│   └── sales.parquet
│
├── json/
│   └── products.parquet
│
└── api/
    └── exchange_rates.parquet
```

---

## Benefícios

- Preservação dos dados originais.
- Auditoria.
- Reprocessamento.
- Comparação entre versões.
- Recuperação em caso de falhas.

---

# Camada Silver

## Objetivo

A camada Silver é responsável pelo tratamento e padronização dos dados.

Nesta etapa os dados passam por transformações que eliminam inconsistências e melhoram sua qualidade.

O foco é disponibilizar datasets limpos e consistentes para análises posteriores.

---

## Características

- Dados limpos.
- Dados padronizados.
- Dados consistentes.
- Sem registros duplicados.
- Tipos de dados corrigidos.

---

## Transformações

As principais transformações incluem:

- Conversão de tipos.
- Padronização de datas.
- Padronização de textos.
- Remoção de duplicidades.
- Tratamento de valores nulos.
- Correção de inconsistências.
- Renomeação de colunas.
- Normalização de informações.

---

## Estrutura

```
silver/

├── products.parquet
├── customers.parquet
├── sales.parquet
├── categories.parquet
└── exchange_rates.parquet
```

---

## Benefícios

- Maior qualidade dos dados.
- Facilidade para consultas.
- Dados consistentes.
- Base confiável para análises.

---

# Camada Gold

## Objetivo

A camada Gold contém dados preparados para consumo analítico.

Nesta etapa são aplicadas regras de negócio, agregações e cálculos que geram informações de valor para tomada de decisão.

Os datasets desta camada são otimizados para consultas SQL, dashboards e indicadores.

---

## Características

- Dados consolidados.
- Dados agregados.
- Estrutura voltada ao negócio.
- Alta performance para leitura.

---

## Exemplos de Indicadores

- Produto mais vendido.
- Categoria mais vendida.
- Ticket médio.
- Venda diária.
- Venda semanal.
- Venda mensal.
- Faturamento.
- Lucro bruto.
- Giro de estoque.

---

## Estrutura

```
gold/

├── sales_by_day.parquet
├── sales_by_month.parquet
├── top_products.parquet
├── top_categories.parquet
├── average_ticket.parquet
├── revenue.parquet
└── inventory_turnover.parquet
```

---

## Benefícios

- Consultas rápidas.
- Dashboards simplificados.
- Indicadores prontos para consumo.
- Menor processamento durante as análises.

---

# Evolução dos Dados

Durante o processamento, os dados evoluem em qualidade e valor analítico.

```
Bronze

Dados Brutos

        │

        ▼

Silver

Dados Limpos e Padronizados

        │

        ▼

Gold

Dados Consolidados e Analíticos
```

Cada camada possui uma responsabilidade específica e complementa a anterior.

---

# Comparativo das Camadas

| Característica | Bronze | Silver | Gold |
|----------------|:------:|:------:|:----:|
| Dados Brutos | ✅ | ❌ | ❌ |
| Dados Tratados | ❌ | ✅ | ✅ |
| Regras de Negócio | ❌ | ❌ | ✅ |
| Agregações | ❌ | ❌ | ✅ |
| Histórico Completo | ✅ | ❌ | ❌ |
| Dados para Dashboards | ❌ | ❌ | ✅ |
| Reprocessamento | ✅ | ❌ | ❌ |

---

# Fluxo Entre as Camadas

```
Fontes de Dados

        │

        ▼

Ingestão

        │

        ▼

Validação

        │

        ▼

Bronze

        │

        ▼

Transformações

        │

        ▼

Silver

        │

        ▼

Regras de Negócio

        │

        ▼

Gold
```

Cada etapa adiciona valor aos dados, tornando-os progressivamente mais organizados, consistentes e úteis para análise.

---

# Considerações Finais

A utilização das camadas Bronze, Silver e Gold proporciona uma arquitetura escalável e alinhada às boas práticas de Engenharia de Dados.

Essa abordagem facilita a manutenção do pipeline, melhora a qualidade dos dados e permite que novas fontes e regras de negócio sejam incorporadas sem alterar a estrutura principal do projeto.

O **ReiReal Data Ingestion** adota esse modelo para garantir que os dados sejam preservados em sua forma original, evoluam por meio de transformações controladas e estejam disponíveis para consumo analítico de forma confiável e eficiente.