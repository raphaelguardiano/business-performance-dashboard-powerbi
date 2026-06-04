# Medidas DAX

Este documento registra as medidas DAX previstas e criadas no projeto **Business Performance Dashboard — Power BI**.

As medidas serão atualizadas conforme forem implementadas no Power BI Desktop.

---

## 1. Observação inicial

As medidas abaixo foram planejadas com base na estrutura esperada do dataset Maven Toys.

Tabelas consideradas:

* `Sales`
* `Products`
* `Stores`
* `Inventory`
* `Calendar`

Campos principais considerados:

* `Sales[Units]`
* `Sales[Product_ID]`
* `Sales[Store_ID]`
* `Products[Product_Price]`
* `Products[Product_Cost]`
* `Products[Product_Name]`
* `Products[Product_Category]`
* `Stores[Store_Name]`
* `Inventory[Stock_On_Hand]`
* `Calendar[Date]`

Algumas medidas podem precisar de pequenos ajustes caso o Power BI importe os nomes das tabelas ou colunas com alguma diferença.

---

## 2. Medidas comerciais principais

### Total Units

```DAX
Total Units =
SUM ( Sales[Units] )
```

Descrição: soma total de unidades vendidas.

---

### Total Sales Lines

```DAX
Total Sales Lines =
COUNTROWS ( Sales )
```

Descrição: conta a quantidade de linhas de venda registradas na tabela `Sales`.

---

### Total Revenue

```DAX
Total Revenue =
SUMX (
    Sales,
    Sales[Units] * RELATED ( Products[Product_Price] )
)
```

Descrição: calcula a receita total multiplicando unidades vendidas pelo preço do produto.

---

### Total Cost

```DAX
Total Cost =
SUMX (
    Sales,
    Sales[Units] * RELATED ( Products[Product_Cost] )
)
```

Descrição: calcula o custo total multiplicando unidades vendidas pelo custo do produto.

---

### Gross Profit

```DAX
Gross Profit =
[Total Revenue] - [Total Cost]
```

Descrição: calcula o lucro bruto pela diferença entre receita total e custo total.

---

### Gross Margin %

```DAX
Gross Margin % =
DIVIDE ( [Gross Profit], [Total Revenue] )
```

Descrição: calcula a margem bruta percentual.

Observação: formatar esta medida como porcentagem no Power BI.

---

### Average Revenue per Sale Line

```DAX
Average Revenue per Sale Line =
DIVIDE ( [Total Revenue], [Total Sales Lines] )
```

Descrição: calcula a receita média por linha de venda.

---

### Distinct Products Sold

```DAX
Distinct Products Sold =
DISTINCTCOUNT ( Sales[Product_ID] )
```

Descrição: calcula a quantidade de produtos distintos vendidos.

---

### Active Stores

```DAX
Active Stores =
DISTINCTCOUNT ( Sales[Store_ID] )
```

Descrição: calcula a quantidade de lojas com vendas registradas.

---

## 3. Medidas de participação

### Revenue Share %

```DAX
Revenue Share % =
DIVIDE (
    [Total Revenue],
    CALCULATE ( [Total Revenue], ALL ( Products ) )
)
```

Descrição: calcula a participação da receita no contexto selecionado em relação ao total geral de produtos.

Observação: formatar esta medida como porcentagem no Power BI.

---

### Profit Share %

```DAX
Profit Share % =
DIVIDE (
    [Gross Profit],
    CALCULATE ( [Gross Profit], ALL ( Products ) )
)
```

Descrição: calcula a participação do lucro bruto no contexto selecionado em relação ao total geral de produtos.

Observação: formatar esta medida como porcentagem no Power BI.

---

### Category Revenue Share %

```DAX
Category Revenue Share % =
DIVIDE (
    [Total Revenue],
    CALCULATE ( [Total Revenue], ALL ( Products[Product_Category] ) )
)
```

Descrição: calcula a participação da receita por categoria em relação ao total geral das categorias.

Observação: formatar esta medida como porcentagem no Power BI.

---

## 4. Medidas temporais

### Revenue YTD

```DAX
Revenue YTD =
TOTALYTD (
    [Total Revenue],
    Calendar[Date]
)
```

Descrição: calcula a receita acumulada no ano.

---

### Profit YTD

```DAX
Profit YTD =
TOTALYTD (
    [Gross Profit],
    Calendar[Date]
)
```

Descrição: calcula o lucro bruto acumulado no ano.

---

### Revenue Previous Month

```DAX
Revenue Previous Month =
CALCULATE (
    [Total Revenue],
    DATEADD ( Calendar[Date], -1, MONTH )
)
```

Descrição: calcula a receita do mês anterior.

---

### Revenue MoM %

```DAX
Revenue MoM % =
DIVIDE (
    [Total Revenue] - [Revenue Previous Month],
    [Revenue Previous Month]
)
```

Descrição: calcula a variação percentual da receita em relação ao mês anterior.

Observação: formatar esta medida como porcentagem no Power BI.

---

## 5. Medidas de estoque

### Total Stock On Hand

```DAX
Total Stock On Hand =
SUM ( Inventory[Stock_On_Hand] )
```

Descrição: soma o estoque disponível registrado na tabela `Inventory`.

---

### Products with Zero Stock

```DAX
Products with Zero Stock =
CALCULATE (
    DISTINCTCOUNT ( Inventory[Product_ID] ),
    Inventory[Stock_On_Hand] = 0
)
```

Descrição: calcula a quantidade de produtos distintos com estoque igual a zero.

---

### Store-Product Combinations

```DAX
Store-Product Combinations =
COUNTROWS ( Inventory )
```

Descrição: conta o total de combinações loja-produto existentes na tabela de estoque.

---

### Zero Stock Combinations

```DAX
Zero Stock Combinations =
CALCULATE (
    COUNTROWS ( Inventory ),
    Inventory[Stock_On_Hand] = 0
)
```

Descrição: conta quantas combinações loja-produto possuem estoque igual a zero.

---

### Zero Stock %

```DAX
Zero Stock % =
DIVIDE (
    [Zero Stock Combinations],
    [Store-Product Combinations]
)
```

Descrição: calcula o percentual de combinações loja-produto com estoque zerado.

Observação: formatar esta medida como porcentagem no Power BI.

---

### Simplified Stock Turnover

```DAX
Simplified Stock Turnover =
DIVIDE (
    [Total Units],
    [Total Stock On Hand]
)
```

Descrição: calcula uma relação simplificada entre unidades vendidas e estoque atual.

Observação importante: esta medida deve ser interpretada como **giro simplificado**, pois o dataset possui estoque atual, mas não possui histórico completo de estoque médio, entradas, saídas e reposições.

---

## 6. Medidas de ranking

### Product Revenue Rank

```DAX
Product Revenue Rank =
RANKX (
    ALL ( Products[Product_Name] ),
    [Total Revenue],
    ,
    DESC
)
```

Descrição: cria o ranking de produtos por receita total.

---

### Store Revenue Rank

```DAX
Store Revenue Rank =
RANKX (
    ALL ( Stores[Store_Name] ),
    [Total Revenue],
    ,
    DESC
)
```

Descrição: cria o ranking de lojas por receita total.

---

## 7. Medidas auxiliares recomendadas

As medidas abaixo podem ser úteis no desenvolvimento do dashboard.

### Average Gross Profit per Sale Line

```DAX
Average Gross Profit per Sale Line =
DIVIDE ( [Gross Profit], [Total Sales Lines] )
```

Descrição: calcula o lucro bruto médio por linha de venda.

---

### Average Units per Sale Line

```DAX
Average Units per Sale Line =
DIVIDE ( [Total Units], [Total Sales Lines] )
```

Descrição: calcula a média de unidades vendidas por linha de venda.

---

### Revenue per Active Store

```DAX
Revenue per Active Store =
DIVIDE ( [Total Revenue], [Active Stores] )
```

Descrição: calcula a receita média por loja ativa.

---

### Gross Profit per Active Store

```DAX
Gross Profit per Active Store =
DIVIDE ( [Gross Profit], [Active Stores] )
```

Descrição: calcula o lucro bruto médio por loja ativa.

---

### Stock Coverage Ratio

```DAX
Stock Coverage Ratio =
DIVIDE (
    [Total Stock On Hand],
    [Total Units]
)
```

Descrição: calcula uma relação simplificada entre estoque atual e unidades vendidas.

Observação: assim como o giro simplificado, esta medida não representa cobertura real de estoque em dias, pois o dataset não possui histórico de estoque médio nem vendas diárias por posição de estoque.

---

## 8. Medidas que podem ser criadas depois

As medidas abaixo não precisam ser criadas no início. Elas podem ser adicionadas se forem úteis durante a construção das páginas do dashboard.

### Revenue by Selected Context

```DAX
Revenue by Selected Context =
[Total Revenue]
```

Descrição: medida auxiliar para uso em visuais quando for necessário reforçar o contexto de filtro.

---

### Gross Profit by Selected Context

```DAX
Gross Profit by Selected Context =
[Gross Profit]
```

Descrição: medida auxiliar para uso em visuais quando for necessário reforçar o contexto de filtro.

---

### Low Margin Flag

```DAX
Low Margin Flag =
IF (
    [Gross Margin %] < 0.20,
    "Baixa margem",
    "Margem adequada"
)
```

Descrição: classifica produtos, categorias ou lojas com margem abaixo de 20%.

Observação: o limite de 20% é uma regra analítica inicial e pode ser ajustado depois da análise da distribuição real das margens.

---

### Zero Stock Flag

```DAX
Zero Stock Flag =
IF (
    [Total Stock On Hand] = 0,
    "Estoque zerado",
    "Com estoque"
)
```

Descrição: classifica itens conforme disponibilidade de estoque.

---

## 9. Cuidados de interpretação

Durante o uso das medidas, observar os seguintes pontos:

* Receita Total não deve ser interpretada como lucro.
* Lucro Bruto não considera despesas operacionais, impostos, frete ou custos administrativos.
* Margem Bruta % mede rentabilidade bruta, não margem líquida.
* Estoque atual não representa estoque médio histórico.
* Giro Simplificado de Estoque é apenas uma aproximação analítica.
* Produtos com maior receita não são necessariamente os mais rentáveis.
* Lojas com menor receita não devem ser consideradas ruins sem avaliar localização, maturidade e contexto.
* Toda conclusão deve estar vinculada aos dados disponíveis.

---

### 10. Status das medidas

Status atual:

- Medidas planejadas: sim.
- Medidas criadas no Power BI: sim.
- Medidas validadas em cartões de teste: sim.
- Medidas validadas no dashboard final: ainda não.
