# Clusterização de Cientes de um E-commerce

O objetivo aqui é clusterizar os clientes de um e-commerce que atua em 37 países. Isso será feito a partir de uma tabela RFM, que também será montada e tratada aqui.

A Clusterização se trata de uma separação em grupos ainda não existentes, mas que é feita de acordo com características em comum que observamos nos dados trabalhados. Nesse caso, se trata de clientes e suas compras. 
Antes de clusterizar, precisaremos criar uma tabela RFM (Recência, Frequência, Monetário), que nos dará as informações mais importantes de cada cliente para o nosso negócio. A recência nos diz o tempo que passou desde sua última compra, a frequência nos diz quantas vezes esse cliente já comprou e o monetário nos diz o valor médio de compra dele.

## Bibliotecas:
1. Pandas.
2. Matplotlib.
3. Plotly.
4. Scikit-Learn.
5. Yellowbrick.

## Análises iniciais:
1. Percebemos que há dados nulos em colunas importantes, como *CostumerID*, que é a coluna de identificação. Vale lembrar que, como o foco está nos clientes, é impossível trabalhar com queles que não podem ser identificados.
2. As datas não estão no formato certo, o que pode atrapalhar sua utilização
3. Percebemos também a presença de dados duplucados.
4. Além disso, há valores negativos para quantidade e preço, o que não pode condizer com a realidade. E essas variáveis também apresentam indícios de outliers, que podem influenciar nosso resultado final.

## Tratamento dos Dados:
1. Excluímos as linhas sem *CostumerID* e todas as entradas foram embora.
2. Tratamos a quantidade e o preço atravez de filtros.
3. Dropamos os dados duplicados.
4. Corrigimos o tipo de dado das datas e na coluna *CostumerID*.
5. Dropamos os outliers mais discrepantes, ao percebermos que se tratam de poucos dados.
6. Incluimos no dataframe uma coluna com o valor total gasto em cada compra, construída com a multiplicação da quantidade pelo preço unitário.
7. Por fim, criamos uma variável de referência com uma data próxima à última data do dataframe.
Esses dois últimos passos foram feitos para auxiliar na criação da tabela RFM.

## Visualizações:
1. Mostramos, em um gráfico de barras, o top 10 de países que venderam mais, de acordo com o valor das vendas.
2. Também apresentamos os 10 produtos mais vendidos.
3. Para mostrar a sazonalidade, utilizamos um gráfico de linhas, com o valor total das vendas ao longo do tempo.
4. Por fim, mostramos o valor das vendas a cada mÊs, com um gráfico de barras.
5. (Tentamos criar um gráfico com as vendas por mês, separadas por país, mas falhou. Estou aberta a sugestões.)

## Tabela RFM:
1. A tabela foi toda criada a partir do *groupby()*, que agrupa dados da forma que escolhemos.
2. Verificamos a existência de um outlier bastante descrepante no Monetário, então utilizamos um filtro para excluí-lo. Apesar disso, ainda existiam outros valores (menos) descrepantes ali, então criamos um teto equivalente ao valor máximo entre os primeiros 95% dos dados, de forma que qualquer valor acima dele fosse modificado para esse teto.
3. O último passo foi normalizar, para evitar que o modelo seja influÊnciados pelas diferenças de valores entre as colunas.

## Clusterização:
1. Utilizamos K-Means, DBSCAN, Clusterização Hierárquica e Mean Shift como opções para clusterizar. Cada um trabalha de um modo específico, e podemos compará-los de acordo com métricas de performance.
2. As métricas utilizadas foram Silhouette, Davies Bouldin e Calinski Harabasz.
3. O modelo que melhor performou, de acordo com as métricas e os gráficos tridimencionais, foi o K-Means, que separa os grupos de acordo com a "vizinhança dos dados". Esse processo pode ser melhor entendido nos gráficos apresentados.

## Conclusão:
Foi possível identificarmos 4 clusters. Minha interpretação foi de que os grupos são:
1. De possíveis novos clientes;
2. De possíveis churn;
3. Clientes de compras recorrentes, com ítens de baixo custo;
4. Clientes com compras esporádicas, mas com ítens de alto custo.

A partir daí, o e-commerce pode bolar estratégias de marketing específicas para cada um dos grupos e, assim, melhorar suas vendas.
