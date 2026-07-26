# Fontes de Dados

## Objetivo

Este documento descreve as fontes de dados suportadas pelo **ReiReal Data Ingestion**, suas características e a estratégia utilizada para ingestão.

O pipeline foi projetado para consumir dados provenientes de diferentes origens, permitindo que novas fontes sejam adicionadas sem necessidade de mudanças significativas na arquitetura.

---

# Visão Geral

Na primeira versão do projeto serão utilizadas quatro fontes de dados:

- PostgreSQL
- Arquivos CSV
- Arquivos JSON
- APIs REST

Cada fonte possui um módulo de ingestão independente, responsável por estabelecer conexão, realizar a leitura dos dados e encaminhá-los para as próximas etapas do pipeline.

---

# PostgreSQL

## Descrição

O PostgreSQL representa uma fonte de dados estruturada.

Os dados são armazenados em tabelas relacionais e podem ser consultados utilizando SQL.

Essa fonte simula bancos de dados utilizados por sistemas transacionais, ERPs, CRMs e aplicações corporativas.

---

## Exemplos de Dados

- Produtos
- Clientes
- Pedidos
- Vendas
- Estoque
- Categorias

---

## Estratégia

ELT (Extract, Load, Transform)

Os dados são extraídos do banco de dados e carregados na camada Bronze, preservando sua estrutura original.

As transformações são realizadas posteriormente.

---

## Vantagens

- Dados estruturados
- Alta confiabilidade
- Consultas SQL
- Facilidade de integração

---

# Arquivos CSV

## Descrição

Arquivos CSV são amplamente utilizados para troca de informações entre sistemas.

São simples de manipular e muito comuns em processos de importação e exportação de dados.

---

## Exemplos de Dados

- Relatórios de vendas
- Produtos
- Estoque
- Movimentações financeiras
- Exportações de sistemas

---

## Estratégia

ETL (Extract, Transform, Load)

Antes do carregamento são realizadas validações estruturais para garantir a qualidade dos dados.

---

## Validações

- Arquivo existente
- Arquivo vazio
- Cabeçalho
- Quantidade de colunas
- Tipos de dados
- Campos obrigatórios

---

## Vantagens

- Fácil integração
- Simplicidade
- Grande compatibilidade entre sistemas

---

# Arquivos JSON

## Descrição

O formato JSON é amplamente utilizado por aplicações modernas para troca de dados estruturados.

Possui uma estrutura hierárquica baseada em objetos e listas.

---

## Exemplos de Dados

- Exportações de APIs
- Configurações
- Eventos
- Catálogos
- Dados semiestruturados

---

## Estratégia

ETL (Extract, Transform, Load)

Os dados passam por validação estrutural antes de serem armazenados.

---

## Validações

- Estrutura JSON válida
- Campos obrigatórios
- Tipos de dados
- Objetos aninhados
- Listas

---

## Vantagens

- Flexibilidade
- Estrutura hierárquica
- Muito utilizado em aplicações web

---

# APIs REST

## Descrição

APIs REST permitem o consumo de informações disponibilizadas por sistemas externos através de requisições HTTP.

São utilizadas para integração entre aplicações.

---

## Exemplos de Dados

- Cotação de moedas
- Dados meteorológicos
- Produtos
- Informações públicas
- Dados governamentais

---

## Estratégia

ELT/Híbrido

Os dados são obtidos por requisições HTTP e passam por validações básicas antes do armazenamento.

Transformações mais complexas são realizadas nas etapas posteriores do pipeline.

---

## Métodos HTTP Utilizados

- GET

Nesta primeira versão do projeto serão realizadas apenas consultas para obtenção de dados.

---

## Validações

- Status HTTP
- Timeout
- Estrutura JSON
- Campos obrigatórios
- Dados vazios

---

## Vantagens

- Dados em tempo real
- Integração entre sistemas
- Atualização automática
- Grande variedade de fontes

---

# Comparativo das Fontes

| Fonte | Estrutura | Estratégia | Formato |
|--------|-----------|------------|----------|
| PostgreSQL | Estruturada | ELT | Tabelas |
| CSV | Estruturada | ETL | Arquivo texto |
| JSON | Semiestruturada | ETL | Objetos JSON |
| API REST | Semiestruturada | ELT/Híbrido | JSON |

---

# Organização dos Módulos

Cada fonte possui um módulo de ingestão independente.

```
ingestion/

├── database/
│   └── postgres_ingestion.py
│
├── csv/
│   └── csv_ingestion.py
│
├── json/
│   └── json_ingestion.py
│
├── api/
│   └── api_ingestion.py
│
└── common/
    └── base_ingestion.py
```

Essa organização permite reutilização de código, baixo acoplamento e facilidade para adicionar novas fontes no futuro.

---

# Fluxo das Fontes

Independentemente da origem, todas as fontes seguem o mesmo fluxo de processamento.

```
Fonte de Dados

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

Gold
```

---

# Extensibilidade

A arquitetura foi projetada para suportar novas fontes de dados.

Para adicionar uma nova origem, basta implementar um novo módulo de ingestão seguindo a interface definida em `BaseIngestion`.

Exemplos de futuras integrações:

- Microsoft SQL Server
- MySQL
- Oracle Database
- MongoDB
- Apache Kafka
- Amazon S3
- Azure Blob Storage
- Google Cloud Storage
- Apache Hive
- Apache Iceberg

Essa abordagem torna o pipeline modular, escalável e aderente às boas práticas de Engenharia de Dados.