# Amortizations-System
Some ideas to financial calculate tools

#APRESENTA O CABEÇALHO E ORIENTAÇÕES GERAIS DO PROGRAMA

print("\n== OLÁ, VOCÊ ESTÁ NO SISTEMA SIMULADOR DE FINANCIAMENTOS DO BANCO XYZ ==") # print do cabeçaho do programa
print("\t\tPor favor, insira a seguir os dados do seu financiamento:\n") # instruções gerais ao usuário.

#NESTA PARTE O USUÁRIO FARÁ A IMPUTAÇÃO DOS DADOS DO FINANCIAMENTO

n = int(input("Digite o prazo do seu financiamento em anos: \n")) # vai atrbuir o tempo do empréstimo em anos
i = float(input ("Digite a taxa anual do seu financiamento (não é necessário o sinal '%' apenas o numero inteiro não decimal: \n")) # vai receber a taxa de juros anual
i = i / 100 #  transforma i em decimal
sd = float(input ("Digite o valor total do seu financiamento: \n")) # recebe o valor do empréstimo
n1 = n * 12 # vai receber o prazo em meses para montar a evolução de cada linha do empréstimo

# depois da inserção de dados o programa vai chamar a função to_choose para que seja escolhido o método de amortização

def sac(): # FUNÇÃO DESENVOLVE O CÁLCULO CASO A FUNÇÃO "TO_CHOOSE" RETORNE  SAC.
    print("\n====Evolução do Financiamento pelo SAC - Sistema de Amortização Constante") # vai fazer print do cabeçalho da opção
    print(f"nº \t\t Parcela \tAmortização \tJuros \tSaldo Devedor\n") # vai fazer print do cabeçalho da tabela de evolução
    x = 0  # variável local de contagem
    global sd
    if(x == 0):
        print(f"{0} \t\t\t\t\t\t\t\t\t\t\t {sd:.2f} ") # Monta a linha "0" do financiamento que representa o momento da contratação e por isso nao tem parcela, nem juros tampouco amortização, apenas mostra o saldo devido.
        x=1
    amort = sd / n1  # variavel local que recebe o valor da amortização. Neste método a amortização tem valor fixo.
    while x <= n1: # loop que vai montar linha a linha e evolução do empréstimo
        juros = (sd * (i/12)) # apura o valor dos juros linha a linha
        sd = sd - amort # apura a evoluçao do saldo devedor linha a linha
        parcela = amort + juros # apura o valor da parcela linha a linha
        print(f"{x} \t\t{parcela:.2f} \t\t{amort:.2f} \t\t{juros:.2f} \t\t {sd:.2f} ") # faz o print de cada linha da evolução
        x += 1

def price(): # FUNÇÃO DESENVOLVE O CÁLCULO CASO A FUNÇÃO "TO_CHOICE" RETORNE PRICE.
    print("\n====Evolução do Financiamento pelo 'PRICE' - Sistema Francês de Amortização") # vai fazer print do cabeçalho da opção
    print(f"nº Parcela Amortização Juros Saldo Devedor\n") # vai fazer print do cabeçalho da tabela de evolução
    global sd # declarada sd como global para a função poder acessar esse dado

    #Neste método o valor da parcela é fixo e a fórmula de cálculo é extensa. Para ficar mais legível quebrei em partes.

    y = 1+(i/12) # para facilitar o entendimento separei o cálculo em partes colocando em Y e Y1 (var.local) partes do cálculo do coeficiente.
    y1 = (y ** n1)
    PMT = sd * ((y1 * (i/12)) / (y1 -1)) # aqui as partes armazenadas em y e y1 são trazidas para o cálculo final da parcela.
    x = 0  # variável local de contagem
    if(x == 0):
        print(f"{0} \t\t\t\t\t\t\t {sd:.2f} ") # Monta a linha "0" do financiamento que representa o momento da contratação e por isso nao tem parcela, nem juros tampouco amortização, apenas mostra o saldo devido.
        x=1
    while x <= n1: # loop que vai montar linha a linha e evolução do empréstimo
        juros = (sd * (i/12)) # apura o valor dos juros linha a linha
        amort = PMT - juros # apura a amortização linha a linha
        sd = sd - amort # apura a evoluçao do saldo devedor linha a linha
        print(f"{x} \t{PMT:.2f} \t{amort:.2f} \t{juros:.2f} \t {sd:.2f} ") # faz o print de cada linha da evolução
        x += 1

def to_choose (): # ESTA FUNÇÃO SERÁ USADA PARA A DEFINIÇÃO DO MÉTODO DE AMORTIZAÇÃO A SER UTILIZADO.
    sistema = input(
        "Escolha o sistema de Amortização: Para Price (P) e para SAC (S): ")  # para escolha do método, se Price ou SAC
    if (sistema == "P"):
        price() # chama a função de cálculo pelo price
    elif (sistema == "S"):
        sac() # chama a função de cálculo pelo SAC
    else: # prende o usuário nessa função  até que digite corretamente o "char" de escolha.
        print("Valor digitado inválido!")
        to_choose()

to_choose() # DEPOIS DA INSERÇÃO DOS DADOS VAI CHAMAR A FUNÇÃO DE ESCOLHA DO MÉTODO.
