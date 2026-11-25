# PROMPT ZIVA — Boss 2: Uva-morcego (luta)

## Contexto
Segundo boss (santuário na Floresta; ritual, drops e a liberação da **fase 2 do pesadelo** já funcionam pela F4). Ele **voa**: testa a mira para cima e dá uma janela de dano quando **erra o mergulho e cai no chão**.
Cena: `enemies/grape_boss/grape_boss.tscn`. Animações: `Idle`, `Wander`, `Attack_Start/Attack_Loop`, `Dash_Start/Dash_Loop`, `Dash_Hit` (→ Wander), `Dash_Miss` (→ `Fallen_Loop`), `Fallen_Recover`. Projétil: `grape_projectile.glb`. Olho com shape key `EyeRed` (osso `CTRL_Rage`). Voo por código.
- Modo **rápido**: pode fazer todas as etapas de uma vez, mas o validador cobre cada uma. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim. Variável **`escala`**.
- Multiplayer: mira o **jogador mais próximo**; nada de `Engine.time_scale`. Padrões de aviso iguais aos do Tomate (`Decal` vermelho, ≥ 1,2 s, branco nos últimos 0,1 s, áreas redondas).

## ETAPA 0 — Relatório curto
Como o `grape_boss` funciona hoje (vida, ataques, voo, uso das animações, morte).

## Luta
1. **Voo:** circula (`Wander`) a ⚙️ 8–12 m de altura em volta do jogador, mudando de lado.
2. **Chuva de uvas** (`Attack_Start` → `Attack_Loop`): solta ⚙️ 5 uvas (`grape_projectile`) que caem em arco perto do jogador. Cada ponto de queda tem um **círculo vermelho** 1,2 s antes. Cada uva estoura em suco: ⚙️ 10 de dano, raio 1,5 m × `escala`.
3. **Mergulho** (`Dash_Start` → `Dash_Loop`): o **olho fica vermelho** (`EyeRed`) e aparece uma **faixa** no chão na direção do mergulho por 1,2 s; ele mergulha em linha reta até onde o jogador estava.
   - Acertou o jogador → `Dash_Hit`, ⚙️ 20 de dano + empurrão, volta a voar.
   - **Errou** → bate no chão → `Dash_Miss` → **`Fallen_Loop` ⚙️ 3 s: caído no chão, leva dano × 2** (hora de bater, até corpo a corpo alcança) → `Fallen_Recover` → volta a voar.
4. Escolha ⚙️: chuva (peso 1), mergulho (peso 2); se passar 3 ataques sem ele cair, o próximo é mergulho.
5. **Fase 2 (< 50% de vida), sem texto:** olho vermelho fixo (`CTRL_Rage` cheio) + um grito curto + pulso roxo. Faz **2 mergulhos seguidos** (o 2º com aviso de 1,2 s também) e a chuva passa a 8 uvas; ⚙️ 20% mais rápido.
6. **Entrada:** título **"Uva-morcego"**, subtítulo ⚙️ **"A Sombra do Parreiral"**; barra roxo-uva `#7B3FA0` com marcador em 50%; invulnerável na entrada. Vida ⚙️ 2200.
7. **Morte:** animação de morte existente (ou `Dash_Miss` + some em suco) → drops da F4 (liberação da fase 2 já existe).

## Sinais (para os sons)
`chuva_inicio` · `uva_estourou(posicao)` · `mergulho_aviso` · `mergulho_inicio` · `mergulho_acertou` · `mergulho_errou` · `caiu` · `levantou` · `fase2` · `morreu`

## Teste automático
`dev/validate_uva`: avisos ≥ 1,2 s, chuva com círculos, mergulho que erra → caído 3 s com dano ×2, acerto → volta a voar, garantia do mergulho, fase 2 sem texto com 2 mergulhos, drops. Placar.

## Checklist
- [ ] Voo · [ ] Chuva de uvas com avisos · [ ] Mergulho com olho vermelho e faixa; erro = caído ×2
- [ ] Fase 2 sem texto · [ ] Entrada/barra/morte · [ ] Sinais · [ ] Validador · Nada além disso foi alterado
