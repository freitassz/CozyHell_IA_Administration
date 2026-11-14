# Pedido para o chat de modelagem — Soco com a mão esquerda segurando arma

> Use a skill `lowpoly-game-3d-blender`. Pasta: `Blender\bracos_novo\` (scripts `bracos_v5.py`, `revolver_modelo.py`, `revolver_anim.py`).

## Contexto
No jogo, a tecla **V** faz um **soco rápido** com a arma na mão. O soco enche a barra de **Essência do Sonho** (+12 por acerto), então o jogador vai usar isso **o tempo todo** no meio do tiroteio.
Hoje, como não existe animação para isso, o jogo faz: guardar a arma → soco → sacar. Fica lento e feio.
Precisamos de uma animação em que **a mão direita continua segurando a arma** e **a mão esquerda entra na tela, dá o soco e sai**.

## O que fazer
Criar a ação **`Soco_Esquerdo_Arma`** nos braços (`bracos.glb`).

### Regra principal: reaproveitável em todas as armas
- A ação deve ter chave **só nos ossos do lado esquerdo** (`Raiz_L`, `Braco_L`, `Antebraco_L`, `Mao_L` e dedos `_L`).
- **Não chave** os ossos do lado direito nem `Arma_R`. Assim, no Godot, o braço direito continua na pose da arma que estiver na mão (revólver hoje, outras armas depois) e a mesma animação serve para todas.
- Exporte com `export_force_sampling=False` (como já é feito), para a ação gravar só os ossos com chave.
- Não precisa de ação nova no `revolver.glb`.

### Movimento (30 fps)
| Momento | Tempo ⚙️ | O que acontece |
|---|---|---|
| Início | 0,00 s | braço esquerdo **fora da tela**, abaixo à esquerda (igual à pose da arma, onde a esquerda nunca aparece) |
| Entrada | até ~0,10 s | sobe rápido, punho fechado (preset **punho**), antebraço já armando |
| **Impacto** | **~0,17 s** | punho no **centro-esquerda da tela**, um pouco abaixo da mira, braço quase esticado; **amasso no osso `Mao_L`** (escala, como nos socos atuais) |
| Volta | até ~0,40 s | recua e desce para fora da tela, com um pequeno exagero no fim (como em `02_2_Volta_*`) |
| Fim | ~0,40 s | **igual ao primeiro quadro** (fora da tela) — emenda = 0 |

- Estilo e pose do punho iguais aos socos aprovados (`02_1_2_Soco_Esquerdo`), mas **sem cruzar na frente da arma**: o soco não pode tapar o revólver nem a mira.
- Usar a câmera **calibrada pelo print do jogo** (`cam_fps`, FOV ~68°) nas prévias e desenhar a **cruz no centro da tela**.
- Lado esquerdo = espelho: rotações locais dos dedos com `Quaternion((w, x, -y, -z))`.

### Conferir
- Primeiro e último quadro iguais (diferença de `matrix_basis` = 0).
- A ação tem **só** ossos `_L` (conferir no JSON do glb).
- Prévia com o revólver na mão (pose `Revolver_Pose`) em 4–5 quadros: início, entrada, impacto, volta, fim.

## Entregar
1. `bracos.glb` atualizado (o único que muda) + `.py` atualizado.
2. Prancha de prévia com o revólver na mão.
3. **Dados para o prompt do Ziva** (trazer de volta para o chat de administração):
   - nome exato da ação;
   - duração (s) e número de quadros;
   - tempo do **impacto** (s);
   - lista de ossos com chave;
   - se o Godot precisa de algum cuidado para a mão direita não "voltar ao repouso" ao tocar essa ação (ex.: `AnimationPlayer` com `deterministic = false`, ou tocar com blend 0).
