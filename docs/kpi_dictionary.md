# Dicionário de KPIs

Este documento descreve os principais indicadores utilizados no dashboard do projeto Business Performance Dashboard — Power BI.

## 1. KPIs executivos

| KPI | Descrição | Fórmula conceitual | Finalidade |
|---|---|---|---|
| Receita Total | Valor total gerado pelas vendas | Unidades vendidas × Preço do produto | Medir o volume financeiro vendido |
| Lucro Bruto | Resultado antes de despesas operacionais | Receita Total − Custo Total | Medir contribuição bruta das vendas |
| Margem Bruta % | Percentual da receita que permanece como lucro bruto | Lucro Bruto ÷ Receita Total | Avaliar rentabilidade |
| Unidades Vendidas | Quantidade total de unidades vendidas | Soma de `Sales[Units]` | Medir volume de vendas |
| Total de Vendas | Quantidade de registros de venda | Contagem de linhas da tabela `Sales` | Medir volume transacional |
| Ticket Médio por Linha | Receita média por linha de venda | Receita Total ÷ Total de Vendas | Avaliar valor médio por registro de venda |
| Produtos Vendidos | Quantidade de produtos distintos vendidos | Contagem distinta de `Product_ID` | Medir variedade de produtos vendidos |
| Lojas Ativas | Quantidade de lojas com vendas registradas | Contagem distinta de `Store_ID` | Medir abrangência da operação |

## 2. KPIs de produto

| KPI | Descrição | Finalidade |
|---|---|---|
| Receita por Produto | Receita gerada por cada produto | Identificar produtos líderes em faturamento |
| Lucro por Produto | Lucro bruto gerado por cada produto | Identificar produtos mais rentáveis |
| Margem por Produto | Margem bruta percentual por produto | Identificar produtos com baixa ou alta rentabilidade |
| Unidades por Produto | Quantidade vendida por produto | Avaliar volume comercial |
| Participação na Receita | Percentual da receita concentrado em produto ou categoria | Avaliar dependência de determinados produtos |
| Participação no Lucro | Percentual do lucro concentrado em produto ou categoria | Avaliar contribuição real para o resultado |

## 3. KPIs de loja

| KPI | Descrição | Finalidade |
|---|---|---|
| Receita por Loja | Receita gerada por cada loja | Comparar desempenho comercial entre lojas |
| Lucro por Loja | Lucro bruto gerado por cada loja | Comparar contribuição financeira entre lojas |
| Margem por Loja | Margem bruta percentual por loja | Avaliar eficiência econômica |
| Receita por Cidade | Receita gerada por cidade | Identificar concentração geográfica |
| Receita por Tipo de Localização | Receita por `Store_Location` | Avaliar impacto da localização no desempenho |
| Receita por Loja Ativa | Receita média considerando lojas com venda | Comparar produtividade média |

## 4. KPIs de estoque

| KPI | Descrição | Fórmula conceitual | Finalidade |
|---|---|---|---|
| Estoque Total | Quantidade total disponível em estoque | Soma de `Stock_On_Hand` | Medir disponibilidade total |
| Produtos com Estoque Zerado | Quantidade de produtos com estoque zero | Contagem de produtos com `Stock_On_Hand = 0` | Identificar risco de ruptura |
| Combinações Loja-Produto | Total de combinações entre loja e produto no estoque | Contagem de linhas da tabela `Inventory` | Medir cobertura do estoque |
| Combinações com Estoque Zerado | Combinações loja-produto com estoque zero | Contagem de linhas com `Stock_On_Hand = 0` | Identificar pontos de indisponibilidade |
| Percentual de Estoque Zerado | Proporção de combinações loja-produto sem estoque | Combinações com estoque zero ÷ combinações totais | Avaliar exposição a ruptura |
| Giro Simplificado de Estoque | Relação entre unidades vendidas e estoque atual | Unidades vendidas ÷ estoque disponível | Avaliar movimentação relativa do estoque |

## 5. Observação sobre estoque

O indicador de giro de estoque neste projeto será tratado como **giro simplificado**, pois o dataset possui estoque atual, mas não possui histórico completo de entradas, saídas e estoque médio.

Em uma operação real, o giro de estoque idealmente deveria considerar:

- estoque médio;
- período de análise;
- entradas de mercadoria;
- saídas;
- rupturas;
- reposições.

Como essas informações não estão disponíveis, a análise de estoque será interpretada como diagnóstico aproximado, não como cálculo contábil ou logístico completo.