# Regras comuns para TODAS as armas (chat de modelagem)

> Leia junto com o pedido da categoria. Use a skill `lowpoly-game-3d-blender`. **A aparência de cada arma o Gustavo descreve no chat.**

## Estilo
- Roça + magia do sono: coisas de fazendeiro velhas, sucateadas, remendadas. Não é de brinquedo, mas é leve.
- Cores fortes e claras; nada perto do preto (só o contorno). Cor chapada, sem textura (ou textura assada que continue chapada). **Fosco e sem reflexo.**
- Magia/cristal **opcional**; quando houver peça mágica, objeto/material separado **`EssenciaMagica`**.
- Brilho, fogo, fumaça, faíscas = efeitos no Godot, não no modelo.

## Técnica
- Arma = `.glb` separado com rig próprio, presa no osso **`Arma_R`** com transform zerado (se fizer mais sentido outro encaixe, avise).
- Ações com **mesmo nome e duração** nos braços e na arma (prefixo `<Arma>_`), **sem quadro parado no início**, emendas = 0, 30 fps; `bracos.glb` e o glb da arma **sempre juntos**; `export_force_sampling=False`.
- Armas de tiro: osso **`Cano`** na saída do tiro, apontando para a frente, **paralelo à câmera**; correção de eixo da exportação como nas outras armas.
- **1 mão:** mão esquerda **escondida na mesma pose do revólver** em todas as ações (o soco esquerdo depende disso). **2 mãos:** a esquerda segura a arma e existe a ação **`_Coronhada`** (golpe curto para a frente/esquerda, sem tapar a mira).
- A arma fica à direita da tela por ajuste no Godot: modele com a pegada atual.
- Recuo do tiro é procedural no Godot: `_Atirar` curta e sutil.
- Prévias com a **câmera calibrada do jogo** e a cruz no centro. **Uma imagem de teste antes de animar.**

## Devolver sempre (bloco "Dados para o Ziva")
Arquivo e nó raiz · osso de encaixe · ações com duração (s) e nº de quadros · tempos dos eventos (tiro/arremesso, impacto, munição/cristal na recarga) · ossos especiais · `EssenciaMagica` (se houver).
