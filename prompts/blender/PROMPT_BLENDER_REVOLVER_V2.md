# Pedido para o chat de modelagem — Revólver do Coveiro v2 (redesign de estilo)

> As **referências** visuais serão enviadas pelo Gustavo diretamente neste chat.
> Use a skill `lowpoly-game-3d-blender`. Pasta: `Blender\bracos_novo\` (`revolver_modelo.py`, `revolver_anim.py`).

## Contexto
O revólver atual (aço `#525A5F`, madeira `#8E3B2B`, latão) tem cara de arma real e **destoa** do mundo claro e "sonho feliz" do jogo.
Foi criado um **guia de estilo das armas** (abaixo, resumido). O revólver é a **primeira arma** redesenhada com ele e serve de teste do guia.

## Guia de estilo (resumo)
- **Tema:** roça + magia do sono. Revólver **velho, enferrujado e "cabreiro"** de fazendeiro, remendado na gambiarra, mas ainda com cara de arma (não de brinquedo), um pouco **mais leve**.
- **Paleta forte e clara:** metal pintado `#8FB3C9` ou `#9ED8B5`, metal cru `#B8C2CC`, ferrugem em **manchas chapadas** `#E07B39`/`#C9622B`, madeira mel `#D9A15B`/`#A8693A`, remendos (fita `#E5484D`/`#F2C94C`, arame `#C8CDD2`). Nada perto do preto.
- **Materiais:** só formas e cores chapadas (cor por vértice), **sem textura**, **fosco e sem reflexo** (roughness 1, specular 0, metallic 0). Detalhes extras serão efeitos no Godot.
- **Peça mágica ✅:** o **tambor vira um pote de vidro lilás** `#B98CFF` (ou, se ficar ruim, um frasco lilás preso com arame). É onde a Essência do Sonho "entra". Deve ser um **objeto/material separado** chamado `EssenciaMagica`, para o Godot fazer acender na recarga e no especial. Continua girando com o osso `Tambor`/`Giro`.
- Metal **pintado em azul ou verde-menta claros, com a tinta descascando**; ferrugem em **manchas laranja chapadas**; madeira **cor de mel**; **fitas coloridas** nos remendos; nada perto do preto.

## O que NÃO pode mudar (o código depende disso)
- Mesmos **ossos** e nomes: `Raiz > Cao, Gatilho, Tambor > Giro > Carga, Tambor > Extrator, Balas, Cano`.
- Mesmas **ações**, nomes e durações: `Revolver_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar` (sem quadro parado no início — correção já feita).
- **Empunhadura no mesmo lugar** (encaixe no `Arma_R` com transform zerado; a mão direita não pode atravessar o cabo).
- Osso **`Cano`** na ponta do cano; cano **paralelo à câmera**.
- Correção de eixo da exportação (`RevolverRig` com `rotation_euler = (90°, 0, 0)`), escala de exportação e `ESC=1` dos braços.
- `bracos.glb` e `revolver.glb` **sempre juntos** se algum mudar.
- A mão esquerda continua escondida na pose (o soco esquerdo depende disso).

## Referências
O Gustavo vai mandar as imagens neste chat. Analise a referência antes de modelar e mande **uma imagem de teste** (render pequeno, 1 vista em primeira pessoa) antes de refazer as animações.

## Entregar
1. `revolver.glb` novo (+ `bracos.glb` se precisar reexportar junto), `.py` atualizados.
2. Prancha: vista lateral, 3/4 e **em primeira pessoa** (câmera do jogo, cruz no centro), lado a lado com o revólver antigo.
3. **Dados para o Ziva:** nome do material da peça mágica, se algum osso/ação mudou (não deveria), e qualquer cuidado na troca.
