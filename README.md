# Business Performance Dashboard — Power BI

## 1. Visão geral do projeto

Este projeto tem como objetivo construir um dashboard em Power BI para análise de desempenho comercial e operacional de uma rede varejista fictícia de brinquedos, utilizando o dataset Maven Toys.

A proposta é simular uma situação real de negócio em que uma empresa precisa acompanhar vendas, lucro, margem, desempenho por produto, desempenho por loja e situação de estoque para apoiar decisões gerenciais.

O foco do projeto não é apenas criar visualizações, mas transformar dados operacionais em diagnóstico, indicadores e recomendações práticas de negócio.

## 2. Problema de negócio

A Maven Toys possui dados distribuídos em diferentes tabelas, incluindo vendas, produtos, lojas, calendário e estoque.

Sem uma visão consolidada, torna-se mais difícil responder perguntas importantes, como:

- Quais categorias e produtos mais geram receita?
- Quais produtos mais contribuem para o lucro?
- Existem produtos com alto faturamento, mas baixa margem?
- Quais lojas e cidades apresentam melhor desempenho?
- O tipo de localização da loja influencia o resultado?
- Existem sinais de risco de ruptura ou estoque parado?

## 3. Objetivo

Criar um dashboard em Power BI que permita analisar:

- receita total;
- lucro bruto;
- margem bruta;
- unidades vendidas;
- desempenho por categoria;
- desempenho por produto;
- desempenho por loja;
- desempenho por cidade;
- desempenho por tipo de localização;
- situação de estoque.

## 4. Dataset

O dataset utilizado é o **Maven Toys**, disponibilizado pela Maven Analytics.

Arquivos utilizados no projeto:

- `sales.csv`
- `products.csv`
- `stores.csv`
- `inventory.csv`
- `calendar.csv`
- `data_dictionary.csv`

## 5. Ferramentas utilizadas

- Power BI Desktop
- Power Query
- DAX
- Git
- GitHub Desktop
- GitHub

## 6. Estrutura do projeto

```text
business-performance-dashboard-powerbi/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── docs/
│   ├── business_problem.md
│   ├── data_dictionary.md
│   ├── kpi_dictionary.md
│   ├── analysis_plan.md
│   └── insights_and_recommendations.md
│
├── powerbi/
│   └── business-performance-dashboard.pbix
│
├── images/
│
├── dax/
│   └── measures.md
│
├── README.md
└── LICENSE