# ⚔️ Veyra — Fragmentos de um Reino

> Jogo 2D/2.5D de estratégia e tática por turnos desenvolvido como projeto prático para a avaliação **AF** da disciplina **Programação Avançada e Estrutura de Dados** (Prof. Adriano Felix Valente).

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

*(Nota: Mover uma tropa para cima de outra do mesmo tipo realiza uma fusão que recupera o HP da unidade).*

---

## 🧠 Relação com a Disciplina (Estruturas de Dados)
Embora desenvolvido em tecnologias Web (HTML5, CSS3 e JavaScript puro), o projeto aplica diretamente os conceitos fundamentais estudados em sala de aula na **Linguagem C**:

- **Registros (`struct` em C ➔ Objetos JS):** Agrupamento dos atributos de cada unidade (`HP`, `MOV`, `ALC`, `DANO`) em estruturas lógicas coesas.
- **Matrizes (`grid[x][y]`):** Mapeamento bidimensional das coordenadas, relevos, biomas e obstáculos do campo de batalha.
- **Ordenação / Algoritmo do Pintor:** Cálculo dinâmico de profundidade (`depthA - depthB`) para ordenar o vetor de objetos e renderizar o cenário 2.5D de trás para frente no Canvas.
- **Máquina de Estados:** Controle rígido das telas (`GAME_STATE`) e dos turnos (`TURN_STATE`), garantindo que o sistema opere em um único estado por vez e transicione apenas via gatilhos de eventos.

---

## 🤖 Metodologia de Desenvolvimento e Uso de IA
Atendendo às diretrizes metodológicas estabelecidas pela atividade avaliativa — que determinou o uso obrigatório e a análise comparativa de pelo menos duas ferramentas de Inteligência Artificial no processo de programação —, o grupo empregou o **Google Gemini** e o **ChatGPT** com papéis complementares:

1. **Google Gemini:** Responsável pela criação da arquitetura base em HTML, CSS e JavaScript, geração do mapa das 12 ilhas, rotas marítimas e renderização 2.5D no HTML Canvas.
2. **ChatGPT:** Utilizado para revisar a lógica de combate, validar o algoritmo de perseguição da IA inimiga e comparar as estruturas de dados do jogo com a **Linguagem C**.

### Evolução dos Prompts
1. **Base do Jogo:** *"Desenvolva um jogo original em 2D utilizando HTML, CSS e JavaScript, chamado Veyra, Fragmentos de um Reino. Crie um mundo fictício composto por 12 ilhas, cada uma com nomes, características e recursos próprios, conectadas por rotas marítimas. Desenvolva um mapa interativo e funcional em HTML Canvas..."* ➔ **Resultado:** Geração da estrutura inicial e do mapa navegável.
2. **Batalhas e Tropas:** *"Implemente combate tático... Crie infantaria, arqueiros e defensores."* ➔ **Resultado:** Implementação do sistema de turnos e classes de unidades.
3. **Biomas Variados:** *"Cada ilha deve ter biomas diferentes, rios, para dificultar batalha."* ➔ **Resultado:** Criação de cenários de neve, deserto, vulcão e floresta.
4. **Loja e Economia:** *"Dar uma função para o ouro (comprar tropas, equipamentos)."* ➔ **Resultado:** Criação do menu Acampamento e sistema de tesouros.
5. **Persistência e Menus:** *"Dar possibilidade de salvar jogo e de sair da partida."* ➔ **Resultado:** Salvamento local via `localStorage` e menu de pausa integrado.

---

## 🐛 Bugs Encontrados e Correções

### Bug 1: Perda total de tropas travava a campanha
- **Descrição:** Quando o jogador perdia todas as suas unidades em combate, o exército ficava zerado, impedindo o avanço na campanha.
- **Prompt de Correção:** *"O problema de ter 0 tropas continua, encontre uma solução."*
- **Solução:** Alterada a lógica de derrota para que as unidades abatidas recuem para o acampamento em vez de serem excluídas permanentemente do save.

### Bug 2: Montanhas tampavam personagens e bloqueavam cliques
- **Descrição:** Na renderização 2.5D, os blocos sólidos de relevo escondiam unidades posicionadas atrás deles, dificultando a visão tática e a seleção com o mouse.
- **Prompt de Correção:** *"Permitir ver personagens mesmo atrás das montanhas."*
- **Solução:** Aplicação de transparência dinâmica (`globalAlpha`) no Canvas quando há unidades ocultas pelo relevo.

**Código Antes:**
```javascript
ctx.drawImage(montanha, x, y); // Desenhava sólido por cima da tropa
```

**Código Depois:**
```javascript
ctx.globalAlpha = 0.4;
ctx.drawImage(montanha, x, y); // Aplica transparência dinâmica
```

---

## 🚀 Como Executar o Projeto
1. Clone este repositório ou baixe os arquivos.
2. Abra o arquivo `index.html` diretamente em qualquer navegador moderno (Chrome, Edge, Firefox).
3. Não há necessidade de instalar dependências ou servidores externos.

## 📄 Apresentação e Documentação
Os slides completos utilizados na apresentação da disciplina estão disponíveis neste repositório no arquivo `apresentacao-veyra.pdf`.
