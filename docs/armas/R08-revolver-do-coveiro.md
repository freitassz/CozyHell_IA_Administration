# R08 — Revólver do Coveiro

- **Nicho:** Pistola / revólver · **Raridade:** Raro
- **Status:** 🟡 visual na mão ✅ · lógica de dano/WeaponData ⏳

## Arquivos (`3dddddd\Blender\bracos_novo\`)
- `revolver.glb`, `revolver_modelo.py`, `revolver_anim.py`
- Prompt: `PROMPT_ZIVA_REVOLVER.md`

## Montagem no Godot
`HandsVisual/bracos/BracosRig/Skeleton3D/EncaixeArma` (`BoneAttachment3D`, bone `Arma_R`) > `Revolver` (transform zerado; escala 3 vem do `HandModels`).
Clarão / origem visual do tiro: `BoneAttachment3D` no osso `Cano`.

## Animações
`Revolver_Sacar`, `Revolver_Pose`, `Revolver_Atirar`, `Revolver_Cooldown`, `Revolver_Recarregar`, `Revolver_Guardar`.
Recarga cartunesca com uma mão (tranco abre o tambor, cápsulas caem, volta cheia). Mão esquerda nunca aparece.

## Modelo
Aço `#525A5F`, madeira `#8E3B2B`, latão `#D8A73C` (cor por vértice). Ossos: `Raiz > Cao, Gatilho, Tambor > Giro > Carga, Tambor > Extrator, Balas, Cano`.

## Lições
- Cano paralelo à câmera (mira no centro da tela).
- Eixo: `RevolverRig` exportado com `rotation_euler = (90°, 0, 0)`.
- Antes de culpar o código do Ziva, ampliar o print — o erro era da pose/câmera.
