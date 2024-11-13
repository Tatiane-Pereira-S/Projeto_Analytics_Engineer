# Projeto de Análise de Dados Airbnb com SQLite, Pandas, DBT e Great Expectations

Este projeto realiza uma análise de dados dos arquivos de listagens e avaliações do Airbnb usando diversas ferramentas como `Pandas` para transformação de dados, `SQLite` para armazenamento, `DBT` para criação de camadas de dados e `Great Expectations` para validação. A análise é composta por três camadas (Bronze, Silver e Gold) que organizam e enriquecem os dados para consultas analíticas.

## Objetivo

Processar e estruturar os dados de listagens e avaliações do Airbnb de forma eficiente para obter insights sobre preços médios por bairro e garantir a qualidade dos dados através da validação.

## Estrutura do Projeto

1. **Camada Bronze**: Armazena os dados brutos.
2. **Camada Silver**: Realiza a limpeza dos dados, como remoção de duplicatas e conversão de tipos.
3. **Camada Gold**: Agrega os dados para gerar insights, como o preço médio por bairro.

## Pré-requisitos

Certifique-se de ter os seguintes pacotes instalados:

- `pandas`
- `sqlalchemy`
- `sqlite3`
- `dbt` com o adaptador `dbt-sqlite`
- `great_expectations`

Instale as dependências adicionais com:

```bash
pip install -r requirements.txt 
```


## Estrutura de Código

### Importação e Preparação dos Dados
- Importa arquivos CSV de listagens e avaliações para 2023 e 2024.
- Concatena esses dados em DataFrames completos, `df_listing_total` e `df_reviews_global`.

### Criação e Limpeza da Camada Bronze
- Utiliza `sqlite3` para criar e armazenar os dados na camada Bronze com `to_sql`.

### Transformação para Camada Silver
- Realiza operações de limpeza, como remoção de duplicatas e normalização de colunas.
- Converte a coluna `price` para formato numérico e preenche valores ausentes com a média de preço.

### Camada Gold - Agregação de Dados
- Executa uma consulta SQL para calcular o preço médio por bairro na camada Silver, armazenando o resultado em `avg_price_gold`.

### Validação com Great Expectations
- Valida as tabelas agregadas, assegurando a integridade dos dados, como valores de `avg_price` dentro do intervalo esperado (100 a 2000).

### Configuração DBT
- Configura e executa modelos DBT para `listings_bronze`, `listings_silver` e `listings_gold`, além de agregar os dados em `price_by_neighbourhood.sql`.

## Como Executar

### Execução de Carga e Transformação
- Execute o script principal para carregar e transformar os dados até a camada Gold.

### Validação de Dados
- Execute o `Great Expectations` para garantir que os dados estão dentro dos padrões definidos.

### DBT
- Inicie o projeto DBT com `dbt run` para aplicar as transformações nas camadas.

## Estrutura de Diretórios

```plaintext


├── data/                  # Arquivos CSV de entrada
├── dbt_airbnb/            # Projeto DBT
│   ├── models/
│   ├── profiles.yml
├── notebooks/             # Jupyter Notebooks
└── README.md
```

## Resultados

- **Tabela Gold**: Uma tabela contendo o preço médio das listagens do Airbnb por bairro, disponível para visualização e consulta.

## Conclusão

Este projeto exemplifica um pipeline de ETL com camadas de dados, permitindo fácil atualização e análise. Ele também implementa práticas de validação com `Great Expectations` para assegurar a qualidade dos dados antes de análises avançadas.
