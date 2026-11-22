# PROMPT ZIVA — Espantalho Sonâmbulo (torreta lendária) com visual provisório

## Contexto
Arma **Lendária** de **uma mão**: o jogador **arremessa** um espantalho que **finca no chão**, **atrai os inimigos** para ele e **solta corvos** que voam até os inimigos e **explodem**. Ainda sem modelo.
- **Não mude o que não está pedido.** Uma etapa por vez. Comente em português. ⚙️ = valor escolhido por mim. Multiplayer: o espantalho pertence a quem jogou. Só no F3.

## ETAPA 1 — Arremessar e fincar
- Clique: arremessa (projétil com arco, ⚙️ 15 m/s, gravidade 1) e **finca** onde tocar o chão (fica em pé, alinhado ao chão). Só 1 espantalho por jogador ao mesmo tempo.
- "Recarga" = tempo até poder pôr outro (`recarga_s` ⚙️ 12 s, conta a partir do arremesso), gastando `custo_essencia_recarga` ⚙️ 30 ao arremessar.
- Dura ⚙️ 10 s e some (pequena nuvem de palha). Tem vida ⚙️ 150: se os inimigos destruírem antes, some.

## ETAPA 2 — Atrair inimigos
- Inimigos comuns dentro de ⚙️ 15 m **trocam o alvo** para o espantalho enquanto ele existir (bosses **não** são atraídos ⚙️). Quando ele some, voltam ao jogador mais próximo.

## ETAPA 3 — Corvos
- A cada ⚙️ 1,5 s, solta 1 corvo que voa (teleguiado, ⚙️ 12 m/s) até o inimigo mais próximo em 15 m e **explode** ao chegar: ⚙️ 40 de dano, raio 2 m (usa a explosão do prompt "Tiros especiais"; não fere o jogador). Sem inimigo, não solta.
- Essência: 3 por inimigo atingido pela explosão (máx. 3).

## ETAPA 4 — Visual provisório e ficha
- Espantalho: estaca + travessa (cruz) em bloco madeira clara com um "chapéu" bloco; balança de leve. Corvo: forma pequena cinza-azulada (nada perto do preto) com bater de asas simples.
- Ficha **"Espantalho Sonâmbulo"** (Lendário, 1 mão, V = soco com a esquerda, sem especial).

## ETAPA 5 — Teste automático
`dev/validate_espantalho`: finca no chão, 1 por jogador, atrai comuns e não bosses, corvos saem a cada 1,5 s e explodem, dura 10 s, destruído por dano. Placar.

## Checklist
- [ ] Arremessa e finca · [ ] Atrai inimigos comuns em 15 m · [ ] Corvos explosivos · [ ] Duração, vida, recarga 12 s e custo 30
- [ ] Ficha no F3 · [ ] Validador · Nada além disso foi alterado
