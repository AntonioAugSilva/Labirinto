class Labirinto:
    def __init__(self, grid, inicio, premio):
        self.grid = grid
        self.inicio = inicio
        self.premio = premio
        self.linhas = len(grid)
        self.colunas = len(grid[0])
        self.movimentos = [(0, 1), (1, 0), (0, -1), (-1, 0)]  # Direções: Direita, Baixo, Esquerda, Cima
    
    def dentro_limite(self, x, y):
        return 0 <= x < self.linhas and 0 <= y < self.colunas
    
    def resolver(self):
        pilha = []
        pilha.append(self.inicio)
        visitados = set()
        
        while pilha:
            x, y = pilha.pop()
            
            if (x, y) == self.premio:
                print("Caminho encontrado!")
                return True
            
            if (x, y) in visitados:
                continue
            
            visitados.add((x, y))
            
            for dx, dy in self.movimentos:
                novo_x, novo_y = x + dx, y + dy
                
                if self.dentro_limite(novo_x, novo_y) and self.grid[novo_x][novo_y] != '#' and (novo_x, novo_y) not in visitados:
                    pilha.append((novo_x, novo_y))
        
        print("Caminho não encontrado!")
        return False

# Exemplo de uso
labirinto = [
    [' ', ' ', ' ', '#', ' ', ' '],
    ['#', '#', ' ', '#', ' ', '#'],
    [' ', ' ', ' ', ' ', ' ', ' '],
    [' ', '#', '#', '#', '#', ' '],
    [' ', ' ', ' ', ' ', ' ', 'P']  # 'P' representa o prêmio
]

inicio = (0, 0)  # Posição inicial
premio = (4, 5)  # Posição do prêmio

jogo = Labirinto(labirinto, inicio, premio)
jogo.resolver()
