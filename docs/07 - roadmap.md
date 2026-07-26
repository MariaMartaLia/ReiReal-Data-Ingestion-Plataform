# Roadmap

## Objetivo

Este documento apresenta o planejamento evolutivo do **ReiReal Data Ingestion**.

O desenvolvimento do projeto foi dividido em versões incrementais, permitindo que novas funcionalidades sejam adicionadas de forma organizada, sem comprometer a arquitetura existente.

Cada etapa representa uma evolução do pipeline e demonstra a aplicação gradual de conceitos de Engenharia de Dados.

---

# Visão Geral

```
MVP
 │
 ▼
v1.1
 │
 ▼
v1.2
 │
 ▼
v2.0
 │
 ▼
v3.0
```

---

# MVP - Fundação do Pipeline

## Objetivo

Construir a estrutura inicial do projeto e implementar um pipeline funcional utilizando múltiplas fontes de dados.

### Funcionalidades

- Estrutura do projeto
- Arquitetura em camadas
- Ingestão de CSV
- Ingestão de JSON
- Ingestão de PostgreSQL
- Consumo de API REST
- Validação de dados
- Persistência em Parquet
- Camadas Bronze, Silver e Gold
- Transformações básicas
- Geração de indicadores iniciais
- Documentação completa

### Status

🟡 Em desenvolvimento

---

# Versão 1.1

## Objetivo

Melhorar a qualidade do pipeline e ampliar a cobertura de validações.

### Funcionalidades

- Validação avançada
- Tratamento de exceções
- Sistema de logs
- Configuração por arquivo `.env`
- Melhor organização dos módulos
- Refatoração do código
- Testes unitários iniciais

### Status

⚪ Planejado

---

# Versão 1.2

## Objetivo

Adicionar monitoramento e métricas de execução.

### Funcionalidades

- Tempo de execução
- Quantidade de registros processados
- Quantidade de erros
- Quantidade de arquivos processados
- Relatórios de execução
- Histórico das execuções

### Status

⚪ Planejado

---

# Versão 2.0

## Objetivo

Escalar o processamento utilizando ferramentas voltadas para grandes volumes de dados.

### Funcionalidades

- Processamento com PySpark
- Execução no Databricks Community Edition
- Otimização de transformações
- Processamento distribuído
- Melhor desempenho

### Status

⚪ Planejado

---

# Versão 2.1

## Objetivo

Expandir as fontes de dados suportadas pelo pipeline.

### Funcionalidades

- Microsoft SQL Server
- MySQL
- Oracle Database
- MongoDB
- Apache Kafka
- Amazon S3
- Azure Blob Storage

### Status

⚪ Planejado

---

# Versão 3.0

## Objetivo

Automatizar a execução e tornar o pipeline mais próximo de um ambiente de produção.

### Funcionalidades

- Orquestração de pipelines
- Agendamento automático
- Monitoramento contínuo
- Alertas de falha
- Data Quality avançada
- Versionamento dos datasets
- Integração com serviços de nuvem

### Status

⚪ Planejado

---

# Tecnologias por Versão

| Versão | Tecnologias |
|---------|-------------|
| MVP | Python, Pandas, PostgreSQL, Requests, PyArrow |
| v1.1 | Logging, python-dotenv, Pytest |
| v1.2 | Monitoramento e métricas |
| v2.0 | PySpark, Databricks |
| v2.1 | Novas fontes de dados |
| v3.0 | Orquestração e automação |

---

# Evolução da Arquitetura

```
MVP

CSV
JSON
PostgreSQL
API

        │

        ▼

Bronze
Silver
Gold

        │

        ▼

---------------------------

v2.0

PySpark

Processamento Distribuído

Databricks

        │

        ▼

---------------------------

v3.0

Orquestração

Monitoramento

Automação

Cloud
```

---

# Prioridades

## Alta Prioridade

- Estrutura do projeto
- Ingestão de dados
- Validação
- Bronze
- Silver
- Gold
- Persistência em Parquet

---

## Média Prioridade

- Logs
- Testes
- Monitoramento
- Configuração por ambiente

---

## Baixa Prioridade

- PySpark
- Databricks
- Kafka
- Cloud
- Orquestração

---

# Critérios de Conclusão do MVP

O MVP será considerado concluído quando atender aos seguintes requisitos:

- Pipeline funcional.
- Ingestão das quatro fontes de dados.
- Dados persistidos em Parquet.
- Camadas Bronze, Silver e Gold implementadas.
- Validações básicas funcionando.
- Geração de indicadores analíticos.
- Documentação completa.
- Código versionado no GitHub.

---

# Visão de Longo Prazo

O objetivo é transformar o **ReiReal Data Ingestion** em um projeto de portfólio que demonstre competências essenciais de um Engenheiro de Dados, incluindo:

- Arquitetura de pipelines.
- Ingestão de múltiplas fontes.
- Qualidade de dados.
- Transformações.
- Modelagem em camadas.
- Processamento distribuído.
- Monitoramento.
- Boas práticas de desenvolvimento.
- Escalabilidade e manutenção.