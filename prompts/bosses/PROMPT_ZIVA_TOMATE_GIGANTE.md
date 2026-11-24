# PROMPT ZIVA — Boss 1: Tomate Gigante (luta)

## Contexto
Primeiro boss da progressão (santuário na Planície; ritual, drops e liberação do **Raro** já funcionam pela F4). Ele **ensina** o jogador a ler avisos e a aproveitar a hora de bater.
Cena: `scenes/enemies/tomato_boss.tscn` (modelo e animações prontos: `Idle`, `Jump_Start/Air/Land`, `Attack_Open/Hold/Close`, `Stun_Start/Loop/End`, `Death_Start` + `tomato_boss_explosion.glb`).
- **Não mude o que não está pedido.** Uma etapa por vez, com teste. Comente em português. Tudo em `@export`; ⚙️ = valor escolhido por mim.
- Uma variável **`escala`** no boss: tamanhos de avisos, alcances e ondas multiplicam por ela.
- Multiplayer: mira o **jogador mais próximo**; **nada de `Engine.time_scale`** em código novo.
- Padrões do jogo: avisos no chão com **`Decal`** (`decal_alvo_mergulho.png`, vermelho `Color(1, 0.18, 0.15)`, `cull_mask` só no terreno), piscar acelerando + **branco nos últimos 0,1 s**, aviso de **≥ 1,2 s**, áreas **redondas**, no máximo 1 dano por onda.

## ETAPA 0 — Relatório (siga se não houver bloqueio)
Como o `tomato_boss` funciona hoje: vida, ataques que já existem, **como funciona a linguada** (ela prende o jogador? o que acontece?), uso das animações, entrada de boss/barra, morte e explosão.

## ETAPA 1 — Pulo esmagador
- `Jump_Start` → `Jump_Air` (altura e deslocamento **por código**; a animação não desloca) → `Jump_Land`.
- Cai **onde o jogador estava** ao pular (⚙️ máx. 12 m por pulo × `escala`). Aviso: círculo vermelho no ponto de queda durante ⚙️ 1,2 s.
- Ao cair: **onda de choque** (anel que se expande no chão até ⚙️ 6 m × `escala`, dá ⚙️ 20 de dano a quem estiver no anel no chão; pular por cima evita) + poeira + tremida perto.
- Ele faz **sequências de 3 pulos**. Depois do 3º: **cansa** (Etapa 4).

## ETAPA 2 — Mordida em investida
- `Attack_Open` → avança em linha reta com `Attack_Hold` (⚙️ 14 m/s, até 18 m × `escala`) → `Attack_Close`.
- Aviso: faixa vermelha no chão na direção da investida por ⚙️ 1,2 s.
- Acertar o jogador: ⚙️ 25 de dano + empurrão.
- **Bater numa árvore/pedra/parede:** para e fica **atordoado** (Etapa 4).

## ETAPA 3 — Linguada (no lugar do cuspe de sementes)
- Use a **linguada que já existe** (relatório). Mantenha o comportamento dela (inclusive se ela **prende** o jogador), só garantindo: aviso visível antes (boca abre/brilha ⚙️ 0,8 s), dano ⚙️ 15, e uma forma clara de **se soltar** se ela prender (ex.: apertar V/soco ou ⚙️ 1,5 s no máximo).
- Me descreva no fim como ela ficou.

## ETAPA 4 — Hora de bater (atordoado)
- Depois de **3 pulos seguidos** ou de **bater na investida**: `Stun_Start` → `Stun_Loop` (⚙️ 3 s) → `Stun_End`. Fica **verde-claro** (troca de material por código) e leva **dano × 2**.
- Escolha dos ataques ⚙️: sequência de pulos (peso 2), investida (peso 1), linguada (peso 1); **garantia**: se passar 2 ataques sem atordoar, o próximo é a sequência de pulos.

## ETAPA 5 — Fase 2 (< 50% de vida)
- Fica ⚙️ 25% mais rápido (pulos, investida, tempo entre ataques).
- **A cada 2 pulos**, nascem **2 tomates comuns** perto dele (⚙️ máx. 6 vivos ao mesmo tempo, usam o inimigo Tomate da fase 1).
- **Sem texto na tela** na troca de fase: só uma animação/efeito do boss (ex.: `Stun_Start` curto + pulso vermelho + rugido). Essa regra vale para **todos os bosses**.

## ETAPA 6 — Entrada, barra, morte
- Entrada com `boss_intro.tscn`: título **"Tomate Gigante"**, subtítulo **"O Rei da Horta"**; invulnerável durante a entrada.
- Barra com `boss_barra.tscn`, cor `#E5484D`, marcador de fase em 50%.
- Vida ⚙️ 1500 (ajuste pelo relatório). Morte: `Death_Start` → troca para a explosão em pedaços → drops da F4.

## Sinais (para os sons depois)
`pulo_inicio` · `pulo_aterrissou` · `investida_inicio` · `investida_bateu(obstaculo: bool)` · `linguada_inicio` · `linguada_prendeu` · `atordoado` · `fase2` · `morreu`

## ETAPA 7 — Teste automático
`dev/validate_tomate`: aviso antes de cada ataque (≥ 1,2 s), 3 pulos → atordoado ×2, investida contra pedra → atordoado, fase 2 a 50% com tomates a cada 2 pulos (máx. 6), sem texto na fase 2, drops ao morrer. Placar.

## Checklist
- [ ] Pulo esmagador com aviso e onda · [ ] Investida com aviso; bate e atordoa · [ ] Linguada (descrita) com aviso e saída
- [ ] Atordoado verde ×2 + garantia · [ ] Fase 2 mais rápida, 2 tomates a cada 2 pulos, **sem texto**
- [ ] Entrada/barra/morte · [ ] Sinais · [ ] Validador · Nada além disso foi alterado
