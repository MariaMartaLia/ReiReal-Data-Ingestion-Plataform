# Arquitetura

## Visão Geral

O **ReiReal Data Ingestion** é um projeto de Engenharia de Dados desenvolvido para centralizar a ingestão de dados provenientes de diferentes fontes, garantindo qualidade, organização e disponibilidade para consumo analítico.

O projeto foi construído utilizando conceitos modernos de Data Engineering, adotando uma arquitetura em camadas que separa as responsabilidades de ingestão, validação, transformação e disponibilização dos dados.

Essa abordagem facilita a manutenção, escalabilidade e evolução dos pipelines, permitindo a inclusão de novas fontes de dados sem impactar a arquitetura existente.

---

# Objetivos da Arquitetura

A arquitetura possui os seguintes objetivos:

- Centralizar a ingestão de dados de múltiplas fontes.
- Separar responsabilidades entre as etapas do pipeline.
- Garantir rastreabilidade dos dados durante todo o processamento.
- Assegurar qualidade e consistência das informações.
- Facilitar manutenção e evolução dos pipelines.
- Disponibilizar dados confiáveis para análises e indicadores de negócio.

---

# Arquitetura do Pipeline

```
                  Fontes de Dados

      PostgreSQL     CSV     JSON     API REST

                     │
                     ▼

             Camada de Ingestão

                     │
                     ▼

             Camada de Validação

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

# Estrutura do Projeto

```
REIREAL-DATA-INGESTION

├── config/
│
├── ingestion/
│   ├── database/
│   │   └── postgres_ingestion.py
│   │
│   ├── api/
│   │   └── api_ingestion.py
│   │
│   ├── csv/
│   │   └── csv_ingestion.py
│   │
│   ├── json/
│   │   └── json_ingestion.py
│   │
│   └── common/
│       └── base_ingestion.py
│
├── validation/
│
├── transformations/
│
├── monitoring/
│
├── data/
│   ├── bronze/
│   ├── silver/
│   └── gold/
│
├── sql/
│
├── notebooks/
│
├── logs/
│
└── tests/
```

---

# Organização das Camadas

## Fontes de Dados

São responsáveis por fornecer as informações que serão processadas pelo pipeline.

Nesta primeira versão do projeto serão utilizadas quatro fontes distintas:

- PostgreSQL
- APIs REST
- Arquivos CSV
- Arquivos JSON

Cada fonte possui um pipeline de ingestão independente, permitindo evolução e manutenção de forma isolada.

---

## Camada de Ingestão

Responsável exclusivamente pela extração dos dados.

Nesta etapa não são realizadas transformações de negócio.

Seu objetivo é conectar às fontes de dados, realizar a leitura das informações e encaminhá-las para o processo de validação ou armazenamento, conforme a estratégia adotada.

---

## Camada de Validação

Responsável por verificar a qualidade dos dados antes que avancem pelo pipeline.

Entre as validações previstas estão:

- Arquivos vazios
- Campos obrigatórios
- Tipos de dados
- Valores nulos
- Registros duplicados
- Integridade dos dados
- Estrutura dos arquivos

---

## Camada Bronze

Representa a primeira camada do Data Lake.

Seu objetivo é armazenar os dados exatamente como foram recebidos da origem.

Características:

- Dados brutos
- Histórico completo
- Sem regras de negócio
- Sem agregações
- Alta rastreabilidade

---

## Camada Silver

Responsável pelo tratamento e padronização dos dados.

Nesta camada são realizadas transformações como:

- Remoção de duplicidades
- Conversão de tipos
- Tratamento de valores nulos
- Padronização de datas
- Padronização de nomes
- Normalização de informações

Ao final desta etapa os dados tornam-se consistentes para utilização analítica.

---

## Camada Gold

Representa a camada analítica do projeto.

Contém dados preparados para consumo por ferramentas analíticas, consultas SQL e dashboards.

Nesta camada serão produzidos indicadores como:

- Produto mais vendido
- Categoria mais vendida
- Ticket médio
- Venda diária
- Venda semanal
- Venda mensal
- Giro de estoque
- Indicadores financeiros

---

# Estratégia de Ingestão

Cada fonte de dados utiliza a estratégia mais adequada ao seu formato.

| Fonte | Estratégia | Justificativa |
|--------|------------|---------------|
| PostgreSQL | ELT | Dados estruturados permitem carregamento direto para Bronze. |
| API REST | ELT/Híbrido | Pequenas validações podem ocorrer antes do armazenamento. |
| CSV | ETL | Arquivos exigem validação estrutural antes da carga. |
| JSON | ETL | Necessita padronização antes do armazenamento. |

---

# Fluxo Geral dos Dados

O processamento segue a seguinte sequência:

1. Leitura da fonte de dados.
2. Extração das informações.
3. Validação da estrutura.
4. Armazenamento na camada Bronze.
5. Transformações e limpeza.
6. Geração da camada Silver.
7. Aplicação das regras de negócio.
8. Geração da camada Gold.
9. Disponibilização para consultas analíticas.

---

# Tecnologias

O projeto utiliza as seguintes tecnologias:

- Python
- PostgreSQL
- SQL
- Pandas
- PyArrow
- Requests
- PySpark
- Git
- GitHub
- VS Code
- Databricks Community Edition

---

# Princípios Arquiteturais

Toda a arquitetura foi construída seguindo os seguintes princípios:

- Separação de responsabilidades.
- Organização em camadas.
- Reutilização de código.
- Baixo acoplamento.
- Alta coesão.
- Escalabilidade.
- Facilidade de manutenção.
- Qualidade dos dados.
- Rastreabilidade.
- Evolução incremental do pipeline.

---

# Escopo da Primeira Versão (MVP)

A primeira versão do projeto terá como objetivo demonstrar as principais competências de Engenharia de Dados.

Serão implementadas:

- Ingestão de arquivos CSV.
- Ingestão de arquivos JSON.
- Ingestão de dados PostgreSQL.
- Consumo de uma API REST.
- Validação dos dados.
- Armazenamento em Bronze, Silver e Gold.
- Geração de indicadores básicos de negócio.
- Persistência em formato Parquet.
- Documentação completa da arquitetura e dos pipelines.

Novas funcionalidades serão adicionadas nas próximas versões sem necessidade de alterações estruturais na arquitetura.