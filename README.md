# Testes A/B
## Introdução
Este será uma breve demonstração de como testes A/B podem ser utilizados em situações de negócios. Os códigos, cálculos e explicações adicionais estão localizados em [ab-testing.ipynb](https://github.com/brenosakaguti/ab-testing-study/blob/main/ab-testing.ipynb) (em inglês)

## Índice
* [Teste 1: Taxa de Conversão](#teste-1-taxa-de-conversão)
* [Teste 2: Valor de Vendas](#teste-2-valor-de-vendas)
* [Teste 3: Múltiplas Opções](#teste-3-múltiplas-opções)

# Teste 1: Taxa de Conversão
## Caso de Negócio
Neste cenário, analisamos dados de um *website* de *e-commerce* que está considerando uma mudança em seu *design* de *webpage*. No *design* anterior, o *website* tinha uma taxa de conversão de visitantes de 13%, e espera-se que a mudança de *design* aumente a taxa de conversão para 15%.

Nossa tarefa é descobrir quantas amostras de dados seriam necessárias para concluir se a mudança de *design* foi efetiva, e, uma vez coletados os dados, realizar o teste para confirmar o resultado.

## Dados
Os dados para o teste vieram na forma de uma tabela contendo várias informações sobre cada usuário do *site*. Para os propósitos do teste, apenas a taxa de conversão foi considerada, mas os outros parâmetros foram usados para filtrar os dados e se certificar que não haviam duplicatas ou dados errôneos.

![tabela de dados](/images/tabela1.png)

*A tabela de dados*

## Tamanho do Efeito e Poder
De acordo com as especificações do estudo, o resultado esperado é um aumento da taxa de conversão de 13% para 15%, o que equivale a um *effect size* de 0,058. Usando um Poder de 80% e nível de significância de 95%, calculamos que o número de pontos de dados necessários para observar o efeito é 4720. Esse foi o número de observações utilizado durante o resto do teste.

## Teste de Hipótese
Usando os dados obtidos, foi realizado um Teste Z entre os grupos controle e tratamento, cada um com 4720 observações.

O teste resultou em um Valor-p de 0,273, maior que o valor alvo para o teste de 0,05. Isso significa que o resultado não foi estatisticamente distinto, ou seja, o novo *design* do *website* não fez diferença na taxa de conversão de clientes.

# Teste 2: Valor de Vendas
## Caso de Negócio
Um outro *website* de *e-commerce* apresenta uma questão diferente. Anteriormente, o *website* necessitava que o cliente preencha todas as informações do cartão de crédito para realizar a compra, mas os desenvolvedores estão trabalhando em uma maneira de preencher os dados automaticamente. No interim, foi realizado um teste para ver se o novo sistema teve um impacto significativo nas vendas.

Originalmente, o *website* tinha uma média de vendas de $1800 por cliente, e o objetivo é de aumentar as vendas em 1%, ou seja, uma média de $1818 por cliente.

## Dados
Para este teste, foram fornecidos dados de mais de 45 mil compras realizadas no site, categorizados pelo tipo de preenchimento utilizado (automático ou manual). O grupo A, de clientes usando preenchimento manual, serve como grupo controle para o experimento, enquanto o grupo B, usando preenchimento automático, será o grupo de tratamento.

![tabela de dados](/images/tabela2.png)

*A tabela de dados*

## Tamanho de Efeito e Poder
O objetivo da mudança de método de compra é de aumentar o valor médio de vendas de $1800 para $1818. Usando o grupo controle para estimar a variância, calculamos por meio do D de Cohen que o tamanho de efeito é 0,013.

Calculando novamente o número de observações necessárias para um teste de poder 80% e significância 95%, obtivemos um número necessário de 90.725. Isso é muito mais que os dados que temos, aproximadamente 23.000 para cada grupo.

Com o número de observações que temos, a chance de observar o efeito esperado, se ele existir, é de apenas 29%. Mesmo assim, como obter mais dados seria difícil, vamos trabalhar com o que temos por enquanto.

## Teste de Hipótese
A hipótese a testar é um aumento no valor médio de vendas. Para isso, vamos usar o Teste T de Student. Primeiro, vamos se certificar que o erro do valor médio segue uma distribuição normal. Para isso, tomamos algumas amostras em grupos de 1000 observações e tomamos suas médias.

![histograma](/images/hist1.png)

*Histograma das médias das amostras*

Como a distribuição aparenta ser próxima de uma normal, prosseguimos com o teste.

O Teste T resultou em um Valor-P de 0,321, bem maior que o *alpha* determinado de 0,05. Isso significa que não há diferença significativa entre o desempenho do sistema de compras com preenchimento automático ou manual. Esse resultado era esperado, pois o suposto efeito é muito pequeno, e o número de observações não era suficiente para realizar um teste com alto poder.

O pequeno tamanho de efeito é visivelmente observável ao plotar um histograma das vendas. As duas distribuições são quase identicas, e um conjunto de dados muito grande seria necessário para encontrar tal efeito.

![histograma de vendas](/images/hist2.png)

*Histograma das vendas, separado por grupos)*

# Teste 3: Múltiplas Opções
## Caso de Negócio
Neste caso, o cliente seria a *Montana State University* (MSU). A universidade reparou que, no *website* da biblioteca, o botão "Interact" era clicado muito menos que os outros, e suspeitaram que isso se devia ao fato de alunos não entenderem o propósito do botão, ou que o texto fosse vago demais. Para testar esta hipótese, foi realizado um teste A/B/n por um determinado período de tempo, onde qualquer visitante do *website* era aleatoriamente redirecionado a uma variante da página. O grupo controle viria a página original, com o botão "Interact", enquanto outros viriam uma versão alternativa, designadas "Connect", "Learn", "Help" ou "Services".

## Dados
Os dados do teste vêm na forma de planilhas contendo informações tais como o número de visitantes de cada página, o número total de cliques que a página recebeu e quantos cliques cada elemento da página foram registrados. No caso, estamos interessados em cliques no botão "Interact" e suas respectivas variações, então os dados de cada planilha foram compilados em uma única tabela.

![tabela de cliquees em webpages](/images/tabela_msu.png)

*Tabela de dados*

Com os dados que temos, há duas métricas possíveis a serem maximizadas: o número de cliques no botão por visitante do *website*, ou o número de cliques do botão dividido pelo número total de cliques. A decisão de que indicador é o mais importante depende do problema a ser resolvido. Por exemplo, se for assumido que o principal problema é uma alta *bounce rate*, isto é, que alunos que acessam a página rapidamente saem sem clicar, então a taxa de cliques por visitante seria uma prioridade a maximizar.

## Teste de Hipóteses
Testes foram realizados usando as duas métricas, clique/visitante e clique/total. Para começar, foi realizado um teste de chi-quadrado para determinar se existe um efeito real ou as diferenças poderiam ser explicadas por aleatoriedade. Ao calcular a tabela de contingência para os dados, foi optido um valor-p de 0, ou seja, é extremamente improvável que as diferenças em *click-through rate* sejam causados por um artefato aleatório, e existe um efeito real dependente do texto nos botões.

Após verificar que o efeito existe, foram realizados testes-Z entre o grupo controle e cada uma das variantes. Os valores-p resultantes foram então corrigidos usando o método de Bonferroni.

![tabela de cliques por visitantes](/images/tabela_msu2.png)

*Tabela de cliques por visitante*

![tabela de cliques por total](/images/tabela_msu3.png)

*Tabela de cliques por cliques totais*

Todas as variantes exceto "Learn" tiveram um resultado estatisticamente significativo em âmbas as métricas. Qual variante é a melhor, porém, depende do aspecto que se deseja maximizar. A variante "Services" teve a maior taxa de cliques/visitante, enquanto "Connect" teve maior cliques/total.
