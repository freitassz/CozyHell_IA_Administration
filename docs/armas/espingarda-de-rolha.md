# Espingarda de Rolha

- **Raridade:** Comum · **Status:** ✅ modelo + 7 animações · ✅ no jogo (polir depois)

## Conceito
Espingarda velha e enferrujada de fazendeiro que atira **rolhas**. Perto e forte. **Duas mãos.**

## Jogabilidade (valores iniciais — vêm da "Teste — Escopeta" que já funciona)
| Campo | Valor |
|---|---|
| Tipo | Projétil (rolhas), 70 m/s, gravidade 0,3 |
| Dano | 8 × 6 rolhas, dispersão 8° |
| Cadência / pente | 1,2/s · 2 |
| Recarga / custo | 1,8 s · 20 de Essência |
| Essência por acerto | 0,8 por rolha |
| Alcance eficaz / meia-vida | 10 m / 8 m |
| Mira | FOV 68 |
| Automática / carregável | não / não |
| `usa_duas_maos` | **sim** → V = **coronhada** |
| Especial | **Coice** (12 rolhas, empurra inimigos 6 m e joga o jogador 4 m para trás) |

## Visual
Aparência descrita pelo Gustavo no chat de modelagem. Regra: silhueta diferente da Metralhadora e do Rifle (ver pedido).

## Animações
`Espingarda_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar/Coronhada`.

## Dados da modelagem
`armas/espingarda/espingarda.glb` (raiz `EspingardaRig`). Cooldown 0,5 s (bombeia). Recarga 1,8 s: rolha 1 em 0,70 s, rolha 2 em 1,27 s, bombeia ~1,5 s. Coronhada 0,6 s, impacto 0,2 s. Ossos: `Bomba`, `Rolha`, `Gatilho`. Textura assada.
