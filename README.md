# Desafio_Pyspark_Stone

#O script teve que ser feito via Google Colab, pois tive problemas com as configuração do Pycharm em minha máquina pessoal
#Tentei fazer o upload direto pelo Google Colab, para manter o visual de lá, porém recebi mensagem de erro e para tentar mais tarde =/

#Subi três script .ypnb:
1-DesafioStone_VersaoFinal.ipynb (Versão definitiva)
2-DesafioStone_VersaoFinal_Logs_adicionais.ipynb (Como o nome sugere, aqui mantive alguns logs adicionais de validação)
3-Desafio_Stone_VersaoInicial_Analises.ipynb (Script inicial com a aplicação das regras sem a utilização de classes e algumas análises de dados iniciais, utilizando a biblioteca Pandas como apoio

Definição de regras antes de criar o script:
1- Já que a definição do valor de distribuição dos bônus está em aberto, tomei como base o valor de um salário mínimo atual (R$ 1.212) e usei os pesos para acrescentar um percentual, seguindo as regras de quem deveria receber mais.
2- Reparti o valor total de R$ 5.000.000,00 em 3, para dividir exatamente o prêmio entre os cenários e também criar um teto, não deixando que a soma dos cenários ultrapassem essa divisão de R$ 1.666.666,66 cada, evitando também que a empresa pague mais do que o valor disponível
3- Os percentuais foram definidos de acordo com esse teto. Para as duas primeiras regras, o bonus mínimo é de um salário mínimo, aumentando 25% a cada peso, e do peso 3 ao peso 5, um aumento de 50%
Exemplo:
  percentual_peso1_area = salario_minimo_base * 1
  percentual_peso2_area = salario_minimo_base * 1.25
  percentual_peso3_area = salario_minimo_base * 1.5
  percentual_peso5_area = salario_minimo_base * 2
4- Tentei repetir essa fórmula para o cenário de tempo de admissão, mas não foi possível manter esses valores pois mais da metade dos funcionário possuem mais de 8 anos de admissão. Então mantive essa porcentagem:
  percentual_peso1_tempo_admissao = salario_minimo_base * 0.75
  percentual_peso2_tempo_admissao = salario_minimo_base * 0.95
  percentual_peso3_tempo_admissao = salario_minimo_base * 1.15
  percentual_peso5_tempo_admissao = salario_minimo_base * 1.55 
 

Alguns pontos dúvidas que surgiram ao analisar o PDF:
1- O Peso 5 realmente tem um peso a mais em relação ao número 3, já que a regra pula o número 4 (R: Já confirmado que sim)
2- Para as regras de faixa salarial:
    Peso 5: Acima de 8 salários mínimos;
    Peso 3: Acima de 5 salários mínimos e menor que 8 salários mínimos;
    Peso 2: Acima de 3 salários mínimos e menor que 5 salários mínimos;
    Peso 1: Todos os estagiários e funcionários que ganham até 3 salários mínimos;
Não ficou claro onde se encaixam os funcionários que, por ventura, recebem os valores exatos de 8, 5 ou 3 salários mínimos. Usei a regra abaixo no código:
    Peso 5 -> Salário maior ou igual a 8 salários mínimos
    Peso 4 -> Salário menor que 8 salários min. e maior ou igual a 5
    Peso 3 -> Salário menor que 5 salários min. e maior ou igual a 3
    Peso 1 -> Salário menor que 3 salários min. e cargo diferente de 'jovem aprendiz'
    ****Como o jovem aprendiz não foi citado na regra (como foi o estagiário), o removi da regra, deixando com peso 99, ou seja, bonus por salario 0
    
    

