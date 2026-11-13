# Visão geral do jogo

> Pitch, público e pilares: [identidade.md](identidade.md).

- **Gênero:** sobrevivência FPS focado em tiro, inspirado em Muck.
- **Sistemas:** máquina caça-níquel de armas, construção (em desenvolvimento), biomas e geração procedural (quase prontos). Multiplayer: futuro.
- **Conteúdo planejado:** 5 bosses, ~8 inimigos.

- **Engine:** Godot 4 (GDScript). Código escrito pelo **Ziva AI**.
- **Câmera:** primeira pessoa.
- **Estilo:** low-poly facetado, cores vivas e chapadas, grama verde-limão clara, terreno **irregular** (morros).
- **HUD:** vida, dinheiro (R$), sucata, defesa, dia/hora, minimapa.
- **Modo criativo (F3):** dá itens como "Ovo: Dragão-Pitaya (Boss)" para spawnar bosses.

## Pastas do projeto Godot (`3dddddd`)
`Blender`, `enemies`, `scenes`, `scripts`, `SFX`, `VFX`, `shaders`, `Terrain`, `ui`, `resources`, `addons`.

Assets entregues vão para `3dddddd\Blender\<subpasta do asset>\` (sons em `<subpasta>\sons\`).
Não deixar GLBs duplicados/antigos lá: o Godot importa tudo.

## Cores de raridade
| Raridade | Cor |
|---|---|
| Comum | `#3DDC4A` |
| Raro | `#2F8BFF` |
| Épico | `#A23DFF` |
| Lendário | `#FFD21F` |

## Coordenadas
- Blender (x, y, z) → Godot (x, z, −y).
- Modelos com a frente em **−Y no Blender** = **+Z no Godot**.
- Peças de corrente: frente em −Z no Godot (`Basis.looking_at`).

## Escalas de referência
- Boss ~5 m · inimigo comum ~1,7 m · objeto ~2,4 m.
- Bosses podem ser reescalados (o dragão ficou 3x): todo prompt tem uma variável `escala`.
