# PROMPT ZIVA — Soco rápido com a mão esquerda (animação nova)

## Contexto
Hoje o soco rápido (**V**) com arma na mão faz: guardar → socar → sacar. Agora existe uma animação própria: **a mão direita continua segurando a arma e a esquerda dá o soco**.
Os arquivos `Blender\bracos_novo\bracos.glb` e `revolver.glb` foram **reexportados juntos**.

- **Não mude o que não está pedido.**
- **Faça uma etapa por vez e teste.**
- Comente o código em português.

## Dados da animação
| Item | Valor |
|---|---|
| Ação | `Soco_Esquerdo_Arma` (só no `bracos.glb`) |
| Duração | 0,40 s — 13 quadros a 30 fps |
| Impacto | **0,167 s** (quadro 5), amasso no osso `Mao_L` |
| Ossos com chave | `Braco_L`, `Antebraco_L`, `Mao_L`, `Indicador1_L`, `Indicador2_L`, `Dedos1_L`, `Dedos2_L`, `Polegar1_L`, `Polegar2_L` (nada do lado direito, nem `Raiz`, nem `Arma_L`) |
| Início e fim | iguais à mão esquerda escondida da `Revolver_Pose` (sem pulo) |

## Mudança nos .glb que afeta o código
As animações dos **dois** `.glb` começavam com **1 quadro parado** (1/30 s). Isso foi corrigido:
- soco em **0,167 s** (antes acontecia em 0,2 s), pegar do chão em **0,467 s**, `Revolver_Atirar` com **0,1 s**, `Revolver_Pose` com **2,0 s**;
- loops não travam mais.

---

## ETAPA 1 — Conferir os tempos depois da reexportação
- Confira se o `ArmaFps` e o `BracosFps` usam **durações fixas no código** (ex.: as fórmulas `vel_tiro = 0.40 * cadencia_tps`, `vel_recarga = 2.0 / recarga_s`, `vel_sacar = 0.40 / tempo_saque_s`, ou tempos de impacto fixos).
- Troque toda duração base fixa pela duração **lida da animação** (`anim.get_animation(nome).length`), para que futuras reexportações não quebrem o ritmo.
- Os tempos de impacto dos socos (`soco_impacto`) devem bater com 0,167 s (soco) e 0,467 s (pegar). Ajuste se o código usava os valores antigos.

**Teste:** revólver atira na cadência certa, recarrega no tempo do `WeaponData`, soco de mão nua acerta no impacto visível; `Revolver_Pose` em loop sem travadinha.

## ETAPA 2 — Segundo AnimationPlayer só para o braço esquerdo
**Não toque o soco no `anim_bracos`**: isso pararia a `Revolver_Pose` (mão direita congela ou volta ao repouso) e tiraria os braços de sincronia com o player da arma.

Crie um segundo player:
```gdscript
# AnimationPlayer só do braço esquerdo: roda DEPOIS do anim_bracos e sobrescreve apenas os ossos _L.
var anim_esquerda := AnimationPlayer.new()
anim_esquerda.name = "AnimEsquerda"
anim_bracos.get_parent().add_child(anim_esquerda)
anim_esquerda.root_node = anim_esquerda.get_path_to(anim_bracos.get_node(anim_bracos.root_node))

# Biblioteca própria, só com o soco: ele não conhece os ossos da direita.
var lib := AnimationLibrary.new()
lib.add_animation("Soco_Esquerdo_Arma", anim_bracos.get_animation("Soco_Esquerdo_Arma"))
anim_esquerda.add_animation_library("", lib)

anim_esquerda.deterministic = false
anim_esquerda.process_priority = anim_bracos.process_priority + 1
anim_esquerda.callback_mode_process = anim_bracos.callback_mode_process
```
- Toque com **blend 0**: `anim_esquerda.play("Soco_Esquerdo_Arma", 0.0)`.
- O `anim_bracos` e o player da arma **continuam** tocando `Revolver_*` normalmente: **dá para atirar durante o soco**.

**Teste:** com o revólver na mão, apertar V → a esquerda entra, soca e sai; a direita não se mexe; atirar durante o soco funciona.

## ETAPA 3 — Ligar no soco rápido (V)
- Com arma na mão, **V** toca `Soco_Esquerdo_Arma` no `anim_esquerda` (em vez de guardar → socar → sacar).
- O dano sai **aos 0,167 s** (pela posição da animação, como no soco de mão nua), com o **mesmo ShapeCast** do soco de mão nua e **+12 de Essência** por acerto.
- Cooldown do V continua 0,6 s ⚙️.
- No `WeaponData`, crie `@export var usa_duas_maos := false`. Se for `true`, use o **fallback antigo** (guardar → socar → sacar). Todas as armas de hoje ficam `false`.

**Teste:** V com cada arma de teste usa a animação nova; acertar um inimigo dá dano no impacto e +12 de essência.

---

## Checklist final
- [ ] Durações lidas das animações (sem tempos base fixos); ritmo do revólver igual ao esperado
- [ ] Impactos dos socos em 0,167 s e pegar em 0,467 s
- [ ] `AnimEsquerda` com biblioteca só do soco, `deterministic = false`, prioridade +1
- [ ] V com arma toca `Soco_Esquerdo_Arma`, mão direita parada, dá para atirar junto
- [ ] Dano no impacto + 12 de essência
- [ ] `usa_duas_maos` no `WeaponData` com fallback antigo
- [ ] Nada além disso foi alterado
