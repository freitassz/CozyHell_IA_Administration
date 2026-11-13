# Bosses

**Ordem ✅:** 1 Tomate (Planície) → 2 Uva-morcego (Floresta, libera pesadelo fase 2) → 3 Dragão-Pitaya → 4 Batata-golem (Pedreira) → 5 Final (a criar; ideia: deus no céu) · ★ secreto: Totem de Melancia (10 vacas-melancia). Ver [loop.md](../jogo/loop.md).

| Boss | Modelo | Animações | Sons | Prompt Ziva | No jogo | Ficha |
|---|---|---|---|---|---|---|
| Dragão-Pitaya | ✅ | por código | ✅ | ✅ | ✅ | [dragao-pitaya](dragao-pitaya.md) |
| Tomate Boss | ✅ | ✅ | ⏳ | ⏳ | ⏳ | [tomate-boss](tomate-boss.md) |
| Uva-morcego | ✅ | ✅ | ⏳ | ⏳ | ⏳ | [uva-morcego](uva-morcego.md) |
| Batata-golem | ❌ refazer | ⏳ | ⏳ | ⏳ | ⏳ | [batata-golem](batata-golem.md) |

Modelos antigos (não feitos pelo Claude) que podem virar boss: PepperBoss (+ Fireball/FireBarrier), CowMellonBossTikiTiki.

## Santuários no jogo hoje (`SHRINE_DEFS`) × plano
| # | Santuário | Cena | Recompensa hoje | No plano? |
|---|---|---|---|---|
| 1 | Tomate Gigante | `tomato_boss.tscn` | `boss_seed_1a` | ✅ boss 1 |
| 2 | Hidra Picante | `hidra_picante.tscn` | `boss_seed_1b` | ❌ placeholder |
| 3 | Golem de Raiz | `golem_raiz.tscn` | `boss_seed_2a` | ≈ Batata-golem (boss 4)? |
| 4 | Espantalho Vulcânico | `espantalho_vulcanico.tscn` | `boss_seed_2b` | reserva |
| 5 | Deus da Colheita Abissal | `deus_colheita.tscn` | Troféu da Colheita | ≈ boss final ("deus no céu") |

- Ativa com E, consome 3 sementes (tier ≥1, temporário) e o santuário **some**.
- **Uva-morcego** e **Dragão-Pitaya** não têm santuário (só ovo do criativo).
- ⚠️ "Santuário some" conflita com a decisão de **reinvocar boss** com oferenda simples.
- Posições com a seed fixa `556677869`: 197–329 m do spawn.

## Pacote padrão de cada boss
1. Modelo + rig + animações em etapas, verificadas.
2. Âncoras FX, `*_dados.json` e mapa FX.
3. Explosão/morte em GLB separado, se fizer sentido.
4. Sons sincronizados em `sons\`.
5. `PROMPT_ZIVA.md` (lógica) e `PROMPT_ZIVA_SONS.md` (só sons).
6. Entrada (`boss_intro.tscn`) + barra (`boss_barra.tscn`).
7. Checklist de teste.
