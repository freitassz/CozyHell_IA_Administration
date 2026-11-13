# Caça-níquel de pedra

- **Status:** ✅ implementado pelo Ziva · **Pasta:** `Blender\caçaniqueis\`
- **Tamanho:** ~2,4 m, alavanca em +X

## O que faz
Roleta de armas com fogo por raridade e 4 níveis de explosão.

## Modelo e rig
Ídolo no topo, tela inclinada (material `TelaRoleta`), glifo retrátil (osso `Glifo`), laterais com motivos variados.
Rig: `Root > Spin > Body > Lever / Idol / Glifo / FX_*`. `CTRL_Glow` / `CTRL_Crack` dirigem os morphs `EyeGlow` / `Cracks`.
Âncoras: 7× `FX_Fogo_*`, `FX_Tela`, `FX_Fumaca`, `FX_Explosao`, `FX_Item`.

## Animações
`Lever_Pull` → `Spin_Loop` → `Spin_Stop` → `Fail` ou `Explode_Start_Comum/Raro/Epico/Lendario`; `Fall_Start/Loop/Impact`.
Explosão: `cacaniquel_explosao.glb` (`Explode_Comum` só desmonta; Lendário tem onda de choque).

## Sons
12 sons em `sons\`. Prompts: `PROMPT_ZIVA.md`, `PROMPT_ZIVA_SONS.md`.

## Polimento opcional (Etapa 1)
- [ ] Som do fogo por raridade
- [ ] "Plim" ao sair a arma
