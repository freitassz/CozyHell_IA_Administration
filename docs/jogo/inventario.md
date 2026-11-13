# Inventário do que já existe no jogo

> Fase F1.5: listar tudo o que já está no projeto e decidir o destino **antes** de criar algo novo.
> Destino: ✅ manter · 🔧 ajustar · ❌ tirar · ❓ decidir. Destinos marcados com * são **proposta do Claude**.
> Fonte: levantamento feito pela IA do Godot (Ziva), nov/2026.

## Player
| Coisa | Estado hoje | Destino | Nota |
|---|---|---|---|
| Braços FPS (soco, pegar, gestos) | pronto | ✅* | |
| Stamina (correr, pular) | existe | ✅ | |
| Vida | existe | ✅ | |
| **Armaduras** | existem: madeira 5%, pedra 10%, ferro 16% de redução **por peça** | 🔧* | base do sistema de armaduras (P10) já existe; ajustar aos 4 minérios |
| **Acessórios** | existem (ex.: `DEFENSE_BOOST`) | ❓ | itens passivos — quais existem? como se ganha? |
| Defesa (HUD) | "Defesa: N% de redução de dano" = armaduras + acessórios | ✅* | |
| Ferramentas: pá, enxada, machado, picareta | ? | ❓ | picareta vai ter níveis |

## Armas (`resources/items/weapons/`)
| Arma | Tipo | Destino | Nota |
|---|---|---|---|
| Pistola (`pistol`) | hitscan, dano 45, cooldown 0,25 s, alcance 50 m | ❓ | desbloqueada na loja (`unlock_pistol`), sai em máquinas e na Mesa de Contrato |
| Revólver do Coveiro (`revolver`) | — | 🔧 | visual + animações prontos; redesign de estilo |
| Escopeta de Cano Duplo (`shotgun`) | — | ❓ | |
| Rifle Automático de Fazendeiro (`rifle`) | — | ❓ | |
| Canhão de Batatas Ancestral (`potato_cannon`) | — | ❓ | já está no tom "gambiarra da roça" |
| Espada Enferrujada (`sword`) | corpo a corpo | ❓ | |
| Espada de Ferro (`iron_sword`) | corpo a corpo | ❓ | |
| Foice de Colheita Brutal (`scythe`) | corpo a corpo | ❓ | |
| Marreta Pesada (`warhammer`) | corpo a corpo | ❓ | |
| Sistema de tiro (munição/recarga) | recarga infinita | 🔧 | vai usar Essência do Sonho |

## Formas de conseguir arma (⚠️ sobreposição)
| Fonte | O que faz | Destino | Nota |
|---|---|---|---|
| Máquina caça-níquel | sorteia armas; repetida → sucata | ✅ | fonte principal; níveis por boss |
| **Mesa de Contrato / Armeiro** (`WeaponTrader`) | painel de contratos de armas | ❓ | o que é um contrato? compete com a máquina? |
| **Loja** (`unlock_pistol`) | desbloqueia armas | ❓ | onde fica? o que vende? |
| Bigorna | fabrica armas e ferramentas por combinação de itens, sem dinheiro | ✅* | lugar natural das **armas de boss** |

## Mundo
| Coisa | Estado hoje | Destino | Nota |
|---|---|---|---|
| Geração procedural (`IslandGenerator`) | quase pronta; **seed fixa** `556677869` | 🔧* | seed aleatória/escolhida (multiplayer e mundos novos precisam) |
| Biomas: Planície, Floresta, Pedreira | quase prontos | ✅ | |
| Minérios | ? | ✅ | quantos existem hoje? plano: 4 |
| Ciclo dia/noite (`DayNightCycle`) | dia = 12 min reais; noite 20h–5h; shader de céu | ✅* | |
| **Hordas noturnas** (`NightSpawnManager`) | inimigos perto do jogador à noite; fogem ao amanhecer | ✅* | muito Muck, combina; multiplayer: "perto **dos** jogadores" |
| Clima (`WeatherSystem`) | chuva dobra o crescimento das plantações | ❓ | |
| **Plantações** | existem (crescem, chuva acelera) | ❓ | são as sementes que viram inimigo ou é agricultura de verdade? |
| Monumento (`EnemyMonument`) | E → 3–5 inimigos em 7 m; limpo → moedas; pode sumir | ✅* | é o "pilar de inimigos" |
| Pilares de boss + oferenda | ? | ✅ | existe no jogo ou só na ideia? |
| Spawn natural de inimigos | existe | ✅ | |

## Economia e estações
| Coisa | Estado hoje | Destino | Nota |
|---|---|---|---|
| Máquina(s) caça-níquel | pronta | 🔧 | níveis por boss |
| Repetida → sucata | existe | ✅ | |
| Caixa de venda (no mapa) | existe | 🔧 | virar estação fabricável |
| Moedas (drop do monumento) | existe | ❓ | é o mesmo que R$? |
| Bancada (`Workstation`) | receitas a até 5 m | ✅* | |
| Bigorna (`AnvilStation`) | UI própria; armas/ferramentas por combinação | ✅* | |
| Fornalha (`furnace_station`) | UI própria | ✅* | provavelmente fundir minério → barras para armadura |
| Construção de base | em desenvolvimento | ✅ | |

## Inimigos e bosses
| Coisa | Estado hoje | Destino | Nota |
|---|---|---|---|
| Dragão-Pitaya | pronto | ✅ | boss 3 |
| Tomate Boss | modelo + anim | ✅ | boss 1 |
| Uva-morcego | modelo + anim | ✅ | boss 2 |
| Batata-golem | refazer | ✅ | boss 4 |
| Milho | modelo + anim | ❓ | |
| PepperBoss, CowMellonBossTikiTiki | antigos | ❓ | |
| CowMellon, Carrot, Onion, pepper, Tomato | antigos | ❓ | |

## Interface e estrutura
| Coisa | Estado hoje | Destino | Nota |
|---|---|---|---|
| HUD (vida, R$, sucata, defesa, dia/hora, minimapa) | existe | ✅* | + barra de Essência do Sonho |
| Menu de pausa (ESC) | volume; aba gráficos é placeholder; sair | 🔧* | |
| Modo criativo (F3) / debug | existe | ✅ | ferramentas de teste |
| **Menu principal / tela de título** | ❌ não existe (abre direto no `main.tscn`) | 🔧* | necessário |
| **Criação de mundo** (seed, Soneca/Pesadelo) | ❌ não existe | 🔧* | necessário |
| **Salvar / carregar** | ❌ não existe | 🔧* | **crítico** para mundo persistente |
