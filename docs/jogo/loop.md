# Loop e progressão — v2

> Documento de design central. ✅ = aprovado pelo Gustavo · 🟡 = proposta, falta confirmar.

## História ✅ (ideia) / 🟡 (forma de contar)
O jogo é o **sonho de um fazendeiro**; as plantas se revoltam contra quem as planta e colhe. Cozy = sonho; Hell = pesadelo que se aprofunda com a progressão.
O pesadelo é mostrado como **progressão de jogo** (inimigos novos), não como mudança estética do mundo inteiro. ✅

## Loop curto
1. Explorar, coletar recursos, matar inimigos (spawn natural + pilares de inimigos).
2. Vender na **Caixa de Venda** (estação) → R$.
3. R$ → **máquina caça-níquel** → armas. Repetida → **sucata**.
4. Sucata + minérios + drops → **estações** (bancada, bigorna) → ferramentas, melhorias, armas de boss.
5. Ficou forte → oferenda (semente amaldiçoada 🟡) no **pilar de boss**.

## Loop longo: o que cada boss faz ✅
1. **Dropa uma ficha de raridade e libera essa raridade na máquina.** Ex.: Tomate morto → ficha de item Raro + a máquina passa a sortear Raros.
2. **Dropa material único**, usado na **próxima oferenda** ou numa **arma exclusiva de boss** (feita na estação, fora da máquina).
   - **Reinvocar boss ✅:** a primeira oferenda de cada boss é a difícil (usa o material do boss anterior). Depois de derrotado uma vez, a oferenda dele fica **mais simples, feita com itens comuns**, para lutar de novo e farmar material sem refazer a lista de bosses.
3. Bosses-chave **avançam o pesadelo**: o mundo passa a spawnar **inimigos novos** (como a Plantera no Terraria).
   - O avanço é anunciado com **uma animação pelo mundo + mensagem na tela** ✅, para o jogador perceber.

## Ordem dos bosses ✅
| # | Boss | Bioma | Libera |
|---|---|---|---|
| 1 | Tomate | Planície | ficha + **Raro** na máquina |
| 2 | Uva-morcego | Floresta | **Pesadelo fase 2**: inimigos novos passam a spawnar |
| 3 | Dragão-Pitaya | cava por qualquer bioma | ficha + **Épico** na máquina 🟡 |
| 4 | Batata-golem | Pedreira | ficha + **Lendário** na máquina 🟡 |
| 5 | Final (novo) | o pesadelo | fim da "campanha"; o mundo continua ✅ |

Todos dropam material único (oferenda / arma de boss).

## Minérios e picaretas ✅ (ideia) / 🟡 (detalhes)
- **4 minérios**, todos existem no mundo **desde o início** (o sistema de recursos não muda).
- O que trava é a **picareta**: cada minério exige uma picareta melhor, feita com drops de inimigos que só existem a partir de certa fase do pesadelo.
- Ex.: minério 3 precisa da picareta 3, que precisa de drop dos inimigos da fase 2 (pós Uva-morcego).
- **Uso ✅:** criar alguns itens, mas **principalmente armaduras** e afins.
- 🟡 Novo sistema a definir: **armaduras** (peças, o que dão, como aparecem em primeira pessoa/multiplayer).

## Economia 🟡
| Moeda | Ganha com | Gasta em |
|---|---|---|
| R$ | Caixa de Venda | máquina caça-níquel |
| Sucata | armas repetidas, desmontar | bigorna, construção |
| Minérios | pedreira (picareta certa) | **armaduras**, alguns itens |
| Drops de inimigo | inimigos por fase | picaretas, receitas |
| Material de boss | boss | oferenda seguinte ou arma de boss |

## Construção ✅ mais importância
- **Estações** (bancada, bigorna, Caixa de Venda…) fazem parte da progressão.
- **Base** (paredes, decoração, defesa) continua livre para quem quiser.
- 🟡 Falta a lista de estações e o que cada uma faz.

## Recursos do jogador
| Barra | Serve para | Enche com |
|---|---|---|
| Vida | — | — |
| Stamina ✅ | correr, pular, esquivar | sozinha |
| **Essência do Sonho** ✅ (nome provisório) | **recarregar** armas **e** soltar o **especial / tiro forte** | dano com tiro, **soco/corpo a corpo (muito mais)**, regeneração natural |

- É **uma barra só** para as armas (opção B, modelo Hollow Knight: a mesma SOUL cura e solta magia).
- Ideia do tema: as armas não têm munição de verdade — são **recarregadas com essência do sonho**.
- A cada momento o jogador escolhe: guardar essência para recarregar ou gastar num tiro forte.
- 🟡 Nome final a definir.
- "Calor/superaquecimento" veio da planilha de armas, que é **rascunho**: não faz parte do design até ser rediscutido.

## Morte ✅ (ideia)
Dois modos escolhidos ao criar o mundo/personagem:
- **Pesadelo** ✅ (hardcore): parecido com o Muck (morreu, perdeu). 🟡 Definir se apaga o mundo ou o personagem; no co-op, se vira espectador até reviverem.
- **Soneca** ✅ (leve): renasce perdendo parte dos itens e do dinheiro.
- 🟡 Atenção: "Pesadelo" também é o nome da progressão do mundo (fase 2 do pesadelo). Pode confundir; avaliar chamar a progressão de outra coisa (ex.: "Profundidade do sonho").

## Multiplayer ✅ (vai ter, se possível)
- Implementação fica para depois, mas o código novo já segue regras de multiplayer:
  - nada de `Engine.time_scale` (câmera lenta só visual/local);
  - inimigos e bosses miram o **jogador mais próximo**, nunca "o player";
  - estado do jogo num lugar só (host/servidor manda);
  - mundo gerado por **seed**.
- O "Relay" pago do Ziva é um **relay gerenciado para jogos Godot na Web**. Para PC/Steam não é necessário: o multiplayer do Godot é gratuito (ENet, `MultiplayerSpawner`, `MultiplayerSynchronizer`) e a Steam tem relay grátis (GodotSteam). O Ziva pode escrever esse código pelos prompts normais.
- 🟡 A decidir depois: roleta e drops por jogador ou compartilhados; vida do boss escala com nº de jogadores; no modo Pesadelo, morto vira espectador?
