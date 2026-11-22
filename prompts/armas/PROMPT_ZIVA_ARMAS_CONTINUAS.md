# PROMPT ZIVA — Armas contínuas: Lança-Chamas de Fogão + Mangueira de Água Amaldiçoada (cristal do sono)

## Contexto
Duas armas de **jato contínuo**, ainda sem modelo (visual provisório). Elas **não têm pente**: têm um **cristal do sono** que **escurece** enquanto atiram (superaquecimento). Depende do **status Queimar** (prompt "Tiros especiais").
- **Não mude o que não está pedido.** Uma etapa por vez. Comente em português. ⚙️ = valor escolhido por mim. Só no F3.

## ETAPA 1 — Tiro contínuo
- Novo `tipo_tiro`: **"Contínuo"**. Segurando o botão, aplica dano em **ticks** (`cadencia_tps` = ticks por segundo) a todos os inimigos num **cone/cápsula** à frente (`alcance_eficaz_m` = alcance do jato; campo novo `@export var largura_jato_graus := 20.0` ⚙️), até ⚙️ 5 inimigos por tick.
- Cada tick: `dano` (com nível/Fundir) + `aplica_status` se houver; `essencia_por_acerto` por inimigo por tick (máx. 3 inimigos).
- Sem recuo procedural forte (só uma vibração leve ⚙️).

## ETAPA 2 — Cristal do sono (superaquecimento)
- Campos: `@export var superaquece := false`, `@export var tempo_superaquecer_s := 4.0`, `@export var resfriamento_s := 3.0`.
- O **calor** sobe enquanto atira (0 → 1 em `tempo_superaquecer_s`) e desce sozinho quando solta (1 → 0 em `resfriamento_s`).
- Calor = 1 → **superaqueceu**: trava até o calor voltar a 0.
- **R** = recarrega o cristal **na hora** (calor vai a 0) gastando `custo_essencia_recarga`; sem Essência → aviso de sempre.
- Visual: se o modelo tiver o objeto/material `EssenciaMagica`, a cor dele vai do **lilás brilhante** (`#B98CFF`, calor 0) até **escuro** (calor 1). No provisório, use um bloquinho emissivo na arma. No HUD, o lugar do contador de balas mostra uma barrinha de calor.

## ETAPA 3 — As duas armas
| Campo | Lança-Chamas de Fogão | Mangueira de Água Amaldiçoada |
|---|---|---|
| Raridade | Épico | Lendário |
| Mãos | 2 (V = coronhada) | 2 (V = coronhada) |
| `dano` por tick / `cadencia_tps` | 6 / 12 | 10 / 10 |
| `alcance_eficaz_m` / `largura_jato_graus` | 8 / 20 | 12 / 12 |
| `aplica_status` | `queimar` | — (só dano) |
| `tempo_superaquecer_s` / `resfriamento_s` | 4 / 3 | 5 / 3 |
| `custo_essencia_recarga` (R no cristal) | 25 | 25 |
| `essencia_por_acerto` (por tick) | 0,2 | 0,3 |
| Especial | nenhum | depois |
| Visual provisório do jato | partículas de fogo laranja | jato de água **lilás-esverdeada** (amaldiçoada), partículas |

## ETAPA 4 — Teste automático
`dev/validate_continuas`: ticks por segundo, cone e máx. de alvos, Queimar no lança-chamas, calor sobe/desce, trava no 1 até voltar a 0, R zera gastando Essência. Placar.

## Checklist
- [ ] Tipo Contínuo com ticks e cone · [ ] Cristal: calor, trava, resfriamento, R com Essência, cor do `EssenciaMagica`
- [ ] Lança-Chamas (Queimar) e Mangueira (só dano) no F3 · [ ] Validador com placar · Nada além disso foi alterado
