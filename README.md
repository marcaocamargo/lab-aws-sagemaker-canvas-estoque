# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

Bem-vindo ao desafio de projeto "Previsão de Estoque Inteligente na AWS com SageMaker Canvas".

## 🚀 Passo a Passo

### 1. Selecionando o Dataset

- Escolhi usar o dataset fornecido pela DIO na pasta `datasets` intitulado dataset-1000-com-preco-promocional-e-renovacao-estoque para projeção do projeto de **_Previsão de Estoque Inteligente na AWS com Sagemaker Canvas._**
> Acabei realizando o upload no Canvas com um nome mais simples:
![Imgur](https://imgur.com/Y9oMjiY.png)

### 2. Construindo e Treinando meu modelo

- Realizei a configuração inicial do meu modelo apontando como `target` a coluna QUANTIDADE_ESTOQUE.
> Essa é a versão 1 do modelo criado:
![Imgur](https://imgur.com/zqKZ4oI.png)

- Configurei o modelo selecionando o ID_PRODUTO como `ITEM ID` para identificação de valor único.
- O indicativo para a coluna que contém `timestamps` ele reconheu automáticamente, apenas mantive.
- Alterei para a projeção me mostrar o os 3 próximos dias em vez de somente 1.
- Adicionei para ele tomar como base os feriados nacionais no Brasil.
> Segue configurações realizadar:
![Imgur](https://imgur.com/QXneugO.png)

### 3. Analisando o modelo

- Após ajustes no modelo, tivemos as métricas em `Quick Build` um pouco altas, mesmo com treinamentos, mas mantive assim.
- Temos o `Avg wQL` que é a perda média ponderada de quantis, é uma previsão calculando como um todo a média de precisão de pontos de distribuição, formando o P10, P50 e P90. Quando mais baixo esse valor, mais preciso é o modelo.
- Temos o `MAPE` que é o erro percentual médio absoluto, que seria a diferença percentual entre o valor médio previsto com o valor real. O valor quanto mais próximo de `0`, melhor, sendo `MAPE=0` como um modelo perfeito e sem erros.
- O `WAPW` é o erro percentual absoluto ponderado, ond emede o desvio geral dos valores previstos em relação aos valores observados e é definido pela soma do erro absoluto normalizado pela soma da meta absoluta. Um valor mais baixo indica um modelo mais preciso com `WAPE=0` como um modelo perfeito e sem erros.
- O `RMSE` é a raiz quadrada dos erros quadráticos médios. Um `RMSE` mais baixo indica um modelo mais preciso com `RMSE=0` como um modelo perfeito e sem erros.
- O `MASE` é a média do erro absoluto da previsão normalizada pelo erro médio absoluto de um método simples de previsão de linha de base. Um valor mais baixo indica um modelo mais preciso com `MASE < 1` como um modelo estimado como melhor que a linha de base e um `MASE > 1` como um modelo estimado como pior que a linha de base.
> Resultado do meu modelo, mesmo o RMSE estando alto, foi o mais próximo que cheguei, **precisarai de mais tempo e treinamento.**
![Imgur](https://imgur.com/lZ5fZrm.png)

> Aqui conseguimos analisar também que as colunas `PRECO` com  `17,34%` e `HOLIDAY_BR` com `1,29%` tiveram impactos na projeção.
![Imgur](https://imgur.com/sNvTNVH.png)

### 4. Previsão Final

-   Usando o modelo treinado, fizemos as previsões de estoque.
-   Analisamos dois produtos para termos base e ideais.
-   Começando com o `Item 1014` onde temos uma demanda histórica dele iniciado em `61` e no dia seguinte já está em `51` e depois em `36` e as projeções para os 3 próximos dias em `P10, P50 e P90`
> Projeção em formato de tabela:
![Imgur](https://imgur.com/6Whiwes.png)

> Projeção em formato gráfico:
![Imgur](https://imgur.com/u6cJtJJ.png)

- Aqui temos o `Item 1021` onde temos uma demanda histórica dele iniciado em `73` e no dia seguinte já está em `55` e depois em `36` e as projeções para os 3 próximos dias em `P10, P50 e P90`
> Projeção em formato de tabela:
![Imgur](https://imgur.com/8IN0o9U.png)

> Projeção em formato gráfico:
![Imgur](https://imgur.com/zBllomf.png)

## Explicando P10, P50 e P90

- Esses quantis são usados ​​para levar em conta a incerteza das previsões. Por padrão, as previsões são geradas para 0,1 (P10), 0,5 (P50) e 0,9 (P90).
  - P10 LINHA ROSA (Reflete um cenário pessimista)
  - P50 LINHA VERDE(Reflete um cenário neutro)
  - P90 LINHA AMARELO(Reflete um cenário otimista)
