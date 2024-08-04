Modelo criado utilizando os datasets do exemplo

Após criar o modelo de predição do estoque, como no tutorial, criei um modelo pra fazer a predição das vendas.
Para tanto, criei um campo calculado VENDAS, como sendo a [quantidade em estoque] - [ qualtidade em estoque na data anterior]. Utilizei a tranformação custom, com formulá rodando o PYthon (Pandas) abaixo:

#Ordenar o dataframe pela data
df = df.sort_values(by=["ID_PRODUTO",'DATA_EVENTO'])

#Calcular a nova coluna como a diferença do valor com o valor do dia anterior
df['VENDAS'] = df.groupby('ID_PRODUTO')['QUANTIDADE_ESTOQUE'].shift(1) - df.groupby('ID_PRODUTO')['QUANTIDADE_ESTOQUE'].shift(0)
df['VENDAS'] = df['VENDAS'].apply(lambda x: x if x >= 0 else 0)


Também criei um campo FATURAMENTO como sendo o campo VENDAS * PRECO.


OS valores de saída foram:
Avg. wQL 0.306
MAPE 0.875
WAPE 0.492
RMSE 6.445
MASE 0.743


