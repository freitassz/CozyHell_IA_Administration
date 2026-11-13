# Braços em primeira pessoa (mão nua)

- **Status:** ✅ · **Pasta:** `Blender\bracos_novo\` (script atual `bracos_v5.py`; v4 = base sem arma)

## Arquivos no projeto
- `scripts/player/bracos_fps.gd` (`class_name BracosFps`): estados ESCONDIDO / GUARDA / SOCANDO / VOLTANDO / PEGANDO / GESTO + mola do pulo.
- `scenes/player/hand_models.tscn`: `HandsVisual/bracos` instancia `bracos.glb`; material toon `Mat_hand_cel`.
- `scripts/player/player.gd`: `configurar`, `atualizar_pulo`, `registrar_clique_soco`, `request_pegar`, `esconder`, `mostrar`; `_mao_nua_ativa()`.

Hierarquia: `Head/Camera3D/HandPivot` (bobbing) > `HandModels` (escala 3; pulo) > `HandsVisual` + visuais de ferramentas/armas.

## Regras
- Golpe sai **no impacto** (sinal `soco_impacto`), nunca no clique. Interações de clique (caça-níquel, mesa, monumento) continuam imediatas.
- `velocidade_soco` como `custom_speed`; impacto checado por `current_animation_position`.
- 4 s sem bater → mãos se escondem. Primeiro clique = `02_0_Surgir_Soco`.
- Pegar do chão com qualquer item, passando pelo escondido.

## Animações (30 fps)
`00_Escondido`, `01_0_Surgir`, `01_Pose_Bater` (loop), `02_0_Surgir_Soco`, `02_1_Soco_Direito`, `02_1_2_Soco_Esquerdo`, `02_1_3_Soco_Direito_Combo`, `02_2_Volta_Direito/Esquerdo`, `03_Pegar_Chao`, `03_2_Pegar_Escondido`, `05_Apontar`, `06_Joinha`, `07_Acenar`, `08_Empurrar`.

## Estilo aprovado
Peças arredondadas facetadas (8 lados), mão grande, indicador e polegar separados + bloco dos outros 3 dedos. Pele `#F2A48C`, palma `#E88A78`. Toon + contorno por casco invertido.

## Prompts entregues
`PROMPT_ZIVA_MAOS.md` → `_V2` → `_V3`.

## Pendente
- [ ] Poses próprias por item/arma
