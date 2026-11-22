# Pedido para o chat de modelagem — Corpo a corpo: Cutelo Desgastado, Facão de Mato, Martelo da Vovó

> Siga também `PROMPT_BLENDER_REGRAS_ARMAS.md`. Aparência: o Gustavo descreve. Uma arma por vez: **Cutelo → Facão → Martelo**.

## Os tempos já foram testados no jogo — as animações precisam bater com eles
O golpe **começa no clique** (sem preparo, exceto o Martelo). O dano acontece na **metade final da varrida**. Depois vem a volta (que é a janela do combo).

| Arma | Mãos | Ações de golpe | Duração de cada golpe | Momento do acerto |
|---|---|---|---|---|
| **Cutelo Desgastado** (rápido) | 1 | `Cutelo_Golpe1`, `_Golpe2`, `_Golpe3` (combo de 3; corte curto horizontal, alternando o lado; o 3º mais forte) | 0,47 s = varrida 0,12 + volta 0,35 | 0,06–0,12 s |
| **Facão de Mato** (médio) | 1 | `Facao_Golpe1`, `_Golpe2` (combo de 2; corte diagonal largo, ida e volta) | 0,94 s = varrida 0,24 + volta 0,70 | 0,12–0,24 s |
| **Martelo da Vovó** (pesado) | 2 | `MarteloVovo_Preparo` (levanta, 0,4 s) · `MarteloVovo_Carga` (**loop** levantado, tremendo de leve) · `MarteloVovo_Golpe` (pancada de cima para baixo + volta) | Golpe: 3,28 s = varrida 0,48 + volta 2,80 | 0,24–0,48 s |

Também, para cada arma: `_Sacar`, `_Pose` (loop), `_Guardar`. Martelo (2 mãos): `MarteloVovo_Coronhada` (pancada curta com o cabo).
- Cutelo e Facão são de **1 mão**: a esquerda escondida como no revólver.
- A volta do Martelo (2,8 s) pode ficar mais curta no polimento: avise se a animação pedir outro tempo.

## Devolver
Bloco "Dados para o Ziva" das regras comuns, por arma.
