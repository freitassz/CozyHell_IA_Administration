# Uva-morcego

- **Status:** 🟡 luta em produção (modo rápido) · sons com prompts prontos
- **Envergadura:** ~6 m · **Etapa do roteiro:** 3

## Modelo
Corpo em icosfera, olho com shape key `EyeRed` (via `CTRL_Rage`), asas-folha com 2 ossos cada, caule e 5 uvas. Origem no centro; voo por código.

## Animações
- `Idle`, `Wander`
- `Attack_Start` / `Attack_Loop`
- `Dash_Start` / `Dash_Loop` → `Dash_Hit` (→ Wander) ou `Dash_Miss` (→ `Fallen_Loop`)
- `Fallen_Recover`
- Projétil: `grape_projectile.glb`

## Progressão ✅ (F4)
Santuário na Floresta · 1ª oferenda: Casca do Tomate + drop da Cenoura + drop do Pimentão · dropa Ficha Rara + Semente de Uva Sombria · libera a **fase 2 do pesadelo**.

## Luta (modo rápido — [prompt](../../prompts/bosses/PROMPT_ZIVA_UVA_MORCEGO.md))
- Voa em volta (8–12 m). **Chuva de uvas** (5, círculos de aviso, estouram em suco). **Mergulho** com olho vermelho e faixa: acertou → volta a voar; **errou → cai, 3 s caído com dano ×2**.
- Fase 2 sem texto: olho vermelho fixo, 2 mergulhos seguidos, chuva de 8.
- Entrada "Uva-morcego / A Sombra do Parreiral", barra `#7B3FA0`, vida 2200.
- Sons: [pedido](../../prompts/blender/PROMPT_BLENDER_SONS_UVA.md) → [Ziva](../../prompts/bosses/PROMPT_ZIVA_SONS_UVA.md).

## Ideias
- 
