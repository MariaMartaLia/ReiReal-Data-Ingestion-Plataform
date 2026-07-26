# Pipeline

## Objetivo

Este documento descreve o funcionamento do pipeline do **ReiReal Data Ingestion**, detalhando cada etapa do processamento dos dados, desde a ingestão até a disponibilização para consumo analítico.

O pipeline foi desenvolvido seguindo uma arquitetura modular, permitindo manutenção simplificada, reutilização de código e facilidade para inclusão de novas fontes de dados.

---

# Visão Geral

O pipeline segue um fluxo padronizado para todas as fontes de dados.

```
Fonte de Dados
       │
       ▼
 Ingestão dos Dados
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
       │
       ▼
 Consumo Analítico
```

Cada etapa possui uma responsabilidade específica, garantindo organização e baixo acoplamento entre os componentes.

---

# Estrutura do Pipeline

```
pipeline/

├── ingestion/
│
├── validation/
│
├── transformations/
│
├── monitoring/
│
└── data/
    ├── bronze/
    ├── silver/
    └── gold/
```

Cada módulo executa apenas uma responsabilidade dentro do fluxo.

---

# Etapas do Pipeline

## 1. Ingestão

Responsável pela extração dos dados das fontes.

As fontes suportadas são:

- PostgreSQL
- CSV
- JSON
- API REST

Nesta etapa não são realizadas transformações de negócio.

Responsabilidades:

- Estabelecer conexão.
- Ler os dados.
- Registrar erros de leitura.
- Encaminhar os dados para validação.

---

## 2. Validação

Após a ingestão, os dados passam por verificações de qualidade.

Validações previstas:

- Arquivo vazio
- Estrutura inválida
- Campos obrigatórios
- Tipos de dados
- Registros duplicados
- Valores nulos
- Integridade básica

Caso alguma inconsistência seja encontrada, o pipeline registra o evento em log.

---

## 3. Camada Bronze

Após a validação, os dados são persistidos na camada Bronze.

Características:

- Dados brutos
- Sem transformações
- Histórico preservado
- Possibilidade de reprocessamento

Formato:

- Parquet

---

## 4. Transformações

Nesta etapa ocorre a preparação dos dados.

São realizadas operações como:

- Conversão de tipos
- Padronização de datas
- Normalização de textos
- Tratamento de valores nulos
- Remoção de duplicidades
- Ajustes estruturais

O objetivo é produzir dados consistentes para análise.

---

## 5. Camada Silver

Armazena os dados tratados.

Características:

- Dados limpos
- Estrutura padronizada
- Dados consistentes
- Prontos para processamento analítico

---

## 6. Regras de Negócio

Com os dados limpos, são aplicadas regras que geram informações de valor para o negócio.

Exemplos:

- Total de vendas
- Ticket médio
- Produtos mais vendidos
- Categorias mais vendidas
- Vendas por período
- Indicadores financeiros

O resultado dessas regras alimenta a camada Gold.

---

## 7. Camada Gold

Representa a última etapa do pipeline.

Contém datasets preparados para consumo por ferramentas analíticas.

Exemplos:

- Dashboards
- Consultas SQL
- Relatórios
- Estudos analíticos

---

# Execução do Pipeline

Cada fonte de dados possui um pipeline de ingestão independente.

```
CSV ----------┐
              │
JSON ---------┤
              │
PostgreSQL ---┤
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

Essa arquitetura permite adicionar novas fontes sem alterar o fluxo principal.

---

# Componentes do Pipeline

## Ingestion

Responsável pela comunicação com as fontes de dados.

Implementações previstas:

- PostgreSQL
- CSV
- JSON
- API REST

---

## Validation

Executa verificações de qualidade dos dados antes do processamento.

---

## Transformations

Responsável pela limpeza, padronização e preparação dos dados.

---

## Monitoring

Registra informações sobre a execução do pipeline.

Exemplos:

- Tempo de execução
- Quantidade de registros processados
- Falhas
- Alertas
- Logs

---

## Data

Armazena os datasets produzidos pelo pipeline.

Organização:

```
data/

bronze/

silver/

gold/
```

---

# Tratamento de Erros

O pipeline deve tratar falhas de forma controlada.

Exemplos:

- Erro de conexão com banco
- Arquivo inexistente
- API indisponível
- Timeout
- Estrutura inválida
- Conversão de tipos
- Falhas de leitura

Todos os eventos deverão ser registrados para auditoria e depuração.

---

# Escalabilidade

A arquitetura permite crescimento gradual.

Novas fontes de dados podem ser adicionadas criando um novo módulo de ingestão.

Exemplos:

- MySQL
- Oracle
- SQL Server
- MongoDB
- Kafka
- Amazon S3
- Azure Blob Storage

Nenhuma alteração estrutural será necessária nas demais etapas do pipeline.

---

# Benefícios da Arquitetura

A implementação do pipeline oferece:

- Arquitetura modular.
- Separação de responsabilidades.
- Reutilização de componentes.
- Baixo acoplamento.
- Facilidade de manutenção.
- Escalabilidade.
- Rastreabilidade dos dados.
- Facilidade para inclusão de novas fontes.
- Organização em camadas Bronze, Silver e Gold.
- Preparação dos dados para consumo analítico.

---

# Próximas Evoluções

As próximas versões do pipeline poderão incluir:

- Processamento distribuído com PySpark.
- Orquestração de pipelines.
- Agendamento automático.
- Testes automatizados.
- Monitoramento em tempo real.
- Integração com serviços de nuvem.
- Data Quality avançada.
- Novas fontes de dados.