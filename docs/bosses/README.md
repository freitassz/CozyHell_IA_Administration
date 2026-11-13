# Bosses

**Ordem ✅:** 1 Tomate (Planície) → 2 Uva-morcego (Floresta, libera pesadelo fase 2) → 3 Dragão-Pitaya → 4 Batata-golem (Pedreira) → 5 Final (a criar; ideia: deus no céu) · ★ secreto: Totem de Melancia (10 vacas-melancia). Ver [loop.md](../jogo/loop.md).

| Boss | Modelo | Animações | Sons | Prompt Ziva | No jogo | Ficha |
|---|---|---|---|---|---|---|
| Dragão-Pitaya | ✅ | por código | ✅ | ✅ | ✅ | [dragao-pitaya](dragao-pitaya.md) |
| Tomate Boss | ✅ | ✅ | ⏳ | ⏳ | ⏳ | [tomate-boss](tomate-boss.md) |
| Uva-morcego | ✅ | ✅ | ⏳ | ⏳ | ⏳ | [uva-morcego](uva-morcego.md) |
| Batata-golem | ❌ refazer | ⏳ | ⏳ | ⏳ | ⏳ | [batata-golem](batata-golem.md) |

Modelos antigos (não feitos pelo Claude) que podem virar boss: PepperBoss (+ Fireball/FireBarrier), CowMellonBossTikiTiki.

## Pacote padrão de cada boss
1. Modelo + rig + animações em etapas, verificadas.
2. Âncoras FX, `*_dados.json` e mapa FX.
3. Explosão/morte em GLB separado, se fizer sentido.
4. Sons sincronizados em `sons\`.
5. `PROMPT_ZIVA.md` (lógica) e `PROMPT_ZIVA_SONS.md` (só sons).
6. Entrada (`boss_intro.tscn`) + barra (`boss_barra.tscn`).
7. Checklist de teste.
