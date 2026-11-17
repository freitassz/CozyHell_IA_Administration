# Metralhadora de Sementes

- **Raridade:** Comum · **Status:** ✅ modelo + 7 animações · ✅ no jogo (polir depois)

## Conceito
Parecida com uma **arma de paintball**, mas atira **sementes**. Enferrujada. **Automática.** **Duas mãos.**

## Jogabilidade (valores iniciais sugeridos)
| Campo | Valor |
|---|---|
| Tipo | Projétil (sementes), 80 m/s, gravidade 0,15 |
| Dano | 9, dispersão 3° |
| Cadência / pente | 9/s · 40 |
| Recarga / custo | 2,0 s · 25 de Essência |
| Essência por acerto | 0,5 |
| Alcance eficaz / meia-vida | 25 m / 20 m |
| Mira | FOV 60 |
| Automática | **sim** (recuo baixo e acumulado, com limite) |
| `usa_duas_maos` | **sim** → V = **coronhada** |
| Especial | — |

## Visual
Aparência descrita pelo Gustavo. Ideia de partida: o "reservatório" de sementes em cima, como o de paintball.

## Animações
`Metralhadora_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar/Coronhada`.

## Dados da modelagem
`armas/metralhadora/metralhadora.glb` (raiz `MetralhadoraRig`). Cooldown 0,1 s. Recarga 2,0 s: pote recolocado em 1,33 s. Coronhada 0,6 s, impacto 0,2 s. Ossos: `Reservatorio`, `Gatilho`. Textura assada. ⚠️ Na recarga o pote fica grande na tela por um instante (avaliar jogando).
