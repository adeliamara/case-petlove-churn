# Visão geral

Este código contém funções para análise de dados de assinaturas. Ele utiliza as bibliotecas `pandas` e `matplotlib` para realizar as operações de leitura e limpeza dos dados, cálculo de métricas e geração de visualizações.

1. Visão geral

Nessa etapa, foi necessário fazer uma limpeza dos dados de data. Notei explorando os dados que os padrões de data eram com apenas dois dígitos. Por exemplo, 1999 seria apenas 99. Isso pode gerar diversos problemas se não for bem tratado. Assim, ao analisar os dados observe que aniversários eram todos do século 20. Enquanto created_at e deleted_at do seculo 21. Assim, fiz uma limpeza desses dados e os coloquei no padrão YYYY-MM-DD HH:MM.

Para calcular o `churn` foi preciso verificar o número de usuários ativos até o mês que está sendo analisado. Ou, usuários criados até o último mês com status ativos ou com deleted_at após o mes atual (pois esses terão status canceled, mas isso não significa que no mês que nos referimos ele já estava cancelado.)
Por exemplo, se o mês analisado é mar/2020, então devo considerar todos usuários criados até fevereiro que estão ativos ou que canceleram a assinatura em meses posteriores a março.

O churn, foi por tanto, a razão dos usuários que canceleram em março em relação aos usuários ativos.

Foi também gerado um gráfico de pizza agrupando os status disponíveis.

2. Tempo entre o cancelamento e a última compra.

Aqui só interessa os usuários que possuem data de cancelamento. Por isso, foi utilizado a função `filter_missing_values` para tratar o df apenas com esses usários.

Após isso, foi criado uma nova coluna `time_since_last_purchase` com o tempo entre a data de criação e 

Foi feito a divisão de classes, onde era calculado a amplitude analisada (maximo - minimo de tempo) e dividido número de classes (chamado de num_bins no codigo).

Foi criado algumas funções auxiliares para restringir os intervalos de datas e fazer analises mais apronfudadas dos intervalos mais críticos.

3. Marketing source

Foi feito primeiro uma análise explorátoria dos dados, verificando os canais, a quantidade de ativos, pausados e canceladas.

Depois, assim como foi feito inicialmente, foi avaliado a evolução do `churn` mensal, mas aqui foi agrupado por canal.

4. Ticket médio

O código fornecido realiza uma análise do ticket médio dos clientes e sua relação com a taxa de cancelamento. Ele divide o conjunto de dados em intervalos de ticket médio e calcula a representatividade de cada intervalo, ou seja, a proporção de clientes que se enquadram em cada faixa de ticket médio. Em seguida, ele calcula a taxa de cancelamento para cada faixa de ticket médio.

Para isso, o código possui as seguintes funções:

`calculate_avg_ticket_range`: Calcula os intervalos de ticket médio e atribui a cada registro do DataFrame o intervalo correspondente.
`calculate_representativity`: Calcula a representatividade de cada intervalo de ticket médio com base no DataFrame fornecido.
`calculate_churn_by_avg_ticket_range`: Calcula a taxa de cancelamento para cada intervalo de ticket médio.
plot_data: Plota um gráfico mostrando a representatividade e a taxa de cancelamento por intervalo de ticket médio.
No final do código, a função calculate_rate_by_ticket_medio é chamada, que engloba todas as etapas anteriores. Ela recebe o DataFrame como entrada, executa as etapas de cálculo e plotagem dos dados, fornecendo assim uma análise visual da relação entre o ticket médio e a taxa de cancelamento.

5. Cancelamento por estado

O código fornecido realiza uma análise da taxa de churn (taxa de cancelamento) por estado para um determinado conjunto de dados. Ele possui as seguintes funções:

`calculate_churn_rate_by_state`: Calcula a taxa de churn por estado, dividindo o número de registros cancelados pelo número total de registros para cada estado. O resultado é multiplicado por 100 para obter a taxa em porcentagem.

`calculate_representativity`: Calcula a representatividade de cada estado, ou seja, a proporção de registros que pertencem a cada estado em relação ao número total de registros no conjunto de dados. O resultado é multiplicado por 100 para obter a representatividade em porcentagem.

`create_churn_dataframe`: Cria um DataFrame com duas colunas: "Churn Rate (%)" e "Representatividade (%)", que são preenchidas com os valores de churn por estado e representatividade, respectivamente. O DataFrame é ordenado em ordem decrescente de churn rate.

`plot_churn_by_state`: Plota um gráfico de barras mostrando a taxa de churn por estado e uma linha pontilhada que representa a representatividade de cada estado.


6. Verificando o recency dos clientes ativos


Por fim é feito uma distribuição de frequencia para verificar quanto tempo os clientes ativos estão sem fazer compras. 