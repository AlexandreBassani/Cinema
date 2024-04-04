class Cinema:
    def __init__(self):
        self.salas = {
            'Sala 1': [['-' for _ in range(10)] for _ in range(10)],
            'Sala 2': [['-' for _ in range(10)] for _ in range(10)]
        }
        self.ultima_reserva = None

    def mostrar_mapa(self, nome_sala):
        print("   A B C D E F G H I J")
        letras = 'ABCDEFGHIJ'
        sala = self.salas.get(nome_sala)
        for i in range(10):
            print(i + 1, end='  ')
            for j in range(10):
                print(sala[i][j], end=' ')
            print()

    def visualizar_salas(self):
        for nome_sala in self.salas:
            print(f"\nMapa da {nome_sala}:")
            self.mostrar_mapa(nome_sala)

    def reservar_lugar(self, nome_sala, linha, coluna):
        sala = self.salas.get(nome_sala)
        if sala is None:
            print("Sala não encontrada.")
            return False

        if linha < 0 or linha >= 10 or coluna < 0 or coluna >= 10:
            print("Lugar inválido. Tente novamente.")
            return False

        if sala[linha][coluna] == '-':
            sala[linha][coluna] = 'X'
            assento = f"{chr(coluna + 65)}{linha + 1}"
            self.ultima_reserva = (nome_sala, assento)
            print(f"Lugar reservado com sucesso na {nome_sala}! Assento: {assento}")
            return True
        else:
            print("Lugar já reservado. Escolha outro.")
            return False

def menu():
    cinema = Cinema()

    while True:
        print("\nMenu:")
        print("1. Visualizar salas")
        print("2. Reservar lugar")
        print("3. Sair")

        escolha = input("Escolha uma opção: ")

        if escolha == '1':
            cinema.visualizar_salas()
        elif escolha == '2':
            nome_sala = input("Digite o nome da sala (Sala 1 ou Sala 2): ").title()
            if nome_sala in cinema.salas:
                print(f"Escolheu a {nome_sala}.")
                linha = int(input("Digite o número da linha (1-10): ")) - 1
                coluna = ord(input("Digite a letra da coluna (A-J): ").upper()) - 65
                cinema.reservar_lugar(nome_sala, linha, coluna)
            else:
                print("Sala não encontrada. Tente novamente.")
        elif escolha == '3':
            if cinema.ultima_reserva:
                sala, assento = cinema.ultima_reserva
                print(f"Última reserva: {sala}, Assento: {assento}")
            print("Obrigado por utilizar nosso serviço. Até logo!")
            break
        else:
            print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
    menu()
