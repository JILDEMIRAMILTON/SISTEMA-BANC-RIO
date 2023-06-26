# SISTEMA-BANC-RIO
SISTEMA BANCÁRIO
import datetime

class Banco:
    def __init__(self):
        self.saldo = 0
        self.depositos = []
        self.saques = []
        self.saques_diarios = 0
        self.data_atual = datetime.date.today()

    def deposito(self):
        valor = float(input('Digite o valor a ser depositado: '))
        if valor > 0:
            self.saldo += valor
            self.depositos.append(valor)
            print(f'Depósito de R$ {valor:.2f} realizado com sucesso.')
        else:
            print('Valor inválido para depósito.')

    def saque(self):
        if self.saques_diarios < 3:
            valor = float(input('Digite o valor a ser sacado: '))
            if valor > 0 and valor <= 500:
                if self.saldo >= valor:
                    self.saldo -= valor
                    self.saques.append(valor)
                    self.saques_diarios += 1
                    print(f'Saque de R$ {valor:.2f} realizado com sucesso.')
                else:
                    print('Saldo insuficiente para realizar o saque.')
            else:
                print('Valor inválido para saque. O valor deve ser maior que 0 e no máximo R$ 500.')
        else:
            print('Limite diário de saques atingido.')

    def extrato(self):
        print('--- Extrato ---')
        if len(self.depositos) == 0 and len(self.saques) == 0:
            print('Não foram realizadas movimentações.')
        else:
            for deposito in self.depositos:
                print(f'Depósito: R$ {deposito:.2f}')
            for saque in self.saques:
                print(f'Saque: R$ {saque:.2f}')
        print(f'Saldo atual: R$ {self.saldo:.2f}')


# Exemplo de uso
banco = Banco()

while True:
    print('--- Menu ---')
    print('D - Depositar')
    print('S - Sacar')
    print('E - Extrato')
    print('Sair - Encerrar programa')

    opcao = input('Digite a opção desejada: ')

    if opcao.lower() == 'd':
        banco.deposito()
    elif opcao.lower() == 's':
        if banco.data_atual == datetime.date.today():
            banco.saque()
        else:
            banco.data_atual = datetime.date.today()
            banco.saques_diarios = 0
            banco.saque()
    elif opcao.lower() == 'e':
        banco.extrato()
    elif opcao.lower() == 'sair':
        break
    else:
        print('Opção inválida.')


