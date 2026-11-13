# Inventário do que já existe no jogo

> Fase F1.5 ✅ fechada. Destino: ✅ manter · 🔧 ajustar · ❌ tirar · ⏭️ futuro · ⏸️ em aberto
> Fonte: levantamento do Ziva + catálogo do modo criativo (F3, 101 itens), nov/2026.
> Remoções viram pedido ao Ziva em [prompts/limpeza/PROMPT_ZIVA_LIMPEZA.md](../../prompts/limpeza/PROMPT_ZIVA_LIMPEZA.md).

## Ferramentas
| Item | Destino | Nota |
|---|---|---|
| Mãos Nuas | ✅ | braços FPS prontos |
| Picareta, Picareta de Ferro | 🔧 | escada de picaretas que libera minérios |
| Machado, Machado de Ferro | ✅ | |
| Enxada, Enxada de Ferro, Pá, Pá de Ferro | ❌ | eram do sistema de plantar |
| Vara de Pesca | ⏭️ | pesca como bônus, prioridade muito baixa |

## Armas
| Item | Destino | Nota |
|---|---|---|
| Revólver do Coveiro | 🔧 | único com modelo; redesign de estilo |
| Pistola, Rifle, Escopeta, Canhão de Batatas, Espada Enferrujada, Espada de Ferro, Foice, Marreta | ❌ | placeholders |
| Lista oficial | 🔧 | planilha (será atualizada) |

## Plantio
- **Ação de plantar do jogador: ❌ descontinuada** (junto com enxada e pá). Os inimigos continuam nascendo por spawn natural, monumentos, hordas noturnas e santuários.

## Inimigos (plantas)
| Fase | Inimigos | Liberada por |
|---|---|---|
| 1 | Tomate, Cenoura, Pimentão | início |
| 2 | Cebola, Milho, Abóbora | Uva-morcego (boss 2) |
| 3 | ⏸️ em aberto | ⏸️ |

- Variantes **Mutante / Ancestral**: ❌ descontinuadas.
- Batata (inimigo): ⏸️ em aberto até mexermos nas coisas da batata.
- Vaca-melancia (CowMellon): ✅ criatura especial espalhada pelo mapa; matar **10** invoca o boss secreto.
- Chuva: deixa inimigos mais fortes/rápidos ✅ (a implementar). Crescimento mais rápido ❌.

## Bosses
| Item | Destino | Nota |
|---|---|---|
| Sementes de chefe (Tomate Real, Hidra Picante, Golem de Raiz, Espantalho Vulcânico) | ⏸️ | ver no futuro; Hidra Picante é placeholder |
| Totem de Melancia | ✅ | **boss secreto**: aparece depois de matar 10 vacas-melancia |
| Ovos de invocação | ✅ | ferramenta do modo criativo |
| Boss final | ⏸️ | ideia: um **deus no céu** que observa e solta poderes; reserva: Espantalho Vulcânico |

## Drops de inimigos (antigas "comidas")
| Item | Destino | Nota |
|---|---|---|
| Batata Frita, Bolo de Cenoura, Cenoura Ralada, Molhos, Purê, Tomate Picado | 🔧 | placeholders; trocar nomes/função depois (**cozinhar na fogueira no futuro — não implementado**) |
| Troféu Supremo da Colheita | ⏸️ | |

## Recursos
| Item | Destino | Nota |
|---|---|---|
| Madeira, Pedra, Fibra, Carvão | ✅ | |
| Minério de Ferro → Barra de Ferro | ✅ | único minério; plano: 4 |

## Construções e estações
| Item | Destino | Nota |
|---|---|---|
| Bancada, Bigorna, Fornalha | ✅ | progressão |
| Baú, Cama | ✅ | cama = renascer no modo Soneca |
| Fogueira | ✅ | cozinhar no futuro |
| Paredes, Plataformas, Tetos | ✅ | base |
| Mesa de Contrato | ❌ agora / ⏭️ NPC | NPC que troca itens por **fichas de raridade** |
| Vendinha (`shop_stall` + `shop_ui`) | ❌ → 🔧 | não nasce mais no mapa; vira **construção de venda** que o jogador constrói. O desmanche de arma vai para a **bigorna** |

## Armaduras e acessórios
| Item | Destino | Nota |
|---|---|---|
| Armaduras Madeira/Pedra/Ferro | 🔧 | ajustar aos 4 minérios |
| 5 acessórios | ✅ 🔧 | caça-níquel próprio **mantido**; passam a **empilhar com limite** (5 a 10), podem ser retirados |

## Sistemas
| Coisa | Destino | Nota |
|---|---|---|
| Máquina de armas | ✅ 🔧 | níveis por boss |
| Máquina de acessórios | ✅ | acessórios empilham com limite |
| Loja (`unlock_pistol`) | ❌ | |
| Moedas = R$ | ✅ | |
| Pilar de boss, Monumento | ✅ | |
| **Santuários** (`SHRINE_DEFS`) = pilares de boss | 🔧 | ver tabela em [bosses/README](../bosses/README.md); hoje exigem 3 sementes tier ≥1 (temporário) e **somem** depois de usados |
| Arma repetida na máquina | 🔧 | dá bônus de dano **por categoria**, +0,15 cada, **sem limite**, não salvo; não vira sucata (✅ decidido) |
| Dia/noite + hordas noturnas | ✅ | |
| Geração procedural | 🔧 | seed variável |
| Menu principal / criação de mundo | 🔧 | não existe |
| Salvar / carregar | 🔧 | não existe — crítico |
