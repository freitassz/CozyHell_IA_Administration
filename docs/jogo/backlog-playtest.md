# Backlog do 1º playtest (Gustavo, nov/2026)

> 28 itens + 1 bug visto nos prints. Agrupados em **lotes** (1 prompt do Ziva por lote, ou pedido de modelagem/arte). Tamanho: P pequeno · M médio · G grande. Status: ⏳ pendente · 🟡 prompt pronto · ✅ feito.

## Lote 1 — Fluidez de gameplay ✅ [prompt](../../prompts/mundo/PROMPT_ZIVA_LOTE1_FLUIDEZ.md)
| # | Item | Tam. |
|---|---|---|
| 7 | Recursos mais difíceis de quebrar (árvore/pedra) para dar vontade de fazer machado e picareta | P |
| 11 | **Aumentar o alcance** do corpo a corpo (hoje precisa colar demais, parece que daria para acertar) | P |
| 13 | **Economia mais difícil** (preços de compra ↑, ganho de venda ↓) | P |
| 15 | **Jogador morre → o boss vai embora**; reinvocar só pede os itens **comuns** | M |
| 24 | **Stamina** de movimento + **pulo no deslize mantém o momentum, gastando stamina** (sem agachar+pular infinito) | M |
| 2 | **Nenhum recurso renasce perto de construções** (ex.: árvore no meio da casa) | P |

## Lote 2 — HUD e telas 🟡 prompts: [2A HUD+inventário+crafting](../../prompts/mundo/PROMPT_ZIVA_LOTE2A_HUD_INVENTARIO.md) (#4, #14) · [2B mundo sem texto, caça-níquel, auras, bug](../../prompts/mundo/PROMPT_ZIVA_LOTE2B_MUNDO_SEM_TEXTO.md) (#8, #5, #20, B1)
| # | Item | Tam. |
|---|---|---|
| 4 | **HUD intuitivo** (vida, dinheiro claro, inventário, crafting) | G |
| 8 | **Tirar textos em cima das coisas** — tudo óbvio sem escrever na tela | M |
| 14 | **Descrição de cada item** no inventário; armaduras mostram **defesa e bônus** | M |
| 5 | **Caça-níquel:** tela **totalmente escura** até ativar; só aparece o item ao girar | P |
| 20 | **Totem/santuário** de cada boss reconhecível (**aura** do boss em vez de só estátua) | M |
| B1 | 🐞 Texto gigante "**Cama (recarregando…)**" cobrindo a tela (print 2) | P |

## Lote 3 — Natureza viva 🟡 prompts: [3A árvores/pedras/arbustos/drops](../../prompts/mundo/PROMPT_ZIVA_LOTE3A_NATUREZA_DROPS.md) (#1, #21, #3) · [3B fauna](../../prompts/mundo/PROMPT_ZIVA_LOTE3B_FAUNA.md) (#6)
| # | Item | Tam. |
|---|---|---|
| 1 | **Árvores:** copa maior sem engrossar o tronco; **animação de cair** para o lado em que bate; sem **cepo** | M |
| 21 | Animações também em **pedras e arbustos** ao quebrar | M |
| 6 | **Vaca-melancia:** drop + rework; novos animais pacíficos (**porcos**, **pássaros no céu**) | G |
| 3 | **Drops** não são blocos amarelos: dar forma/ícone a cada drop | M |

## Lote 4 — Terreno, grama e água ⏳
| # | Item | Tam. |
|---|---|---|
| 18 | Grama **flutuando em penhascos** | P |
| 19 | Atirar/cortar o chão com lâmina **corta a grama** e deixa o chão "pelado" | M |
| 25 | **Blend/textura do terreno** mal renderizado (formas duras, baixa resolução) → textura suave | M |
| 27 | **Mais variedade de montanhas** (print 4: todas iguais) | M |
| 22 | **Água realista**, **barra de fôlego**, e inimigo que mata quem tenta **sair da ilha nadando** | G |

## Lote 5 — Colisão e inimigos ⏳
| # | Item | Tam. |
|---|---|---|
| 12 | **Colisão** de todos os inimigos e bosses ajustada aos modelos | M |
| 26 | Colisão das **árvores** | P |
| 23 | **Rework de todos os inimigos** (agressivos demais, feios ou com animação esquisita) | G |

## Lote 6 — Construção ⏳
| # | Item | Tam. |
|---|---|---|
| 9 | **Snap grid ligável/desligável** na construção (print 3: "GRID") para colocar peças livres | M |
| 10 | **Modelos 3D** das construções e dos minérios novos (substituir placeholders) | G (modelagem) |

## Lote 7 — Arte e áudio (modelagem / shader) ⏳
| # | Item | Tam. |
|---|---|---|
| 16 | Melhorar o **outline** das coisas ou **remover** de vez | M |
| 17 | **Shader novo** (pixelado ou outro estilo) | M |
| — | **Sound design** (hoje existe, mas "não será assim") | G |
| 10 | Modelos novos e embelezar os existentes | G |

## Futuro
| # | Item |
|---|---|
| 28 | **Multiplayer** + **corpo físico** para o jogador (ver `docs/sistemas/` e regras de multiplayer) |
| — | Deus (boss final) — por último |

## Interpretações assumidas (ajustáveis)
- **#15:** se o **jogador morre durante a luta**, o boss **vai embora** (some com efeito) e o santuário volta a poder ser usado com a **oferenda de reinvocar (3 drops comuns)**, mesmo que o boss nunca tenha sido derrotado. A 1ª vitória continua dando fichas, material e liberações.
- **#24:** a stamina de movimento já existia (correr/pular); aqui ela passa a ser **visível** e usada no pulo do deslize.
- **#4/#8:** o objetivo é **comunicar por forma, cor e ícone**, não por texto; textos só em menus (Guia, NPCs).
