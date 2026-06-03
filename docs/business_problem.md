# Problema de Negócio

## 1. Contexto

A Maven Toys é uma rede varejista fictícia de brinquedos com operação distribuída em diferentes lojas, cidades e tipos de localização.

A empresa possui dados de vendas, produtos, lojas, calendário e estoque. Porém, esses dados precisam ser organizados em uma visão analítica integrada para apoiar decisões comerciais e operacionais.

## 2. Problema central

A empresa precisa entender seu desempenho comercial e operacional de forma consolidada, identificando quais produtos, categorias, lojas e cidades mais contribuem para o resultado.

Além disso, é necessário avaliar se existem sinais de baixa rentabilidade, concentração de receita, produtos com margem reduzida, estoque parado ou risco de ruptura.

## 3. Pergunta principal de negócio

Como a Maven Toys pode acompanhar seu desempenho de vendas, lucro, margem, lojas, produtos e estoque de forma integrada para identificar oportunidades de melhoria comercial e operacional?

## 4. Perguntas específicas

### Vendas e rentabilidade

- Qual foi a receita total no período analisado?
- Qual foi o lucro bruto total?
- Qual foi a margem bruta geral?
- Quantas unidades foram vendidas?
- Quais categorias mais contribuem para receita?
- Quais categorias mais contribuem para lucro?
- Existem categorias com alta receita, mas baixa margem?

### Produtos

- Quais produtos são campeões de venda?
- Quais produtos geram mais lucro?
- Quais produtos vendem muito, mas apresentam margem baixa?
- Existe concentração de receita em poucos produtos?
- Existem produtos com baixa contribuição para o resultado?

### Lojas e localização

- Quais lojas apresentam melhor desempenho em receita?
- Quais lojas apresentam melhor desempenho em lucro?
- Quais cidades concentram maior resultado?
- O tipo de localização da loja influencia o desempenho?
- Existem lojas com baixa margem apesar de alto faturamento?

### Tempo

- Como a receita evoluiu ao longo do tempo?
- Existe sazonalidade mensal?
- Quais meses tiveram maior volume de vendas?
- A margem se manteve estável ao longo do período?

### Estoque

- Quais produtos possuem maior estoque disponível?
- Existem produtos com estoque zerado?
- Existem produtos com alto estoque e baixa venda?
- Existem produtos com alta venda e baixo estoque?
- Quais lojas apresentam maior exposição a risco de ruptura?

## 5. Hipóteses iniciais

As hipóteses abaixo orientarão a análise, mas não devem ser tratadas como conclusão antes da validação no Power BI.

| Hipótese | Como testar |
|---|---|
| Algumas categorias geram muita receita, mas não necessariamente alto lucro | Comparar Receita Total, Lucro Bruto e Margem Bruta % por categoria |
| Produtos campeões de venda podem apresentar margem baixa | Cruzar unidades vendidas, receita, lucro e margem por produto |
| O desempenho varia conforme o tipo de localização da loja | Comparar KPIs por `Store_Location` |
| Algumas cidades concentram parcela relevante da receita | Criar ranking de receita e lucro por cidade |
| Pode haver risco de ruptura em produtos de alta venda com baixo estoque | Cruzar unidades vendidas com `Stock_On_Hand` |
| Pode haver estoque parado em produtos com alto estoque e baixa venda | Cruzar estoque atual com vendas acumuladas |
| Lojas mais antigas podem ter desempenho diferente das mais novas | Comparar KPIs com `Store_Open_Date` |

## 6. Resultado esperado

O resultado esperado é um dashboard executivo que permita ao usuário:

- monitorar indicadores principais;
- identificar categorias e produtos relevantes;
- comparar desempenho entre lojas;
- avaliar comportamento por localização;
- detectar riscos de estoque;
- apoiar decisões práticas de negócio.

## 7. Limitações conhecidas

Este projeto utiliza um dataset público e fictício. Portanto, algumas análises possuem limitações:

- não há dados de despesas operacionais;
- não há dados de impostos;
- não há dados de frete;
- não há histórico detalhado de movimentação de estoque;
- o estoque representa uma posição atual, não estoque médio histórico;
- não há dados de cliente final;
- não há metas comerciais fornecidas pela empresa.

Por isso, os resultados devem ser interpretados como análise de desempenho comercial e operacional com base nas variáveis disponíveis.