# PROMPT ZIVA — Tiros especiais: Rifle de Pregos (perfuração), Lança-Rojão Junino (explosão), Lampião (fogo) + status Queimar

## Contexto
Três armas de tiro com mecânicas novas, ainda **sem modelo** (use o visual do revólver ou da arma de duas mãos mais parecida como provisório, como foi feito com as armas de teste).
- **Não mude o que não está pedido.** Faça **uma etapa por vez** e teste. Comente em português. Tudo em `WeaponData`/`@export`. ⚙️ = valor escolhido por mim.
- Multiplayer: status e explosões pertencem a quem atirou; nada de `Engine.time_scale`.
- Só no F3 por enquanto (fora da máquina).

## ETAPA 1 — Status Queimar (base para Lampião e Lança-Chamas)
- Componente de status nos inimigos e bosses. **Queimar:** ⚙️ 3 de dano por segundo durante 4 s; **não empilha** (um novo Queimar **renova** a duração). Sinal `status_aplicado(alvo, "queimar")`.
- Visual: partículas de fogo pequenas no inimigo (sem cubos) + leve tom laranja; somem ao acabar.
- Campo no `WeaponData`: `@export var aplica_status := ""` (ex.: `"queimar"`) e `@export var chance_status := 1.0`.
- O dano do Queimar **não** dá Essência (só o acerto direto dá).
**Teste:** um inimigo queimando perde 12 de vida em 4 s; acertar de novo renova sem dobrar.

## ETAPA 2 — Rifle de Pregos (perfuração)
- Campos: `@export var perfura_alvos := 0` (quantos inimigos **a mais** o tiro atravessa) e `@export var perda_dano_perfuracao := 0.25` (cada inimigo atravessado tira 25% do dano para o próximo) ⚙️.
- Tiro instantâneo continua pelo raio da câmera, mas **não para** no 1º inimigo: atravessa até `perfura_alvos` inimigos; para em parede/chão.
- Ficha **"Rifle de Pregos"** (Épico, 2 mãos, V = coronhada): dano 22, `perfura_alvos` 2 (acerta até 3), dispersão 1,5°, cadência 4/s, pente 20, recarga 1,6 s, custo 15, essência/acerto 1, eficaz 40 / meia-vida 35, FOV 55, sem especial (Pregar fica para depois).
- Rastro: termina no **último** inimigo atravessado (ou na parede).
**Teste:** 3 inimigos em fila: o 1º leva 22, o 2º 16,5, o 3º 12,4; o 4º não leva.

## ETAPA 3 — Lança-Rojão Junino (explosão)
- Campos: `@export var raio_explosao_m := 0.0`, `@export var dano_borda_explosao := 0.5` (na borda do raio o dano cai para 50%) ⚙️, `@export var empurrao_explosao_m := 0.0`.
- Projétil explode ao tocar inimigo/chão/parede (ou ao fim do `tempo_vida_projetil_s`). Dano em área com queda até a borda; cada inimigo leva no máximo 1 vez. **O jogador não toma dano da própria explosão** ⚙️.
- Visual provisório: rojão = cilindro fino colorido com rastro de faíscas coloridas; explosão = flash + **confete e faíscas coloridas** (cores fortes do jogo, sem cubos) + tremida de câmera se perto.
- Ficha **"Lança-Rojão Junino"** (Épico, 2 mãos): dano 80, raio 4 m, empurrão 1,5 m, cadência 0,8/s, pente 1, recarga 1,5 s, custo 20, essência/acerto 3 (por inimigo atingido, máx. 3), projétil 30 m/s, gravidade 0,5, eficaz 60 / meia-vida 50, FOV 62, sem especial.
**Teste:** grupo de 5 inimigos: os do centro levam ~80, os da borda ~40; o jogador colado na explosão não toma dano.

## ETAPA 4 — Lampião (fogo lento)
- Ficha **"Lampião"** (raridade a definir → use Épico por enquanto ⚙️, **1 mão**, V = soco com a esquerda): projétil (bola de fogo) 25 m/s, gravidade 0,2, dano 25 + **Queimar** (Etapa 1), cadência 0,8/s, pente 6, recarga 1,6 s, custo 15, essência/acerto 2, eficaz 30 / meia-vida 25, FOV 62, sem especial.
- Visual provisório da bola de fogo: esfera low-poly laranja emissiva com partículas.
**Teste:** acertar aplica Queimar; o tiro é lento e dá para ver a bola voando.

## ETAPA 5 — Teste automático
`dev/validate_tiros_especiais`: Queimar (dano, renovação, sem empilhar), perfuração (3 alvos, perda de dano, para na parede), explosão (queda até a borda, máx. 1 por inimigo, sem dano no jogador), Lampião aplica Queimar. Placar.

## Checklist
- [ ] Status Queimar (3/s por 4 s, renova, sem Essência)
- [ ] Perfuração com perda de 25% por inimigo; Rifle de Pregos
- [ ] Explosão com queda até a borda, sem dano no jogador; Lança-Rojão com confete
- [ ] Lampião com Queimar
- [ ] Validador com placar · Nada além disso foi alterado
