# Loop e progressão — proposta v1

> Documento de design central. Status: 🟡 proposta do Claude em cima das ideias do Gustavo; itens marcados ❓ precisam de confirmação.

## A história amarra tudo
O jogo é o **sonho de um fazendeiro**. As plantas se revoltam contra ele porque ele é quem planta, colhe e come.
- **Cozy** = o sonho bom do começo: campo claro, colorido, fofo.
- **Hell** = o sonho virando **pesadelo**. A cada boss derrotado o sonho fica mais fundo e mais estranho.
- Por ser sonho, **armas absurdas e improvisadas** (rolha, panela de pressão, relógio de cuco) fazem sentido. Isso resolve o choque de estilo: as armas não precisam ser realistas, precisam ser **coisas de fazendeiro que viraram armas no sonho**.

## Loop curto (minuto a minuto)
1. Explorar, coletar recursos e matar inimigos (spawn natural + pilares de inimigos).
2. Vender na **Caixa de Venda** → R$.
3. R$ → **máquina caça-níquel** → armas.
4. Arma repetida → **sucata** (já existe).
5. Sucata + materiais → **bigorna** → melhorar armas.
6. Ficou forte → oferenda no **pilar de boss**.

## Loop longo (os saltos de poder, estilo Terraria)
Cada boss derrotado faz **três coisas**:

| O que | Exemplo | Por quê |
|---|---|---|
| 1. **Abre um novo nível da máquina** | antes do 1º boss a máquina só sorteia Comum/Raro; depois entra Épico; mais tarde Lendário | o salto de poder vem da máquina, que é o coração do jogo |
| 2. **Dropa um material único** | "Casca do Tomate", "Escama de Pitaya" | usado na bigorna para melhorar armas e para fazer a **oferenda do próximo boss** (isso define a ordem, como os itens de invocação do Terraria) |
| 3. **Aprofunda o pesadelo** | céu e névoa mudam de cor, inimigos novos ou mais fortes, minérios novos na pedreira | o mundo muda, o jogador sente que avançou |

Depois do boss final o mundo continua (como no Terraria), no nível máximo de pesadelo.

### Níveis (rascunho ❓)
| Nível | Liberado por | Máquina sorteia | Mundo |
|---|---|---|---|
| 0 — Sonho | início | Comum, Raro | claro, cozy |
| 1 | Boss 1 | + Épico | primeiros sinais de pesadelo |
| 2 | Boss 2 | mais chance de Épico | inimigos novos |
| 3 | Boss 3 | + Lendário | pedreira profunda / minérios novos |
| 4 | Boss 4 | mais chance de Lendário | noite pesada |
| Final | Boss 5 (final) | tudo | pesadelo total, mundo continua |

## Economia
| Moeda | Ganha com | Gasta em |
|---|---|---|
| **R$** | vender recursos e drops na Caixa de Venda | máquina caça-níquel |
| **Sucata** | armas repetidas, desmontar coisas | bigorna (melhorias), construção |
| **Material de boss** | matar o boss | bigorna (melhoria de nível alto) e oferenda do próximo boss |

A sucata garante que **o azar não trava a progressão**: toda rodada da máquina vale alguma coisa.

## Estações × construção de base
Separar duas coisas:
- **Estações** (bancada, bigorna, Caixa de Venda): fazem parte da progressão. São itens que o jogador **coloca onde quiser**, sem precisar de base. A Caixa de Venda vira uma estação que o jogador fabrica (também dá para achar no mapa no começo).
- **Base** (paredes, chão, decoração, defesa): **opcional**, para quem gosta. Não trava nada.

Assim a construção ganha um papel sem virar obrigação.

## Armas: munição e energia
- Munição infinita, mas **recarregar gasta energia** (barra estilo Hollow Knight, enche ao causar dano). ✅ já decidido.
- **Risco:** errou os tiros → não ganhou energia → pente vazio → não consegue atirar → morre. É uma espiral de frustração.
- **Rede de segurança proposta:**
  - golpes corpo a corpo (soco e armas corpo a corpo) enchem **muito** mais energia — "corpo a corpo para recarregar, tiro para matar" (modelo do Doom Eternal, que funciona). Isso dá ao corpo a corpo um **papel claro** num jogo de tiro;
  - regeneração passiva bem lenta da barra, ou recarga lenta grátis com a barra vazia (escolher uma).
- **Brecha:** com várias armas, o jogador troca em vez de recarregar. Aceitável (o tempo de saque já pesa), mas o pente **não enche** ao trocar.
- Armas que superaquecem não usam energia; o resfriamento é o limite delas.

## Stamina
- **Proposta:** stamina só para **correr/esquivar/pular**, regenera sozinha (como no Muck). O ataque especial passa a usar **só cooldown**.
- Isso simplifica (um recurso a menos ligado às armas) e elimina a necessidade da máquina de cerveja.
