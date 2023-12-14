# Clinica-veterinaria-virtual-e-calculadora-de-dosagem.
def selecione_especialidade(): #Aqui esto criando una lista de opções como o professor João nos ensinou com seu programa do Mercado.
    print("Bem-vindo à clínica veterinária **Amigos dos Pets**. Por favor, escolha uma especialidade:")
    print("1. Medicina Geral - Custo: R$150")
    print("2. Odontologia - Custo: R$200")
    print("3. Castração - Custo: R$120")
    print("4. Dermatologia - Custo: R$180")
    print()
    
    especialidades = {  #Nesta parte crio uma lista das especialidades e os custos.
        '1': {'nome': 'Medicina General', 'custo': 150},
        '2': {'nome': 'Odontologia', 'custo': 200},
        '3': {'nome': 'Castração', 'custo': 120},
        '4': {'nome': 'Dermatologia', 'custo': 180}
    }

    while True: #Aqui estou criando um loop incluindo um booleano para garantir que o usuário escolha apenas entre as opções fornecidas.
        opcao = input("Digite o número da especialidade desejada: ")
        if opcao in especialidades:
            break
        else:
            print("Opção inválida. Por favor, escolha um número válido.")

    return especialidades[opcao]

#Aqui estou criando uma função para calcular o troco de pagamento do usuário apenas para pagamento com notas, não incluí moedas!
def calcular_troco(valor_consulta, valor_pago):
    if valor_pago >= valor_consulta:
        troco = valor_pago - valor_consulta

        if troco == 0:
            print("Pagamento aceito. Não há troco disponível.")
            print()
            print("Obrigada pelo pagamento, Pode passar para a consulta!!!")
            print()
        elif troco < 2: #Se o troco é menor que R$2 pesso para o usuario que tiene que hacer un exato o maior.
            print("Lamentamos informar que não temos troco para valores menores que R$2. Por favor, pague com um valor exato ou maior.")
            print()
        else: #Aqui estou descrevendo as opções de troco aos pagamentos do usuário e quando o troco é insuficiente peço ao usuário que insira um valor válido.
            print(f"O seu troco é de R${troco:.2f}")
            print()
            
            denominacoes = [100, 50, 20, 10, 5, 2]

            for denominacao in denominacoes:
                quantidade = int(troco // denominacao)
                if quantidade > 0:
                    print(f"{quantidade} nota(s) de R${denominacao:.2f}")
                    troco -= quantidade * denominacao
                    print()

            print("Obrigada pelo pagamento, Pode passar para a consulta!!!")
            print()
    else:
        print("O valor pago é insuficiente.")
        print()

    return troco

#Como segunda parte no meu programa crie uma calculadora da dosagem de medicamento em relação ao peso do pet, varia conforme ao medicamento e as recomendações do veterinario.
def calcular_dosagem(peso): 
    dosagem = peso * 0.02  # Exemplo: 0.02 mg por cada kg de peso para os medicamentos indicados en cada especialidade desta clínica veterinaria.
    return dosagem


def main(): #Esta ultima parte como o  professor João explicou na ultima aula de resolução de problemas crio minha função "def main():" para incluir as linhas de código que possam dar error potencialmente.
    especialidade = selecione_especialidade()
    print(f"Você selecionou {especialidade['nome']} com custo de R${especialidade['custo']:.2f}. Agora é o momento de pagar para que possamos atender ao seu pet")
    print()

    while True:
        try: #Também envolvo estas partes do código em blocos "try" para resolução de problemas na execução.
            valor_pago = float(input("Informe o valor que você vai pagar, lembre que não trabalhamos com moedas: R$"))

            if valor_pago.is_integer() and valor_pago >= especialidade['custo']:
                break
            else:
                print("Valor inválido. Por favor, informe um valor numérico inteiro igual ou maior que o custo da especialidade.")
        except ValueError:
            print("Por favor, informe um valor numérico inteiro igual ou maior que o custo da especialidade.")
            print()

    troco = calcular_troco(especialidade['custo'], valor_pago)

    if troco >= 2 or troco == 0: #Crio esta condicional para que o programa entenda que os trocos para o usuario podem ser maior ou igual a 2, ou 0.
        try:
            while True:
                peso_pet = float(input("Esperamos que tenha gostado da sua consulta. Agora é o momento de calcular a dosagem do medicamento que o veterinário indicou para seu pet. Por favor, informe o peso de seu pet em kilogramas: "))
                print()
                
                if peso_pet > 0: #Os pesos validos dos pets são maiores a 0. 
                    break
                else:
                    print("Peso inválido. Seu pet está morto se pesa menos que 0. Por favor, informe um peso válido maior que 0.")
                    
            dosagem_recomendada = calcular_dosagem(peso_pet) #Finalmente faço o calculo da dosagem respeito ao peso e agradeço a precensa do usuario.
            dosagem_formatada = "{:.2f}".format(dosagem_recomendada)

            print(f"A dosis recomendada para seu pet de {peso_pet} kg é: {dosagem_formatada} mg. Lembre-se de dar o medicamento conforme as recomendações do veterinário. Agradecemos a preferência. Volte sempre, aqui somos **Amigos dos Pets**")
            print()
        except ValueError:
            print("Por favor, informe um peso válido em quilogramas.")#Esta parte pede ao usuario incluir um peso valido
            print()

if __name__ == "__main__":
    main()

