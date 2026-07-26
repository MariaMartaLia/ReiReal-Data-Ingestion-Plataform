# ReiReal Data Ingestion

Pipeline de Engenharia de Dados desenvolvido para demonstrar a construção de um ambiente de ingestão, processamento e disponibilização de dados utilizando Python e conceitos modernos de Data Engineering.

O projeto simula um cenário real de varejo, consumindo dados de múltiplas fontes, aplicando validações, armazenando informações em um Data Lake e produzindo datasets analíticos para consultas e indicadores de negócio.

---

## Objetivos

- Construir pipelines de ingestão de dados.
- Integrar múltiplas fontes de dados.
- Aplicar conceitos de ETL e ELT.
- Implementar uma arquitetura em camadas (Bronze, Silver e Gold).
- Validar e padronizar dados antes do processamento.
- Gerar datasets analíticos para consumo por consultas SQL e dashboards.
- Demonstrar boas práticas de Engenharia de Dados.

---

## Arquitetura

```
              Fontes de Dados

 PostgreSQL • CSV • JSON • API REST

                │
                ▼

          Camada de Ingestão

                │
                ▼

         Validação dos Dados

                │
                ▼

        Bronze (Raw Data)

                │
                ▼

         Transformações

                │
                ▼

        Silver (Clean Data)

                │
                ▼

      Regras de Negócio

                │
                ▼

        Gold (Analytics)

                │
                ▼

 SQL • Dashboards • Indicadores
```

---

## Fontes de Dados

O pipeline suporta diferentes origens de dados:

- PostgreSQL
- Arquivos CSV
- Arquivos JSON
- APIs REST

Cada fonte possui um módulo de ingestão independente, permitindo escalabilidade e reutilização de código.

---

## Tecnologias

- Python
- PostgreSQL
- SQL
- Pandas
- PyArrow
- Requests
- PySpark
- Git
- GitHub
- Databricks Community Edition
- VS Code

---

## Estrutura do Projeto

```
reireal-data-ingestion/

├── config/
├── data/
│   ├── bronze/
│   ├── silver/
│   └── gold/
├── docs/
├── ingestion/
├── logs/
├── monitoring/
├── notebooks/
├── sql/
├── tests/
├── transformations/
├── utils/
└── validation/
```

---

## Documentação

A documentação do projeto está organizada na pasta `docs/`.

- Arquitetura
- Fluxo de Dados
- Fontes de Dados
- Pipeline
- Modelagem dos Dados
- Camadas Bronze, Silver e Gold
- Catálogo de KPIs
- Roadmap
- Escopo do MVP

---

## Roadmap

### MVP

- Estrutura do projeto
- Ingestão de CSV
- Ingestão de JSON
- Ingestão de PostgreSQL
- Consumo de API REST
- Validação dos dados
- Camadas Bronze, Silver e Gold
- Persistência em Parquet
- KPIs iniciais

### Próximas versões

- Processamento com PySpark
- Databricks Community Edition
- Monitoramento e métricas
- Testes automatizados
- Novas fontes de dados
- Orquestração de pipelines

---

## Status

🚧 Projeto em desenvolvimento.

O objetivo da primeira versão é entregar um pipeline funcional, modular e bem documentado, demonstrando conceitos fundamentais de Engenharia de Dados.

---

## Licença

Este projeto foi desenvolvido para fins de estudo, aprendizado e composição de portfólio.