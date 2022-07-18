# Testes A/B
## Introdução
Este será uma breve demonstração de como testes A/B podem ser utilizados em situações de negócios. Os códigos, cálculos e explicações adicionais estão localizados em [ab-testing.ipynb](https://github.com/brenosakaguti/ab-testing-study/blob/main/ab-testing.ipynb) (em inglês)

# Teste 1: Taxa de Conversão
## Caso de negócio
Neste cenário, analisamos dados de um *website* de *e-commerce* que está considerando uma mudança em seu *design* de *webpage*. No *design* anterior, o *website* tinha uma taxa de conversão de visitantes de 13%, e espera-se que a mudança de *design* aumente a taxa de conversão para 15%.

Nossa tarefa é descobrir quantas amostras de dados seriam necessárias para concluir se a mudança de *design* foi efetiva, e, uma vez coletados os dados, realizar o teste para confirmar o resultado.

## Dados
Os dados para o teste vieram na forma de uma tabela contendo várias informações sobre cada usuário do *site*. Para os propósitos do teste, apenas a taxa de conversão foi considerada, mas os outros parâmetros foram usados para filtrar os dados e se certificar que não haviam duplicatas ou dados errôneos.

![tabela de dados](/images/tabela1.png)

*A tabela de dados*

## Tamanho do Efeito e Poder
De acordo com as especificações do estudo, o resultado esperado é um aumento da taxa de conversão de 13% para 15%, o que equivale a um *effect size* de 0,058. Usando um Poder de 80% e nível de significância de 95%, calculamos que o número de pontos de dados necessários para observar o efeito é 4720. Esse foi o número de observações utilizado durante o resto do teste.

## Teste de hipótese
Usando os dados obtidos, foi realizado um Teste Z entre os grupos controle e tratamento, cada um com 4720 observações.
