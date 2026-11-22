# Pedido para o chat de modelagem — Arremessáveis: Machadinha Enferrujada e Espantalho Sonâmbulo

> Siga também `PROMPT_BLENDER_REGRAS_ARMAS.md`. Aparência: o Gustavo descreve. Os dois são de **1 mão** (esquerda escondida).

## Machadinha Enferrujada (Rara)
- No jogo: arremessada, faz curva da direita para a esquerda até o alvo e **volta para a mão** (o voo é por código).
- **Arquivos:** `machadinha.glb` (na mão, com rig da arma) — o **mesmo modelo** é usado voando (pode ser um nó/objeto sem rig dentro do glb, avise o nome).
- Ações: `Machadinha_Sacar`, `_Pose` (loop), `_Arremessar` (informe o **momento em que ela sai da mão**), `_Pegar` (informe o momento em que ela **chega na mão**), `_Guardar`. Enquanto ela voa, a mão fica vazia (pose de mão aberta esperando, pode ser o fim de `_Arremessar`).

## Espantalho Sonâmbulo (Lendário)
- No jogo: o jogador arremessa um espantalho que **finca no chão**, atrai os inimigos e solta **corvos** que voam até eles e explodem.
- **Arquivos:**
  1. `espantalho_mao.glb` — o espantalho pequeno/dobrado na mão. Ações: `Espantalho_Sacar`, `_Pose`, `_Arremessar` (momento em que sai da mão), `_Guardar`.
  2. `espantalho_fincado.glb` — no chão. Ações: `Fincar` (abre/levanta ao cair), `Idle` (loop, balançando), `Soltar_Corvo` (curta), `Sumir` (desmonta/vira palha). Osso **`FX_Corvo`** de onde o corvo sai.
  3. `corvo.glb` — ação `Voar` (loop). Nada perto do preto (corvo cinza-azulado ou outra cor que o Gustavo quiser).

## Devolver
Bloco "Dados para o Ziva" das regras comuns, para cada arquivo.
