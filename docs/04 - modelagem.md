# Modelagem dos Dados

## Objetivo

Este documento descreve a organização dos dados dentro do pipeline do **ReiReal Data Ingestion**.

A modelagem define como os dados são representados em cada camada do Data Lake, desde a ingestão até a disponibilização para consumo analítico.

O objetivo é garantir consistência, rastreabilidade e facilitar a evolução do projeto.

---

# Visão Geral

O pipeline organiza os dados em três camadas principais:

```
Bronze
    │
    ▼
Silver
    │
    ▼
Gold
```

Cada camada possui uma finalidade específica e representa um estágio do processamento dos dados.

---

# Camada Bronze

## Objetivo

Armazenar os dados exatamente como foram recebidos da fonte de origem.

Nesta camada nenhuma regra de negócio é aplicada.

Características:

- Dados brutos
- Histórico completo
- Sem limpeza
- Sem agregações
- Alta rastreabilidade

Exemplo:

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

# Camada Silver

## Objetivo

Armazenar dados tratados e padronizados.

Nesta etapa são realizadas transformações para garantir consistência.

Transformações previstas:

- Conversão de tipos
- Padronização de datas
- Tratamento de valores nulos
- Remoção de duplicidades
- Normalização de textos

Exemplo:

```
silver/

├── products.parquet
├── customers.parquet
├── sales.parquet
├── categories.parquet
└── exchange_rates.parquet
```

Nesta camada cada dataset representa uma entidade de negócio limpa e padronizada.

---

# Camada Gold

## Objetivo

Disponibilizar dados preparados para consumo analítico.

Os datasets desta camada representam indicadores de negócio e informações consolidadas.

Exemplo:

```
gold/

├── sales_by_day.parquet
├── sales_by_month.parquet
├── top_products.parquet
├── top_categories.parquet
├── average_ticket.parquet
└── inventory_turnover.parquet
```

---

# Organização dos Datasets

Os dados serão organizados por domínio de negócio.

## Produtos

Informações referentes aos produtos.

Exemplo de atributos:

- id
- nome
- categoria
- preço
- custo
- status

---

## Clientes

Informações dos clientes.

Exemplo:

- id
- nome
- cidade
- estado

---

## Vendas

Informações das vendas.

Exemplo:

- id_venda
- data
- cliente
- produto
- quantidade
- valor_unitario
- valor_total

---

## Categorias

Informações das categorias de produtos.

Exemplo:

- id
- nome
- descrição

---

## Estoque

Informações relacionadas ao estoque.

Exemplo:

- produto
- quantidade
- data_movimentacao
- tipo_movimentacao

---

# Evolução dos Dados

Os dados evoluem ao longo do pipeline.

## Bronze

Dados exatamente como chegaram.

↓

## Silver

Dados limpos e padronizados.

↓

## Gold

Dados agregados e preparados para análise.

---

# Formato de Armazenamento

Os datasets serão persistidos em formato Parquet.

Benefícios:

- Compressão
- Alto desempenho
- Leitura colunar
- Integração com Spark
- Integração com Pandas

---

# Convenções de Nomenclatura

Os datasets seguirão um padrão de nomenclatura.

Exemplos:

```
products.parquet

customers.parquet

sales.parquet

categories.parquet

inventory.parquet

sales_by_day.parquet

sales_by_month.parquet

top_products.parquet
```

Boas práticas:

- letras minúsculas
- palavras separadas por underscore
- nomes descritivos
- sem espaços
- sem caracteres especiais

---

# Evolução da Modelagem

A modelagem foi projetada para permitir a inclusão de novos datasets sem impacto na arquitetura existente.

Novas entidades poderão ser adicionadas conforme surgirem novas fontes de dados ou novas necessidades analíticas.

Essa abordagem garante escalabilidade e facilidade de manutenção ao longo da evolução do projeto.