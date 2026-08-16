# Especificação de Requisitos Funcionais

## Caso de Uso (CDU) — Jogar Jogo da Velha Web — UNIFOR

---

## Histórico de Versões

| Data | Versão | Descrição | Autor |
|---|---|---|---|
| 08/08/2026 | 0.1 | Criação do caso de uso de Jogar Jogo da Velha | Pedro |
| 15/08/2026 | 0.2 | Revisão do CDU com base na implementação do `src/index.html` | Pedro |

*obs: o versionamento não foi realizado*

---

# 1. Nome do Caso de Uso

**Jogar Jogo da Velha**

---

# 2. Objetivo

Permitir que o jogador dispute partidas de Jogo da Velha em ambiente web, podendo jogar contra outro jogador local ou contra o computador, nos formatos **Partida Única** ou **Melhor de 3 (MD3)**, com acompanhamento do placar, indicação da rodada, detecção de vitória e empate, destaque visual da combinação vencedora, efeitos sonoros sintetizados, animação de confetes e indicação visual do campeão no formato MD3.

---

# 3. Tipo de Caso de Uso

**Concreto**

---

# 4. Atores

## 4.1 Ator Primário

**Jogador:** interage com a interface, seleciona o modo e formato da partida, realiza as jogadas e pode reiniciar a partida.

## 4.2 Ator Secundário

**Computador:** componente interno da aplicação que realiza automaticamente as jogadas do símbolo `O` quando o modo Contra o Computador está selecionado.

---

# 5. Precondições

- O jogador deve acessar a aplicação por meio de um navegador compatível com HTML5, CSS e JavaScript.
- O navegador deve permitir a execução de JavaScript.
- Para os efeitos sonoros, o navegador deve possuir suporte à Web Audio API.
- A aplicação deve estar carregada com seus recursos contidos no próprio arquivo HTML.

---

# 6. Fluxo Principal — Jogar Partida

**P1.** O jogador acessa a aplicação.

**P2.** O sistema inicializa uma nova partida com:

- tabuleiro vazio;
- jogador `X` como primeiro jogador;
- placar `0 × 0`;
- rodada `1`;
- modo `2 Jogadores (PVP)`;
- formato `Partida Única`;
- partida ativa;
- mensagem de status `"Vez do Jogador X"`.

**P3.** O sistema exibe a interface contendo:

- identificação `"Universidade de Fortaleza"`;
- título `"Jogo da Velha"`;
- indicação de que o jogador pode desafiar amigos ou o computador;
- seletor Modo de Jogo;
- seletor Formato da Partida;
- placar do Jogador X;
- contador de rodada;
- placar do Jogador O ou Computador;
- mensagem de status;
- tabuleiro 3 × 3;
- botão `"REINICIAR JOGO"`.

**P4.** O jogador seleciona uma célula vazia do tabuleiro.

**P5.** O sistema verifica se:

- a partida está ativa;
- a célula está vazia;
- a jogada é permitida para o jogador atual.

**P6.** O sistema registra a jogada:

- atribui `X` ou `O` à posição selecionada;
- atualiza visualmente a célula;
- desabilita a célula ocupada;
- reproduz o efeito sonoro correspondente ao símbolo.

**P7.** O sistema verifica se a jogada produziu uma combinação vencedora entre as oito possibilidades de linhas, colunas e diagonais. **[A1] [E1]**

**P8.** Caso não exista vencedor ou empate, o sistema alterna o jogador atual entre `X` e `O`.

**P9.** O sistema atualiza a mensagem de status para indicar o próximo jogador.

**P10.** Caso o modo seja Contra o Computador e o próximo jogador seja `O`, o sistema inicia automaticamente o fluxo de jogada do computador. **[A2]**

**P11.** O fluxo retorna ao passo P4 até que ocorra uma vitória, empate ou reinício.

---

# 7. Fluxos Alternativos

## A1. Fim da Rodada por Vitória

**A1.1.** No passo P7, o sistema identifica três símbolos iguais em uma linha, coluna ou diagonal.

**A1.2.** O sistema encerra temporariamente a rodada, impedindo novas jogadas.

**A1.3.** O sistema calcula a posição das duas extremidades da combinação vencedora no tabuleiro.

**A1.4.** O sistema desenha uma linha visual sobre as três células vencedoras.

**A1.5.** O sistema aplica destaque visual às três células da combinação vencedora.

**A1.6.** O sistema incrementa o placar do jogador vencedor.

**A1.7.** O sistema reproduz o acorde sonoro de vitória utilizando a Web Audio API.

**A1.8.** O sistema executa a animação de confetes utilizando um elemento `<canvas>`.

**A1.9.** O sistema atualiza o status para:

- `"Jogador X venceu a rodada!"`, quando X vencer;
- `"Jogador O venceu a rodada!"`, no modo PVP quando O vencer;
- `"Computador venceu a rodada!"`, no modo Contra o Computador quando O vencer.

**A1.10.** Se o formato for Partida Única, o sistema mantém a rodada encerrada até que o jogador reinicie a partida.

**A1.11.** Se o formato for Melhor de 3 (MD3) e um jogador atingir duas vitórias, o sistema agenda a exibição da tela de campeão.

**A1.12.** O sistema exibe uma janela de campeão contendo:

- ícone de troféu;
- identificação do campeão;
- placar final;
- botão `"FECHAR"`.

**A1.13.** Se o formato for MD3 e nenhum jogador atingir duas vitórias, o sistema aguarda aproximadamente 2 segundos.

**A1.14.** Após o intervalo, o sistema inicia a próxima rodada, limpa o tabuleiro, remove o destaque da vitória, mantém o placar acumulado e define `X` como primeiro jogador.

---

## A2. Jogada do Computador

**A2.1.** O fluxo é iniciado quando o modo Contra o Computador está selecionado e o jogador atual é `O`.

**A2.2.** O sistema bloqueia os cliques das células enquanto a CPU estiver realizando sua jogada.

**A2.3.** O sistema exibe o status `"Computador pensando..."` e aplica uma animação visual de espera.

**A2.4.** O sistema aguarda aproximadamente 400 ms.

**A2.5.** O sistema calcula a jogada da CPU considerando as posições vazias.

**A2.6.** A CPU procura, nesta ordem:

1. uma posição que permita vencer imediatamente;
2. uma posição que bloqueie uma vitória de X;
3. o centro do tabuleiro;
4. um dos cantos disponíveis;
5. qualquer posição disponível.

**A2.7.** Caso exista uma posição válida, o sistema registra `O` nessa posição.

**A2.8.** O sistema reproduz o efeito sonoro da jogada de `O`.

**A2.9.** O sistema retorna ao fluxo principal para verificar vitória ou empate.

---

## A3. Reinício da Partida

**A3.1.** O jogador seleciona `"REINICIAR JOGO"`.

**A3.2.** O sistema cancela temporizadores pendentes de transição de rodada ou jogada da CPU.

**A3.3.** O sistema limpa todas as nove posições do tabuleiro.

**A3.4.** O sistema define `X` como jogador atual.

**A3.5.** O sistema define a partida como ativa.

**A3.6.** O sistema zera o placar de X e O.

**A3.7.** O sistema redefine a rodada para 1.

**A3.8.** O sistema remove a linha e o destaque visual da última vitória.

**A3.9.** O sistema fecha a janela de campeão, caso esteja aberta.

**A3.10.** O sistema remove os confetes ativos.

**A3.11.** O sistema atualiza a interface e exibe `"Vez do Jogador X"`.

---

## A4. Alteração do Modo de Jogo

**A4.1.** O jogador altera o seletor Modo de Jogo.

**A4.2.** O sistema atualiza a configuração para `pvp` ou `cpu`.

**A4.3.** O sistema reinicia integralmente a partida conforme o fluxo A3.

**A4.4.** Quando o modo Contra o Computador está ativo, o sistema altera o rótulo de O para `"Computador O"`.

---

## A5. Alteração do Formato da Partida

**A5.1.** O jogador altera o seletor Formato da Partida.

**A5.2.** O sistema atualiza a configuração para `single` ou `bo3`.

**A5.3.** O sistema reinicia integralmente a partida conforme o fluxo A3.

**A5.4.** No formato Partida Única, o indicador de rodada apresenta `1/1`.

**A5.5.** No formato MD3, o indicador apresenta inicialmente `1/3` e pode avançar até `3/3`.

---

## A6. Fechamento da Janela de Campeão

**A6.1.** Após a conclusão do MD3, o sistema exibe a janela de campeão.

**A6.2.** O jogador seleciona o botão `"FECHAR"`.

**A6.3.** O sistema oculta a janela de campeão.

**A6.4.** O estado encerrado da partida é mantido até que o jogador selecione `"REINICIAR JOGO"`.

**A6.5.** O jogador também pode fechar a janela clicando na área externa do cartão de campeão.

---

# 8. Fluxos de Exceção

## E1. Fim da Rodada por Empate

**E1.1.** No passo P7, o sistema não identifica uma combinação vencedora.

**E1.2.** O sistema verifica que todas as nove células estão preenchidas.

**E1.3.** O sistema encerra a rodada.

**E1.4.** O sistema exibe o status `"Rodada Empatada!"`.

**E1.5.** O sistema reproduz o efeito sonoro descendente de empate.

**E1.6.** Se o formato for Partida Única, o sistema mantém a partida encerrada até o reinício manual.

**E1.7.** Se o formato for MD3, o sistema aguarda aproximadamente 2 segundos.

**E1.8.** O sistema limpa o tabuleiro e inicia uma nova rodada sem atribuir ponto a nenhum jogador.

---

# 9. Pós-condições

## Ao término de uma rodada

- o resultado da rodada é apresentado na interface;
- o placar permanece armazenado;
- a combinação vencedora permanece visualmente destacada até a preparação da próxima rodada ou reinício;
- em caso de empate, nenhum jogador recebe ponto;
- em MD3, uma nova rodada pode ser iniciada enquanto nenhum jogador possuir duas vitórias.

## Ao término da partida

- em Partida Única, a rodada permanece encerrada;
- em MD3, quando um jogador alcança duas vitórias, o sistema identifica o campeão;
- o placar final permanece disponível na interface;
- o jogador pode fechar a janela de campeão;
- um novo jogo somente é iniciado mediante reinício ou alteração de configuração.

---

# 10. Requisitos Não Funcionais

## RNF-01 — Identidade Visual

A aplicação deve utilizar a identidade visual definida para o projeto, incluindo:

- Azul principal: `#003366`;
- Azul de destaque: `#0056b3`;
- Laranja: `#d97706`;
- Laranja claro: `#f59e0b`;
- Fundo: `#f4f6f9`.

A interface implementada utiliza ainda cartões, bordas arredondadas, sombras, gradientes e comportamento responsivo.

## RNF-02 — Portabilidade

A aplicação deve funcionar integralmente em um único arquivo `index.html`, contendo HTML, CSS e JavaScript, sem necessidade de servidor back-end ou arquivos externos para a execução das regras do jogo.

O arquivo atualmente possui aproximadamente 1.236 linhas no repositório e contém toda a implementação da interface e lógica.

## RNF-03 — Áudio

Os efeitos sonoros devem ser sintetizados exclusivamente por meio da Web Audio API, sem dependência de arquivos `.mp3`, `.wav` ou equivalentes.

A implementação utiliza osciladores e diferentes frequências para:

- jogada de X;
- jogada de O;
- vitória;
- empate.

## RNF-04 — Responsividade

A interface deve adaptar sua disposição a telas menores, reorganizando os controles, placar, tabuleiro e demais componentes para dispositivos móveis.

## RNF-05 — Acessibilidade

As células do tabuleiro devem possuir rótulos `aria-label`, indicando sua posição e, quando aplicável, o símbolo ocupado.

O status da partida deve utilizar `aria-live="polite"` para permitir a comunicação das alterações de estado aos recursos assistivos.

## RNF-06 — Feedback Visual

As ações do usuário devem produzir feedback visual por meio de:

- animação de inserção dos símbolos;
- mudança visual ao passar o cursor sobre células disponíveis;
- destaque das células vencedoras;
- linha de vitória;
- animação de confetes;
- indicador visual de que a CPU está pensando;
- janela de campeão no encerramento do MD3.

---

# 11. Ponto de Extensão

**Não se aplica.**

---

# 12. Frequência de Utilização

Uso recreativo e educacional frequente, especialmente em atividades acadêmicas de desenvolvimento web, engenharia de requisitos, testes de software e demonstrações de aplicações front-end.

---

# 13. Interface Visual

## IV1. Elementos Implementados

| ID | Elemento | Tipo | Comportamento |
|---|---|---|---|
| UI-01 | Identificação institucional | Texto | Exibe `"Universidade de Fortaleza"`. |
| UI-02 | Título | Heading | Exibe `"Jogo da Velha"`. |
| UI-03 | Modo de Jogo | `<select>` | Permite selecionar PVP ou Contra o Computador. |
| UI-04 | Formato da Partida | `<select>` | Permite selecionar Partida Única ou MD3. |
| UI-05 | Placar X | Valor numérico | Exibe vitórias acumuladas de X. |
| UI-06 | Rodada | Texto | Exibe a rodada atual e o total. |
| UI-07 | Placar O/CPU | Valor numérico | Exibe vitórias de O ou do Computador. |
| UI-08 | Status | Texto dinâmico | Informa turno, vitória, empate ou CPU pensando. |
| UI-09 | Tabuleiro | Grid 3 × 3 | Permite selecionar células vazias. |
| UI-10 | Linha de vitória | Overlay visual | É posicionada dinamicamente sobre as três células vencedoras. |
| UI-11 | Confetes | Canvas | Exibe partículas animadas após uma vitória. |
| UI-12 | Reiniciar Jogo | Botão | Reinicia estado, placar e rodada. |
| UI-13 | Janela de campeão | Modal/overlay | Exibe o vencedor definitivo do MD3 e o placar final. |
| UI-14 | Fechar campeão | Botão | Fecha a janela de campeão. |

A implementação atual contém todos esses componentes, incluindo o canvas de confetes e o modal de campeão.

---

# 14. Protótipo da Interface

```text
====================================================================
                    UNIVERSIDADE DE FORTALEZA
                         JOGO DA VELHA
             Desafie seus amigos ou enfrente o computador.
====================================================================

 [ Modo de Jogo: 2 Jogadores (PVP) ▼ ]
 [ Formato da Partida: Partida Única ▼ ]

 +---------------------------------------------------------------+
 | JOGADOR X             RODADA              JOGADOR O           |
 |    0                     1/1                    0              |
 +---------------------------------------------------------------+

                         Vez do Jogador X

                  +---------+---------+---------+
                  |         |         |         |
                  |         |    X    |         |
                  |         |         |         |
                  +---------+---------+---------+
                  |         |         |         |
                  |    O    |         |    X    |
                  |         |         |         |
                  +---------+---------+---------+
                  |         |         |         |
                  |    O    |    X    |         |
                  |         |         |         |
                  +---------+---------+---------+

                     [ REINICIAR JOGO ]

       X começa a partida. No modo contra o computador,
                         a CPU joga como O.
====================================================================
Em caso de vitória, a implementação acrescenta visualmente uma linha sobre as três células vencedoras, destaca essas células e executa os confetes.
```

# 15. Regras de Negócio

## RN-01 — Primeiro Jogador

O jogador X sempre inicia a partida e cada nova rodada.

## RN-02 — Ocupação

Uma célula ocupada não pode receber outra jogada.

## RN-03 — Vitória

Uma vitória ocorre quando um jogador possui três símbolos iguais em uma das oito combinações possíveis:

- três linhas;
- três colunas;
- duas diagonais.

## RN-04 — Empate

O empate ocorre quando todas as nove posições estão preenchidas e não existe combinação vencedora.

## RN-05 — Pontuação

Uma vitória incrementa em um ponto o placar do respectivo jogador.

Empates não alteram o placar.

## RN-06 — Partida Única

No formato Partida Única, a partida termina após vitória ou empate e permanece encerrada até o reinício.

## RN-07 — Melhor de 3

No formato MD3, o primeiro jogador a alcançar duas vitórias é declarado campeão.

## RN-08 — Empate no MD3

Um empate não atribui ponto e não incrementa a rodada. O tabuleiro é preparado para uma nova rodada.

## RN-09 — CPU

No modo Contra o Computador, X pertence ao jogador humano e O pertence à CPU.

A CPU aguarda aproximadamente 400 ms antes de realizar sua jogada.

## RN-10 — Estratégia da CPU

A CPU tenta:

1. ganhar imediatamente;
2. bloquear uma vitória de X;
3. ocupar o centro;
4. ocupar um canto;
5. selecionar outra posição vazia.

## RN-11 — Alteração de Configuração

A alteração do modo de jogo ou do formato da partida reinicia a partida e zera o placar.

## RN-12 — Reinício

O comando `"REINICIAR JOGO"` restaura todos os valores iniciais da partida.

---

# 16. Observações de Implementação

O estado principal da aplicação é mantido em um objeto contendo:

- `options`;
- `currentPlayer`;
- `running`;
- `winsX`;
- `winsO`;
- `currentRound`;
- `modeSelect`;
- `formatSelect`;
- temporizadores.

A detecção de vitória utiliza exatamente oito padrões:

- três linhas;
- três colunas;
- duas diagonais.

A linha de vitória é calculada dinamicamente a partir da posição geométrica das células no navegador, considerando distância e ângulo entre a primeira e a última célula da combinação.

Os confetes são produzidos diretamente por JavaScript em um elemento `<canvas>`, sem biblioteca externa de confetes.

A CPU não utiliza uma IA baseada em minimax. Sua estratégia implementada é uma heurística de cinco níveis:

1. vitória imediata;
2. bloqueio;
3. centro;
4. cantos;
5. posição disponível.

A janela de campeão é utilizada especificamente para comunicar o vencedor definitivo do formato MD3.

---

# 17. Matriz de Rastreabilidade

| ID Requisito | Funcionalidade / Comportamento | Passos CDU | Interface / Implementação | Validação |
|---|---|---|---|---|
| RF-01 | Seleção do modo de jogo | P3, A4 | UI-03 / `modeSelect` | `pvp` ou `cpu`. |
| RF-02 | Seleção do formato | P3, A5 | UI-04 / `formatSelect` | `single` ou `bo3`. |
| RF-03 | Marcação de jogada | P4–P6 | UI-09 / `makeMove()` | Célula vazia e partida ativa. |
| RF-04 | Alternância de turnos | P8–P9 | UI-08 / `currentPlayer` | Alterna X ↔ O. |
| RF-05 | Detecção de vitória | P7, A1 | `winPatterns` / `getWinningPattern()` | Oito padrões válidos. |
| RF-06 | Detecção de empate | P7, E1 | `isDraw()` | Todas as nove células preenchidas. |
| RF-07 | Linha de vitória | A1.3–A1.5 | UI-10 / `drawWinningLine()` | Linha calculada sobre as células vencedoras. |
| RF-08 | Destaque das células vencedoras | A1.5 | CSS `.winning` | Três células recebem destaque. |
| RF-09 | Confetes | A1.8 | UI-11 / Canvas | Partículas animadas após vitória. |
| RF-10 | Áudio de jogada | P6 | Web Audio API / `playMoveSound()` | Som sintetizado para X e O. |
| RF-11 | Áudio de vitória | A1.7 | Web Audio API / `playWinSound()` | Acorde sintetizado. |
| RF-12 | Áudio de empate | E1.5 | Web Audio API / `playDrawSound()` | Sequência sonora descendente. |
| RF-13 | Placar | A1.6 | UI-05 e UI-07 | Incremento do vencedor. |
| RF-14 | Transição de rodada | A1.13–A1.14 | UI-06 / `startNextRound()` | Limpa tabuleiro e mantém placar. |
| RF-15 | Vitória no MD3 | A1.11–A1.12 | UI-13 / `showChampion()` | Duas vitórias encerram o MD3. |
| RF-16 | Jogada da CPU | A2 | `scheduleCpuMove()` / `chooseCpuMove()` | Executada após 400 ms. |
| RF-17 | Estratégia da CPU | A2.5–A2.6 | `chooseCpuMove()` | Vitória, bloqueio, centro, canto ou posição livre. |
| RF-18 | Bloqueio durante CPU | A2.2 | UI-09 / `disabled` | Usuário não pode clicar durante turno O da CPU. |
| RF-19 | Reinício | A3 | UI-12 / `resetGame()` | Estado, placar e rodada zerados. |
| RF-20 | Alteração de modo | A4 | UI-03 | Alteração provoca reinício. |
| RF-21 | Alteração de formato | A5 | UI-04 | Alteração provoca reinício. |
| RF-22 | Identidade visual | RNF-01 | CSS | Cores institucionais. |
| RF-23 | Responsividade | RNF-04 | CSS Media Query | Adaptação para telas menores. |
| RF-24 | Acessibilidade | RNF-05 | `aria-label`, `aria-live` | Feedback semântico. |

---

# 18. Dicionário de Dados e Estrutura de Estado

| Variável | Tipo | Valor Inicial | Descrição |
|---|---|---|---|
| `state.options` | `Array(9)` | `["", "", "", "", "", "", "", "", ""]` | Representa as nove posições do tabuleiro. |
| `state.currentPlayer` | `String` | `"X"` | Jogador cujo turno está ativo. |
| `state.running` | `Boolean` | `true` | Indica se a rodada aceita jogadas. |
| `state.winsX` | `Integer` | `0` | Vitórias acumuladas de X. |
| `state.winsO` | `Integer` | `0` | Vitórias acumuladas de O ou CPU. |
| `state.currentRound` | `Integer` | `1` | Rodada atual. |
| `state.modeSelect` | `String` | `"pvp"` | Modo PVP ou CPU. |
| `state.formatSelect` | `String` | `"single"` | Partida Única ou MD3. |
| `state.transitionTimer` | `Timer/null` | `null` | Temporizador para transição entre rodadas. |
| `state.cpuTimer` | `Timer/null` | `null` | Temporizador da jogada da CPU. |
| `winPatterns` | `Array` | 8 combinações | Combinações possíveis de vitória. |
| `audioContext` | `AudioContext/null` | `null` | Contexto usado para geração dos efeitos sonoros. |
| `confettiParticles` | `Array` | `[]` | Partículas ativas do efeito de confetes. |
| `confettiAnimation` | `AnimationFrame/null` | `null` | Identificador da animação dos confetes. |

Esses elementos correspondem diretamente às estruturas presentes no `index.html`.

---

# 19. Critérios de Aceite

## CA-01 — Identidade Visual

A aplicação apresenta `"Universidade de Fortaleza"`, utiliza as cores institucionais especificadas e apresenta o título `"Jogo da Velha"`.

## CA-02 — Estado Inicial

Ao carregar ou reiniciar a aplicação, o tabuleiro está vazio, X inicia, o placar é `0 × 0` e a rodada é `1/1` ou `1/3`, conforme o formato.

## CA-03 — Ocupação

Uma célula já preenchida não pode ser sobrescrita.

## CA-04 — Bloqueio Pós-Rodada

Após vitória ou empate, não é possível realizar novas jogadas até a próxima rodada ou reinício.

## CA-05 — Alternância de Turnos

Em PVP, após cada jogada válida, o sistema alterna corretamente entre X e O.

## CA-06 — CPU

No modo Contra o Computador, a CPU realiza automaticamente sua jogada como O após aproximadamente 400 ms.

## CA-07 — Estratégia da CPU

A CPU prioriza vitória imediata, bloqueio de X, centro, cantos e demais posições disponíveis nessa ordem.

## CA-08 — Vitória

O sistema identifica corretamente as oito combinações vencedoras.

## CA-09 — Linha de Vitória

Ao ocorrer uma vitória, uma linha visual é posicionada sobre as três células vencedoras.

## CA-10 — Confetes

Ao ocorrer uma vitória, o sistema apresenta uma animação de confetes.

## CA-11 — Áudio

O sistema reproduz sons sintetizados para jogadas, vitória e empate sem depender de arquivos de áudio externos.

## CA-12 — Empate

Quando as nove células são preenchidas sem vencedor, o sistema informa `"Rodada Empatada!"` e reproduz o efeito sonoro de empate.

## CA-13 — Placar

Uma vitória incrementa apenas o placar do vencedor e um empate não altera os placares.

## CA-14 — MD3

No formato Melhor de 3, o primeiro jogador a alcançar duas vitórias é declarado campeão.

## CA-15 — Transição MD3

Quando ainda não houver campeão, o sistema limpa o tabuleiro após aproximadamente 2 segundos e inicia a próxima rodada mantendo o placar.

## CA-16 — Janela de Campeão

Ao terminar um MD3 por duas vitórias, o sistema exibe o campeão e o placar final em uma janela visual.

## CA-17 — Reinício

O botão `"REINICIAR JOGO"` zera placar e rodada, limpa o tabuleiro, remove efeitos visuais e define X como primeiro jogador.

## CA-18 — Alteração de Configuração

Alterar modo ou formato reinicia a partida e zera o placar.

## CA-19 — Responsividade

A interface permanece utilizável em telas menores.

## CA-20 — Acessibilidade

As células possuem rótulos acessíveis e as alterações de status podem ser comunicadas por tecnologia assistiva.

---

# 20. Checklist de Validação do Artefato

## 20.1 Estrutura

- [ ] Nome do caso de uso iniciado por verbo no infinitivo.
- [ ] Objetivo definido.
- [ ] Tipo do caso de uso definido.
- [ ] Atores identificados.
- [ ] Precondições definidas.
- [ ] Fluxo principal definido.
- [ ] Fluxos alternativos definidos.
- [ ] Fluxo de exceção definido.
- [ ] Pós-condições definidas.
- [ ] Requisitos não funcionais definidos.
- [ ] Regras de negócio identificadas.
- [ ] Critérios de aceite definidos.

## 20.2 Correspondência com a implementação

- [ ] Modo PVP implementado.
- [ ] Modo CPU implementado.
- [ ] Formato Partida Única implementado.
- [ ] Formato MD3 implementado.
- [ ] Placar implementado.
- [ ] Contador de rodadas implementado.
- [ ] Detecção das oito combinações vencedoras implementada.
- [ ] Detecção de empate implementada.
- [ ] Linha de vitória implementada.
- [ ] Destaque das células vencedoras implementado.
- [ ] Confetes implementados em Canvas.
- [ ] Áudio implementado com Web Audio API.
- [ ] Modal de campeão implementado.
- [ ] Reinício implementado.
- [ ] Alteração de configurações com reinício implementada.
- [ ] Responsividade implementada.
- [ ] Recursos básicos de acessibilidade implementados.

---

# 21. Matriz de Correspondência com o Código

| Componente do CDU | Implementação no `index.html` |
|---|---|
| Estado da partida | `state` |
| Combinações vencedoras | `winPatterns` |
| Atualização da interface | `updateInterface()` |
| Status | `setStatus()` e `updateTurnStatus()` |
| Vitória | `getWinningPattern()` |
| Empate | `isDraw()` |
| Linha de vitória | `drawWinningLine()` |
| Limpeza da linha | `hideWinningLine()` |
| Finalização de vitória | `finishRound()` |
| Finalização de empate | `finishDraw()` |
| Próxima rodada | `startNextRound()` |
| Jogada | `makeMove()` |
| CPU | `scheduleCpuMove()` |
| Estratégia da CPU | `chooseCpuMove()` |
| Reinício | `resetGame()` |
| Campeão MD3 | `showChampion()` |
| Fechamento do campeão | `closeChampion()` |
| Som | `getAudioContext()`, `playTone()`, `playMoveSound()`, `playWinSound()`, `playDrawSound()` |
| Confetes | `launchConfetti()` e `animateConfetti()` |

A correspondência acima foi obtida diretamente da implementação atual do arquivo `src/index.html`.

---

# 22. Referência da Implementação

A especificação foi revisada com base no arquivo `src/index.html` do repositório **jogo-da-velha-unifor**, disponível no GitHub.

O diretório `src` contém atualmente o arquivo `index.html`, e a versão analisada concentra nele a estrutura HTML, os estilos CSS e a lógica JavaScript da aplicação.

**Abrir o `src/index.html` no GitHub**

---

# 23. Observação de Consistência

Há um ponto da implementação que merece ser validado antes da entrega final do artefato:

> No fluxo de empate do MD3, `finishDraw()` agenda `startNextRound(false)` sem verificar se a partida já está na terceira rodada.

Assim, caso a terceira rodada termine empatada, o código atual pode iniciar novamente uma rodada mantendo o contador em `3/3`, em vez de encerrar definitivamente a disputa.

Portanto, o CDU acima descreve a intenção funcional do MD3, mas esse cenário específico deve ser corrigido ou explicitamente decidido pela equipe antes da implementação ser considerada totalmente aderente ao requisito **CA-05**.
