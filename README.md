<h1 align="center"> Projeto de Automação Brasfoot </h1>
</br>
<p> Este projeto não é de curso nem uma cópia de terceiros. </p>

<p> Criado para acabar com um processo repetitivo e monótono dentro do Brasfoot (um jogo no qual você assume o papel de técnico e dirigente de um clube de futebol). Essa automação em Python serve para gerenciar a categoria de base de um clube de forma rápida e inteligente. </p> 

<p> O código irá fazer uma análise do elenco da categoria de base, dispensar os atletas de baixo desempenho e manter somente os craques. </p>

</br>

### __Bibliotecas Utilizadas:__ ###  

__PyAutoGUI__ </br>
Biblioteca Python usada para automatizar a interação com a interface gráfica, simulando movimentos e cliques do mouse. 

__Time__ </br>
É uma biblioteca padrão do python utilizada para criar pausas entre as ações, garantindo um fluxo suave entre cliques e análises.

</br>

### Funcionalidades do Código: ###

* Navega automaticamente até a tela da categoria de base de um clube.

* Analisa visualmente os atributos de cada jogador para determinar se ele é talentoso ou não.

* Identifica os jogadores com baixo ou elevado desempenho. 

* Dispensa os jogadores menos habilidosos, mantendo apenas os craques na base.

### Código:
```
import pyautogui
import time

# Automação de Venda de jogadore da base.  

def clicar(x,y):
    pyautogui.moveTo(x, y, duration=0.5)x
    pyautogui.click(x,y)
    
caminho_juniores = [
    (331, 45),      # Ícone de times.
    (1211, 268),    # ícone da Academia de Juniores.
    (1005, 337),    # Primeiro Jogador da Academia de Juniores.
]

for x, y in caminho_juniores:
    clicar(x,y)

linhas_jogadores = [
    [(997, 334), (1014, 334), (1031, 334), (1047, 334), (1065, 334)],  # Jogador 1
    [(997, 355), (1014, 355), (1031, 355), (1048, 355), (1065, 355)],  # Jogador 2
    [(999, 375), (1014, 375), (1032, 375), (1048, 375), (1065, 375)],  # Jogador 3
    [(998, 395), (1014, 395), (1032, 395), (1048, 395), (1065, 395)],  # Jogador 4
    [(997, 415), (1014, 415), (1032, 417), (1048, 415), (1064, 415)],  # Jogador 5
]

cor_verde = (36, 91, 45) # verde escuro

jogadores_ruins = []

print()
print(" Identificando jogadores:")
print()

for i, linha in enumerate(linhas_jogadores):
    coordenadas_verdes = sum(1 for x,y in linha if pyautogui.pixel(x,y) == cor_verde)

    if coordenadas_verdes >= 1 and coordenadas_verdes <= 4:
        print(f"    Jogador {i + 1}: ruim de bola.")
        jogadores_ruins.append(i)  
    else:
        print(f"    Jogador {i + 1}: craque.")

tempo_espera = 0.5
dispensar_jogador = (780, 767)
confirmar_dispensa = (937, 542)

print()     
print(" Excluindo somente jogadores ruins:")
print()


for i in reversed(jogadores_ruins):
    linha = linhas_jogadores[i] 
    print(f"    Excluindo o jogador {i + 1}...")

    for coordenada in linha:
        clicar(*coordenada)

    clicar(*dispensar_jogador)
    time.sleep(tempo_espera)  

    clicar(*confirmar_dispensa)
    time.sleep(tempo_espera)  

    linhas_jogadores.pop(i)  
    time.sleep(tempo_espera)  
```
