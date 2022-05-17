# Amortizations-System


print("\n== OLÁ, VOCÊ ESTÁ NO SISTEMA SIMULADOR DE FINANCIAMENTOS DO BANCO XYZ ==") 

print("\t\tPor favor, insira a seguir os dados do seu financiamento:\n") 

n = int(input("Digite o prazo do seu financiamento em anos: \n")) 
i = float(input ("Digite a taxa anual do seu financiamento (não é necessário o sinal '%' apenas o numero inteiro não decimal: \n")) 
i = i / 100 
sd = float(input ("Digite o valor total do seu financiamento: \n")) 
n1 = n * 12 

def sac(): # FUNÇÃO DESENVOLVE O CÁLCULO CASO A FUNÇÃO "TO_CHOOSE" RETORNE  SAC.
    print("\n====Evolução do Financiamento pelo SAC - Sistema de Amortização Constante") 
    print(f"nº \t\t Parcela \tAmortização \tJuros \tSaldo Devedor\n") 
    x = 0  
    global sd
    if(x == 0):
        print(f"{0} \t\t\t\t\t\t\t\t\t\t\t {sd:.2f} ") 
        x=1
    amort = sd / n1  
    while x <= n1: 
        juros = (sd * (i/12)) 
        sd = sd - amort 
        parcela = amort + juros 
        print(f"{x} \t\t{parcela:.2f} \t\t{amort:.2f} \t\t{juros:.2f} \t\t {sd:.2f} ")
        x += 1

def price(): # FUNÇÃO DESENVOLVE O CÁLCULO CASO A FUNÇÃO "TO_CHOICE" RETORNE PRICE.
    print("\n====Evolução do Financiamento pelo 'PRICE' - Sistema Francês de Amortização") 
    print(f"nº Parcela Amortização Juros Saldo Devedor\n") 
    global sd 

    y = 1+(i/12) 
    y1 = (y ** n1)
    PMT = sd * ((y1 * (i/12)) / (y1 -1)) 
    x = 0  
    if(x == 0):
        print(f"{0} \t\t\t\t\t\t\t {sd:.2f} ") 
        x=1
    while x <= n1: 
        juros = (sd * (i/12)) 
        amort = PMT - juros 
        sd = sd - amort 
        print(f"{x} \t{PMT:.2f} \t{amort:.2f} \t{juros:.2f} \t {sd:.2f} ") 
        x += 1

def to_choose (): # ESTA FUNÇÃO SERÁ USADA PARA A DEFINIÇÃO DO MÉTODO DE AMORTIZAÇÃO A SER UTILIZADO.
    sistema = input(
        "Escolha o sistema de Amortização: Para Price (P) e para SAC (S): ")  
    if (sistema == "P"):
        price() 
    elif (sistema == "S"):
        sac() 
    else: #
        print("Valor digitado inválido!")
        to_choose()

to_choose() 
