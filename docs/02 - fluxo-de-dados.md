# Fluxo de Dados

## Objetivo

Este documento descreve como os dados percorrem o pipeline do **ReiReal Data Ingestion**, desde sua origem até a disponibilização para consumo analítico.

O fluxo foi projetado para garantir rastreabilidade, qualidade dos dados e separação de responsabilidades entre as etapas do processamento.

---

# Visão Geral

Todos os dados seguem um fluxo padronizado, independentemente da sua origem.

```
              Fonte de Dados

      PostgreSQL • CSV • JSON • API

                     │
                     ▼

             Camada de Ingestão

                     │
                     ▼

             Camada de Validação

                     │
                     ▼

             Camada Bronze

                     │
                     ▼

          Camada de Transformação

                     │
                     ▼

             Camada Silver

                     │
                     ▼

        Regras de Negócio / Agregações

                     │
                     ▼

              Camada Gold

                     │
                     ▼

        SQL • Dashboards • Analytics
```

---

# Etapas do Fluxo

## 1. Origem dos Dados

O pipeline pode consumir dados provenientes de diferentes fontes.

As fontes suportadas são:

- PostgreSQL
- APIs REST
- Arquivos CSV
- Arquivos JSON

Cada fonte possui seu próprio processo de ingestão, mas todas seguem o mesmo fluxo após a extração.

---

## 2. Ingestão

Nesta etapa ocorre apenas a captura dos dados.

Nenhuma regra de negócio é aplicada.

As responsabilidades desta etapa incluem:

- Conectar à fonte de dados.
- Ler os registros.
- Tratar erros de conexão.
- Registrar logs da execução.
- Encaminhar os dados para validação.

Saída:

Dados extraídos da origem.

---

## 3. Validação

Após a ingestão, os dados passam por uma camada responsável pela verificação de qualidade.

As validações incluem:

- Arquivos vazios
- Estrutura do arquivo
- Campos obrigatórios
- Tipos de dados
- Valores nulos
- Registros duplicados
- Integridade básica

Caso algum erro seja encontrado, o evento será registrado em log para análise.

Saída:

Dados validados.

---

## 4. Camada Bronze

A camada Bronze representa o armazenamento bruto dos dados.

Nenhuma transformação de negócio é aplicada.

Objetivos:

- Preservar os dados originais.
- Garantir rastreabilidade.
- Permitir reprocessamentos futuros.

Características:

- Dados brutos
- Histórico completo
- Sem limpeza
- Sem agregações

Formato previsto:

- Parquet

---

## 5. Transformações

Após o armazenamento na Bronze, inicia-se o processo de transformação.

As transformações incluem:

- Conversão de tipos
- Padronização de datas
- Padronização de textos
- Remoção de duplicidades
- Tratamento de valores nulos
- Correção de inconsistências

Nesta etapa ainda não existem indicadores de negócio.

O objetivo é apenas produzir dados consistentes.

---

## 6. Camada Silver

A camada Silver armazena dados limpos e padronizados.

Os datasets desta camada estão preparados para análises, mas ainda representam informações operacionais.

Características:

- Dados consistentes
- Dados padronizados
- Dados limpos
- Estrutura otimizada para consultas

---

## 7. Regras de Negócio

Com os dados organizados na Silver, são aplicadas regras de negócio para geração de informações analíticas.

Exemplos:

- Soma de vendas
- Ticket médio
- Total vendido por categoria
- Produtos mais vendidos
- Indicadores financeiros
- Indicadores de estoque

Esta etapa gera datasets analíticos.

---

## 8. Camada Gold

A camada Gold representa a última etapa do pipeline.

Seu objetivo é disponibilizar dados prontos para consumo.

Os datasets desta camada serão utilizados em:

- Consultas SQL
- Dashboards
- Indicadores
- Estudos analíticos
- Relatórios

Características:

- Dados agregados
- Alta performance para leitura
- Estrutura voltada ao negócio

---

# Fluxo por Fonte

## PostgreSQL

```
Banco PostgreSQL

      │

      ▼

Extração

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

Estratégia:

ELT

---

## CSV

```
Arquivo CSV

      │

      ▼

Leitura

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

Estratégia:

ETL

---

## JSON

```
Arquivo JSON

      │

      ▼

Leitura

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

Estratégia:

ETL

---

## API REST

```
API REST

      │

      ▼

Requisição HTTP

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

Estratégia:

ELT/Híbrido

---

# Fluxo de Erros

Sempre que ocorrer alguma falha durante o processamento, o pipeline deverá registrar informações para facilitar a identificação do problema.

Exemplos:

- Falha de conexão
- Arquivo inexistente
- Erro de leitura
- Timeout de API
- Campo obrigatório ausente
- Erro de conversão
- Arquivo corrompido

Todos os eventos deverão ser registrados na camada de monitoramento e logs.

---

# Resultado Final

Ao término do processamento, o pipeline disponibiliza datasets organizados em três camadas:

**Bronze**

Dados brutos preservados para auditoria e reprocessamento.

**Silver**

Dados limpos, padronizados e preparados para análises.

**Gold**

Dados consolidados para consultas SQL, dashboards e indicadores de negócio.

---

# Benefícios do Fluxo

A arquitetura proposta oferece diversos benefícios:

- Separação clara de responsabilidades.
- Facilidade para manutenção.
- Reprocessamento simplificado.
- Maior qualidade dos dados.
- Escalabilidade.
- Rastreabilidade completa.
- Facilidade para inclusão de novas fontes.
- Estrutura aderente às boas práticas de Engenharia de Dados.