# Pedido para o chat de modelagem — Revólver do Coveiro v2 (redesign de estilo)

> Use a skill `lowpoly-game-3d-blender`. Pasta: `Blender\bracos_novo\` (`revolver_modelo.py`, `revolver_anim.py`).
> **Como a arma vai parecer, o Gustavo explica neste chat** (referências e descrição). Este pedido traz só o **estilo geral** e as **regras** a seguir.

## Contexto
O revólver atual (aço escuro, madeira escura, latão) tem cara de arma real e **destoa** do mundo claro do jogo.
Foi aprovado um **guia de estilo das armas**. O revólver é a **primeira arma** redesenhada com ele.

## Estilo geral (guia aprovado)
- **Tema:** roça + magia do sono — armas de fazendeiro velhas, sucateadas, remendadas, com toque mágico.
- **Proporções:** não é de brinquedo, mas é **mais leve**; silhueta reconhecível em primeira pessoa.
- **Paleta "sonho feliz":** cores **fortes e claras**; **nada perto do preto** (só o contorno é escuro).
- **Materiais:** formas puramente de cor (cor por vértice), **sem textura**, poucos detalhes modelados. **Fosco e sem reflexo** (roughness 1, specular 0, metallic 0).
- Brilhos, fumaça, faíscas = **efeitos no Godot**, não no modelo.
- A raridade **não** aparece no modelo.
- Se o Gustavo pedir uma **peça mágica**, ela deve ser um **objeto/material separado** chamado `EssenciaMagica` (o Godot vai acendê-la na recarga e no especial).

## Regras técnicas (o código depende disso — não mudar)
- Mesmos **ossos** e nomes: `Raiz > Cao, Gatilho, Tambor > Giro > Carga, Tambor > Extrator, Balas, Cano`.
- Mesmas **ações**, nomes e durações: `Revolver_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar`, **sem quadro parado no início**. Se precisar mudar alguma duração, avise.
- **Empunhadura no mesmo lugar** (encaixe no `Arma_R` com transform zerado; a mão direita não pode atravessar o cabo).
- Osso **`Cano`** na ponta do cano; cano **paralelo à câmera** (mira no centro da tela).
- Correção de eixo da exportação (`RevolverRig` com `rotation_euler = (90°, 0, 0)`), escala de exportação da arma e `ESC=1` dos braços.
- **Mão esquerda escondida** na mesma pose de hoje em todas as ações (o soco rápido `Soco_Esquerdo_Arma` depende disso).
- `bracos.glb` e `revolver.glb` **sempre juntos** se algum mudar.
- Prévias com a **câmera calibrada do jogo** e a cruz no centro.

## Fluxo
1. Analisar as referências do Gustavo.
2. Mandar **uma imagem de teste** (render pequeno, 1 vista em primeira pessoa) antes de mexer nas animações.
3. Iterar uma mudança por vez.

## Entregar
1. `revolver.glb` novo (+ `bracos.glb` se precisar reexportar junto), `.py` atualizados.
2. Prancha: vista lateral, 3/4 e **em primeira pessoa**, lado a lado com o revólver antigo.
3. **Dados para o Ziva** (trazer para o chat de administração): nome do material da peça mágica (se houver), se algum osso/ação/duração mudou, e qualquer cuidado na troca.
