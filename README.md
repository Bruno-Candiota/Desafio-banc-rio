 
import datetime

# Variáveis do sistema
saldo = 0
limite_saque = 500
saques_realizados = 0
limite_saques_diarios = 3
extrato = []
data_ultimo_saque = None

# Menu interativo
while True:
    print("\n=== Sistema Bancário ===")
    print("[1] Depositar")
    print("[2] Sacar")
    print("[3] Extrato")
    print("[4] Sair")
    opcao = input("Escolha uma opção: ")

    if opcao == "1":  # Depósito
        valor = float(input("Informe o valor do depósito: "))
        if valor > 0:
            saldo += valor
            extrato.append(f"Depósito: +R$ {valor:.2f}")
            print(f"Depósito de R$ {valor:.2f} realizado com sucesso!")
        else:
            print("Valor inválido! Informe um valor positivo.")

    elif opcao == "2":  # Saque
        hoje = datetime.date.today()
        
        if data_ultimo_saque != hoje:
            saques_realizados = 0  # Resetar limite diário
            data_ultimo_saque = hoje
        
        if saques_realizados >= limite_saques_diarios:
            print("Limite de saques diários atingido!")
        else:
            valor = float(input("Informe o valor do saque: "))
            if valor > saldo:
                print("Saldo insuficiente!")
            elif valor > limite_saque:
                print(f"O limite máximo por saque é de R$ {limite_saque:.2f}")
            elif valor > 0:
                saldo -= valor
                saques_realizados += 1
                extrato.append(f"Saque: -R$ {valor:.2f}")
                print(f"Saque de R$ {valor:.2f} realizado com sucesso!")
            else:
                print("Valor inválido! Informe um valor positivo.")

    elif opcao == "3":  # Extrato
        print("\n=== Extrato ===")
        if not extrato:
            print("Nenhuma movimentação registrada.")
        else:
            for transacao in extrato:
                print(transacao)
        print(f"\nSaldo atual: R$ {saldo:.2f}")

    elif opcao == "4":  # Sair
        print("Encerrando o sistema...")
        break

    else:
        print("Opção inválida! Tente novamente.")
