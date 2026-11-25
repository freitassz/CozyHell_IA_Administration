# PROMPT ZIVA — Pimenta Ardente (PepperBoss2): luta com bola de fogo rebatível

## Contexto
Boss de **etapas rígidas**: paira a distância fixa do jogador e o rodeia; ciclo = **2 ataques sorteados + bola de fogo**; o jogador **rebate** a bola (corpo a corpo) → o boss fica **atordoado**. Modelo e animações novos vêm do chat de modelagem; **enquanto não chegarem, use a cena/animações atuais** (`IDLE`, `ATTACK_FIREBALL`, `DEFENSE_FIRE`, `HURT`) e deixe os nomes novos num mapa `@export` (ver "Mapa de animações").
- **Modo rápido:** pode fazer tudo de uma vez; o validador cobre cada etapa. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim. Variável **`escala`**.
- Multiplayer: orbita o **jogador mais próximo**; rebater vale de qualquer jogador; nada de `Engine.time_scale`.
- Avisos no padrão do jogo: `Decal` vermelho no terreno, **≥ 1,2 s**, piscar acelerando, branco nos últimos 0,1 s, áreas redondas, 1 dano por onda. **Sem texto na fase 2.**

## ETAPA 0 — Relatório curto
O projeto já tem `PepperBoss`, `Fireball` e `FireBarrier` antigos: me diga o que existe (cena, scripts, vida) e o que dá para reaproveitar. Diga também onde ficam o golpe corpo a corpo, o soco V e a coronhada (para a Etapa 3).

## ETAPA 1 — Órbita
- Mantém distância horizontal **fixa** ⚙️ 14 m × `escala` do jogador e altura ⚙️ 9 m; **gira em volta** a ⚙️ 20°/s, invertendo o sentido a cada ataque. Se o jogador anda, ele corrige para manter a distância (⚙️ até 8 m/s). Pequeno balanço vertical (⚙️ 0,4 m). Sempre olha para o jogador.

## ETAPA 2 — Ciclo e ataques
Ciclo: **2 ataques** sorteados entre {Brasas, Anel, Mãos} (nunca o mesmo duas vezes seguidas) → **Bola de fogo** → repete. Pausa ⚙️ 0,8 s entre ataques.
- **Brasas:** ⚙️ 6 brasas (9 na fase 2); a 1ª cai **em cima do jogador**, as outras até 5 m dele. Círculo vermelho 1,2 s; cada uma: 10 de dano, raio 1,5 m × `escala`, aplica **Queimar** (já existe).
- **Anel de fogo:** o boss fica invulnerável (escudo) ⚙️ 1,5 s; círculo no chão **sob ele** mostra o alcance (até ⚙️ 24 m × `escala`) por 1,2 s; depois uma **onda de fogo baixa** se expande (⚙️ 14 m/s, altura 1 m): **pular por cima** evita; 20 de dano + Queimar.
- **Mãos:** 2 círculos vermelhos (1 em cima do jogador, 1 a ⚙️ 4 m; 3 na fase 2) por 1,2 s; as mãos (`pimenta_mao` ou blocos provisórios) descem e **esmagam**: 25 de dano, raio 2,5 m; ficam ⚙️ 0,8 s no chão e somem. Mãos do corpo escondidas durante o ataque (`Maos_Enviar`/`Maos_Voltar`).

## ETAPA 3 — Bola de fogo rebatível
- Aviso: boca acende e brilha por 1,2 s (`Lancar_Bola`).
- A bola (raio ⚙️ 0,8 m, brilhante, rastro) voa até onde o jogador estava, a ⚙️ 16 m/s (fase 2: +20%).
- **Rebater:** golpe de **arma corpo a corpo**, **soco V** ou **coronhada** cujo alcance toque a bola (⚙️ até 2,5 m do jogador) → hitstop local + a bola **volta teleguiada** ao boss a ⚙️ 28 m/s. **Tiros atravessam a bola.**
- Bola rebatida acerta o boss → **atordoado**: desce a ⚙️ 3 m de altura, para a órbita, olhos/boca apagam (material), **dano ×2** por ⚙️ 4 s (fase 2: 3 s) → acorda e sobe. Cada bola rebatida dá a Essência de um acerto de soco ⚙️ 12.
- **Errou** (bola acerta jogador = 20 de dano + Queimar, ou chão/obstáculo = explode): o boss **lança outra** na hora (mesmo aviso). Depois de ⚙️ 4 erros seguidos a próxima bola vem 30% mais lenta.
- Atordoado sem ciclo: ao acordar, o ciclo recomeça nos 2 ataques.

## ETAPA 4 — Fase 2, entrada, morte, drops
- **Fase 2 (< 50%, sem texto):** `Fase2` (olhos/boca flamejam) + pulso laranja + tremida; órbita +25%; brasas 9, mãos 3, bola +20%, atordoado 3 s. Só troca fora de ataque.
- **Entrada:** título "Pimenta Ardente", subtítulo "A Brasa do Sonho"; invulnerável durante; barra `#FF6A1F` com marcador em 50%; vida ⚙️ 2000.
- **Morte:** `Morte_Start` → some em fogo → drops provisórios: ⚙️ 3× Molho de Pimenta + dinheiro (fora da cadeia de progressão por enquanto).
- Crie o **Ovo: Pimenta Ardente (Boss)** no F3. Remova o inimigo "Abóbora" da fase 2 (fase 2 = Cebola + Milho, `# TEMP`).

## ETAPA 5 — Sinais e sons (ligar só depois que os arquivos existirem)
Sinais: `brasas_inicio` · `brasa_caiu(pos)` · `anel_aviso` · `anel_inicio` · `maos_aviso` · `maos_esmagaram` · `bola_aviso` · `bola_lancada` · `bola_rebatida` · `bola_errou` · `atordoado` · `acordou` · `fase2` · `morreu`.
Sons em `res://Blender/<pasta do PepperBoss2>/sons/`, `volume_db = 0`, loops com "Detect From WAV", **preso** no boss (`unit_size` 12 / `max_distance` 100) salvo: `brasa_impacto`, `bola_explode`, `maos_esmagar`, `morte` **no lugar** (player criado fora, liberado no `finished`); `fogo_loop` toca enquanto voa; `bola_loop` enquanto a bola voa (preso na bola); `atordoado_loop` até `acordou`. 1 som por evento.

## Mapa de animações (`@export`)
`idle, brasas, anel, maos_enviar, maos_voltar, lancar_bola, hurt, atordoado_start, atordoado_loop, atordoado_end, fase2, morte` → nomes atuais onde existirem (`IDLE`, `DEFENSE_FIRE`, `ATTACK_FIREBALL`, `HURT`); ausentes = pular a animação, manter a lógica.

## ETAPA 6 — Teste
`dev/validate_pimenta`: órbita à distância fixa, ciclo 2+bola, sem repetir ataque, avisos ≥ 1,2 s, rebater (golpe/V/coronhada) atordoa e tiros não, erro → nova bola, dano ×2 atordoado, fase 2 sem texto, drops. Placar.

## Checklist
- [ ] Órbita fixa · [ ] Ciclo 2+bola · [ ] Brasas, Anel, Mãos com avisos · [ ] Bola rebatível → atordoado
- [ ] Erro → nova bola · [ ] Fase 2 sem texto · [ ] Entrada/barra/morte · [ ] Ovo F3 · [ ] Sinais e sons · [ ] Validador · Nada além disso foi alterado
