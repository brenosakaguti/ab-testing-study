# Testes A/B
## Introdução
Este será uma breve demonstração de como testes A/B podem ser utilizados em situações de negócios. Os códigos, cálculos e explicações adicionais estão localizados em [ab-testing.ipynb](https://github.com/brenosakaguti/ab-testing-study/blob/main/ab-testing.ipynb) (em inglês)

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

O Teste T resultou em um Valor-P de 0,321.

