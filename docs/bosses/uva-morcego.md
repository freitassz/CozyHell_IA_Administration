# Uva-morcego

- **Status:** 🟡 modelo + animações ✅ · sons ⏳ · prompt Ziva ⏳
- **Envergadura:** ~6 m · **Etapa do roteiro:** 3

## Modelo
Corpo em icosfera, olho com shape key `EyeRed` (via `CTRL_Rage`), asas-folha com 2 ossos cada, caule e 5 uvas. Origem no centro; voo por código.

## Animações
- `Idle`, `Wander`
- `Attack_Start` / `Attack_Loop`
- `Dash_Start` / `Dash_Loop` → `Dash_Hit` (→ Wander) ou `Dash_Miss` (→ `Fallen_Loop`)
- `Fallen_Recover`
- Projétil: `grape_projectile.glb`

## Comportamento (a definir)
- [ ] Padrão de voo e ataques
- [ ] Janela de dano (provavelmente `Fallen_Loop` após errar o dash)
- [ ] Entrada, barra, drops

## Ideias
- 
