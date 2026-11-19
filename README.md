# ⚔️ Veyra — Fragmentos de um Reino

> Jogo 2D/2.5D de estratégia e tática por turnos desenvolvido para a avaliação **AF** da disciplina **Programação Avançada e Estrutura de Dados**.

## 👥 Integrantes do Grupo
- **Felipe Dantas**
- **Gabriel Gomes**
- **Henrique Dante**

---

## 🎮 Conceito e Mecânicas
O mundo de **Veyra** é um arquipélago fragmentado composto por **12 ilhas em guerra**, conectadas por rotas marítimas. O objetivo do jogador é liderar sua aliança, gerenciar ouro no Acampamento, conquistar territórios e reconstruir o reino por meio de combates táticos em turnos.

### Classes de Unidades

| Unidade | Função Tática | Vida (HP) | Movimento (MOV) | Alcance (ALC) | Dano |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Guerreiro** | Linha de frente equilibrada | 6 | 2 | 1 | 2 |
| **Arqueiro** | Ataque à distância | 3 | 2 | 4 | 2 |
| **Escudeiro** | Defesa extrema | 8 | 1 | 1 | 1 |
| **Vanguarda** | Cavalaria rápida e letal | 4 | 3 | 1 | 3 |

---

## 🧠 Relação com a Disciplina (Estruturas de Dados)
- **Registros (`struct` em C ➔ Objetos JS):** Agrupamento dos atributos de cada unidade (`HP`, `MOV`, `ALC`, `DANO`).
- **Matrizes (`grid[x][y]`):** Mapeamento bidimensional das coordenadas, relevos e terrenos do campo de batalha.
- **Ordenação / Algoritmo do Pintor:** Cálculo de profundidade (`depthA - depthB`) para desenhar os elementos 2.5D de trás para frente no Canvas.
- **Máquina de Estados:** Controle rígido das telas (`GAME_STATE`) e dos turnos (`TURN_STATE`) disparado por eventos.

---

## 🤖 Ferramentas de IA e Comparação
Foram utilizadas duas inteligências artificiais com papéis complementares durante o desenvolvimento:
1. **Google Gemini:** Responsável pela criação da arquitetura base em HTML, CSS e JavaScript, geração do mapa das 12 ilhas, rotas marítimas e renderização 2.5D no HTML Canvas.
2. **ChatGPT:** Utilizado para revisar a lógica de combate, validar o algoritmo de perseguição da IA inimiga e comparar as estruturas de dados do jogo com a **Linguagem C**.

### Evolução dos Prompts
1. **Base do Jogo:** *"Desenvolva um jogo original em 2D utilizando HTML, CSS e JavaScript, chamado Veyra, Fragmentos de um Reino. Crie um mundo fictício composto por 12 ilhas..."* ➔ Gerou o mapa navegável em Canvas.
2. **Batalhas e Tropas:** *"Implemente combate tático... Crie infantaria, arqueiros e defensores."* ➔ Adicionou o sistema de turnos e as classes.
3. **Biomas Variados:** *"Cada ilha deve ter biomas diferentes, rios, para dificultar batalha."* ➔ Criou mapas de neve, deserto, vulcão e floresta.
4. **Loja e Economia:** *"Dar uma função para o ouro (comprar tropas, equipamentos)."* ➔ Criou o menu Acampamento e os baús de tesouro.
5. **Persistência e Menus:** *"Dar possibilidade de salvar jogo e de sair da partida."* ➔ Implementou salvamento local (`localStorage`) e menu de pausa.

---

## 🐛 Bugs Encontrados e Correções

### Bug 1: Perda total de tropas travava a campanha
- **Descrição:** Quando o jogador perdia todas as unidades em batalha, o exército ficava zerado e impedia o avanço na campanha.
- **Prompt de Correção:** *"O problema de ter 0 tropas continua, encontre uma solução."*
- **Solução:** Implementada lógica para que tropas derrotadas recuem em vez de serem apagadas permanentemente.

### Bug 2: Montanhas tampavam personagens e bloqueavam cliques
- **Descrição:** O relevo sólido no mapa 2.5D escondia unidades posicionadas atrás dele, dificultando a visualização e a seleção.
- **Prompt de Correção:** *"Permitir ver personagens mesmo atrás das montanhas."*
- **Código Antes:**
```javascript
ctx.drawImage(montanha, x, y); // Desenhava sólido por cima da tropa
```
- **Código Depois:**
```javascript
ctx.globalAlpha = 0.4;
ctx.drawImage(montanha, x, y); // Aplica transparência dinâmica
```

---

## 📄 Apresentação do Projeto
Os slides completos utilizados na apresentação estão disponíveis neste repositório no arquivo `apresentacao-veyra.pdf`.


