# PROMPT ZIVA — Ajuste 1 do corpo a corpo (tempos)

## Contexto
O Gustavo testou as três armas. O Cutelo está rápido demais e o Facão e o Martelo não passam a sensação de peso. Só mudam **tempos** e **quando o golpe acerta**.
- **Não mude o que não está pedido.**
- Comente o código em português.

## 1. Novos tempos (no `WeaponData` de cada arma)
| Arma | `tempo_ativo_s` | `tempo_recuperacao_s` | Total |
|---|---|---|---|
| Cutelo Desgastado | **0,12** (era 0,08) | **0,35** (era 0,18) | 0,47 s — o tempo que o Facão tinha |
| Facão de Mato | **0,24** (era 0,12) | **0,70** (era 0,35) | 0,94 s — o dobro |
| Martelo da Vovó | **0,48** (era 0,12) | **2,80** (era 0,70) | 3,28 s — o quádruplo |

O visual provisório do golpe acompanha esses tempos (a varrida dura o `tempo_ativo_s`).

## 2. Quando o golpe acerta
Com o ativo mais longo, o dano **não pode** sair no clique (o bloco ainda está no começo da varrida). Regra nova:
- O golpe **começa no clique** (sem espera, a varrida já começa), mas **só acerta** quando passa na frente do jogador: nos **últimos 50%** do `tempo_ativo_s` ⚙️ (campo novo `inicio_acerto := 0.5`, fração do ativo).
- Cutelo: acerta entre 0,06 s e 0,12 s · Facão: 0,12–0,24 s · Martelo: 0,24–0,48 s.
- Martelo carregado: a carga continua sendo segurar; ao soltar, o mesmo ativo de 0,48 s e o acerto na metade final.
- Hitstop, tremida, lascas e essência continuam iguais, no momento do acerto.

## 3. Teste
- Atualize o `dev/validate_corpo_a_corpo` para os tempos novos e para o acerto na metade final do ativo. Me diga o placar.

## Checklist
- [ ] Tempos novos nas 3 armas
- [ ] `inicio_acerto` (0,5): o golpe começa no clique e acerta na metade final da varrida
- [ ] Validador atualizado e placar
- [ ] Nada além disso foi alterado
