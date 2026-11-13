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
3. Bosses-chave **avançam o pesadelo**: o mundo passa a spawnar **inimigos novos** (como a Plantera no Terraria).

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
- 🟡 Falta definir: para que serve cada minério (melhorias na bigorna? armas de boss? construção?).

## Economia 🟡
| Moeda | Ganha com | Gasta em |
|---|---|---|
| R$ | Caixa de Venda | máquina caça-níquel |
| Sucata | armas repetidas, desmontar | bigorna, construção |
| Minérios | pedreira (picareta certa) | ferramentas, melhorias, construção |
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
| **Energia** ✅ | recarregar armas (🟡 e ataque especial?) | dano com tiro, **soco/corpo a corpo (muito mais)**, regeneração natural lenta |
| Calor | armas contínuas | esfria sozinho |

🟡 Em discussão: usar a Energia também para o especial (ver C04 em `revisao.md`).

## Morte ✅ (ideia)
Dois modos escolhidos ao criar o mundo/personagem:
- **Hardcore:** parecido com o Muck (morreu, perdeu). 🟡 Definir se apaga o mundo ou o personagem; no co-op, se vira espectador até reviverem.
- **Modo leve ("baby"):** renasce perdendo parte dos itens e do dinheiro. 🟡 Sugestão de nomes temáticos: **"Soneca"** (leve) e **"Pesadelo"** (hardcore).
