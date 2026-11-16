# Pedido para o chat de modelagem — Família de armas de DUAS MÃOS (enferrujadas)

> Use a skill `lowpoly-game-3d-blender`. Pasta sugerida: `Blender\armas\<nome_da_arma>\` (ou junto de `bracos_novo\`, como preferir — avise).
> **A aparência de cada arma o Gustavo descreve neste chat.** Este pedido traz o estilo geral, as regras técnicas e o que o jogo precisa de cada arma.
> **Faça UMA arma por vez**, nesta ordem: **1. Espingarda de Rolha → 2. Metralhadora de Sementes → 3. Rifle de Pressão.** A primeira define o padrão das armas de duas mãos.

## Estilo geral (guia aprovado — `docs/armas/guia-estilo.md`)
- Roça + magia do sono: armas de fazendeiro velhas, **enferrujadas**, sucateadas, remendadas. Não são de brinquedo, mas são **mais leves**.
- Paleta forte e clara ("sonho feliz"); nada perto do preto (só o contorno).
- Cor chapada por vértice, **sem textura**, poucos detalhes. **Fosco e sem reflexo** (roughness 1, specular 0, metallic 0).
- Magia/cristal é **opcional** (só se o Gustavo pedir). Se tiver, objeto/material separado `EssenciaMagica`.
- Brilho, fumaça, faíscas = efeitos no Godot.

## ⚠️ As três se parecem (todas enferrujadas) — regra de silhueta
Na primeira pessoa o jogador precisa saber **qual arma está segurando só pela forma**. Cada uma deve ter uma silhueta própria, por exemplo:
- **Espingarda:** curta e grossa, cano(s) largo(s).
- **Metralhadora:** volume em cima (reservatório de sementes, estilo paintball).
- **Rifle de Pressão:** a mais **longa** e fina, com luneta.
Confira as três lado a lado em primeira pessoa (câmera do jogo) antes de fechar a segunda e a terceira.

## O que muda nas armas de duas mãos (novo padrão)
- A **mão esquerda segura a arma** (guarda-mão/cano) em todas as ações — ela **não** fica escondida como no revólver.
- O soco rápido (V) **não** usa o `Soco_Esquerdo_Arma`: cada arma tem a sua **coronhada** (`<Arma>_Coronhada`, golpe com a coronha/cabo para a frente), com **tempo de impacto** informado.
- Mão direita no cabo/gatilho; mão esquerda derivada da arma (como a direita no revólver), para nada escorregar.

## Regras técnicas (iguais ao revólver)
- Arma = **.glb separado** com rig próprio, presa no osso `Arma_R` (transform zerado no Godot).
- Osso **`Cano`** na ponta do cano (origem do rastro/projétil). Cano **paralelo à câmera** (mira no centro), prévias com a **câmera calibrada do jogo** e a cruz no centro.
- Correção de eixo da exportação (rig da arma com `rotation_euler = (90°, 0, 0)`, conferir `Cano` em +Y no glb).
- Ações com **mesmo nome e duração** nos dois .glb (braços e arma), **sem quadro parado no início**, emendas verificadas (= 0). `bracos.glb` e o glb da arma **sempre juntos**.
- O **recuo do tiro é procedural** no Godot: `_Atirar` pode ser curta e sutil (mecanismo da arma: cão, bomba, gatilho).
- `export_force_sampling=False`.

## Ações de cada arma
`<Arma>_Sacar`, `_Pose` (loop), `_Atirar`, `_Cooldown`, `_Recarregar`, `_Guardar`, **`_Coronhada`**.
Prefixos: `Espingarda_`, `Metralhadora_`, `RiflePressao_`.

| Arma | Recarga deve mostrar (sugestão, o Gustavo pode mudar) | Duração base da recarga |
|---|---|---|
| Espingarda de Rolha | abre o cano e coloca rolhas | ~1,8 s |
| Metralhadora de Sementes | enche/troca o reservatório de sementes | ~2,0 s |
| Rifle de Pressão | **bombeia** o ar (alavanca) e põe o projétil | ~2,2 s |

(O código ajusta a velocidade pela duração real lida da animação — pode variar, mas avise.)

## Entregar (por arma)
1. `<arma>.glb` + `bracos.glb` (se as ações novas dos braços forem nele) + `.py`.
2. Prancha: lateral, 3/4 e **primeira pessoa** (câmera do jogo), e — a partir da 2ª arma — as armas lado a lado em primeira pessoa.
3. **Dados para o Ziva** (trazer ao chat de administração):
   - nome do arquivo e do nó raiz;
   - lista de ações com **duração (s)** e nº de quadros;
   - **tempo de impacto da coronhada**;
   - em que momento do `_Recarregar` o pente "enche" (se não for no fim);
   - ossos especiais (ex.: reservatório, bomba) e se o `Cano` está certo;
   - material `EssenciaMagica` (se existir).
