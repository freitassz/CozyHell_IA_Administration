# PROMPT ZIVA — Uva-morcego: o laser volta

## Contexto
A luta nova tirou o **laser pelo olho** do sorteio. O Gustavo quer o laser **de volta**. O código dele ainda está no `grape_boss.gd`.
- **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.

## O que fazer
1. **Volta para o sorteio:** pesos ⚙️ mergulho 2, chuva 1, **laser 1**. A garantia continua (3 ataques sem cair → mergulho).
2. **Mantenha o comportamento do laser antigo** (dano, duração, como ele mira/varre), só adaptando à altura de voo nova (8–12 m).
3. **Aviso de ≥ 1,2 s** antes de disparar (regra dos bosses): o olho acende vermelho (`EyeRed`) e aparece uma **linha fina de mira** (vermelha, pouco opaca) do olho até onde o laser vai acertar; ela pisca acelerando e fica **branca nos últimos 0,1 s**. Se o laser varre, mostre também no chão o **caminho da varrida** com a faixa vermelha.
4. **Fase 2:** o laser continua igual (só os 20% de velocidade entre ataques, sem encurtar o aviso).
5. Sinais novos para os sons: `laser_aviso` e `laser_inicio` / `laser_fim`.
6. Atualize o `dev/validate_uva`: laser no sorteio, aviso ≥ 1,2 s, linha de mira visível. Placar.

## Checklist
- [ ] Laser de volta no sorteio (peso 1) · [ ] Comportamento antigo mantido · [ ] Aviso ≥ 1,2 s com linha de mira
- [ ] Sinais `laser_aviso`, `laser_inicio`, `laser_fim` · [ ] Validador atualizado · Nada além disso foi alterado
