-class ContaBancaria:
    def __init__(self, numero_conta, saldo=0):
        self.numero_conta = numero_conta
        self.saldo = saldo

    def depositar(self, valor):
        self.saldo += valor
        print(f'Depósito de R${valor} realizado com sucesso.')
    
    def sacar(self, valor):
        if self.saldo >= valor:
            self.saldo -= valor
            print(f'Saque de R${valor} realizado com sucesso.')
        else:
            print('Saldo insuficiente.')

    def visualizar_saldo(self):
        print(f'Saldo da conta {self.numero_conta}: R${self.saldo:.2f}')


class ContaCorrente(ContaBancaria):
    def __init__(self, numero_conta, saldo=0, taxa_manutencao=0):
        super().__init__(numero_conta, saldo)
        self.taxa_manutencao = taxa_manutencao

    def aplicar_taxa_manutencao(self):
        self.saldo -= self.taxa_manutencao
        print(f'Taxa de manutenção de R${self.taxa_manutencao} aplicada com sucesso.')


class ContaPoupanca(ContaBancaria):
    def __init__(self, numero_conta, saldo=0, juros=0.03):
        super().__init__(numero_conta, saldo)
        self.juros = juros

    def calcular_juros(self):
        self.saldo += self.saldo * self.juros
        print(f'Juros de {self.juros * 100}% aplicados com sucesso.')


class Cliente:
    def __init__(self, nome, conta_corrente=None, conta_poupanca=None):
        self.nome = nome
        self.conta_corrente = conta_corrente
        self.conta_poupanca = conta_poupanca

    def exibir_informacoes(self):
        print(f'Nome: {self.nome}')
        if self.conta_corrente:
            print('Conta Corrente:')
            self.conta_corrente.visualizar_saldo()
        if self.conta_poupanca:
            print('Conta Poupança:')
            self.conta_poupanca.visualizar_saldo())


# Exemplo de Uso:
if __name__ == "__main__":
    # Criando contas
    conta_corrente = ContaCorrente(numero_conta='123', saldo=1000, taxa_manutencao=10)
    conta_poupanca = ContaPoupanca(numero_conta='456', saldo=2000)

    # Criando cliente
    cliente1 = Cliente(nome='João', conta_corrente=conta_corrente, conta_poupanca=conta_poupanca)

    # Realizando operações
    cliente1.exibir_informacoes()
    conta_corrente.depositar(500)
    conta_corrente.aplicar_taxa_manutencao()
    conta_corrente.visualizar_saldo()
    conta_poupanca.depositar(1000)
    conta_poupanca.calcular_juros()
    conta_poupanca.visualizar_saldo()
    conta_poupanca.sacar(500)
    conta_poupanca.visualizar_saldo()
    cliente1.exibir_informacoes()
