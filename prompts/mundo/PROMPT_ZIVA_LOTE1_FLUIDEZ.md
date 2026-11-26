# PROMPT ZIVA — Lote 1: fluidez de gameplay (dificuldade de recursos, alcance, economia, boss vai embora, stamina/deslize, sem respawn em construção)

## Contexto
Primeiro playtest do Gustavo gerou ajustes. Este lote tem 6 itens pequenos/médios de **gameplay**. Modo rápido: tudo de uma vez, com **validador**.
- **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim (tudo em `@export`/Resource, num lugar central quando for número de balanceamento). Estado no **save**.

## ETAPA 0 — Relatório curto (siga se não houver bloqueio)
Me diga os números **de hoje**: vida de árvore/pedra/arbusto e dano das ferramentas (mão nua, machado, picareta e as de ferro); preços de compra/venda mais comuns (Barraca de Venda, máquinas, bigorna, Andarilho, Trader); alcance de cada golpe corpo a corpo e do soco/coronhada; como funciona hoje o **deslize** e a **stamina** (existe barra? quanto gasta correr/pular?); como o respawn de recursos escolhe onde nascer.

## 1. Recursos mais difíceis (#7)
- Variável global `mult_vida_recursos := 3.0` ⚙️ (árvore, pedra, arbusto, minérios mantêm a regra do nível de picareta). Dano das ferramentas **inalterado**, então fica mais lento **principalmente à mão** e recompensa fazer machado/picareta.
- Meta de sensação: árvore ≈ **~25 golpes à mão**, ~**10 com machado**, ~**6 com machado de ferro** ⚙️ (ajuste a vida base para isso; me diga os números finais).

## 2. Alcance do corpo a corpo (#11)
- Multiplique o alcance dos golpes por `mult_alcance_golpe := 1.4` ⚙️ (Cutelo, Facão, Martelo, **soco V, coronhada**) e dê **mais tolerância lateral** ao arco/cápsula (⚙️ +0,3 m de raio no acerto). Alcance final (me diga): Cutelo ≈ 2,2 m · Facão ≈ 3,1 m · Martelo ≈ 3,4 m · soco ≈ 2,0 m.
- Acertar o inimigo deve valer quando o **modelo dele** parece alcançável (use o raio do corpo do inimigo no teste de acerto).

## 3. Economia mais difícil (#13)
- Crie `economia.tres` central com: `mult_preco_compra := 2.0` e `mult_preco_venda := 0.6` ⚙️, aplicados em **todas** as fontes (Barraca de Venda, Andarilho, máquinas caça-níquel, bigorna/estações que cobram R$, Trader). Bônus de conjunto de Ouro continua somando por cima da venda.
- Preços/recompensas de monumento e boss em R$: ⚙️ ×0,8.
- Me diga uma tabela "antes → depois" dos principais preços.

## 4. Boss vai embora quando o jogador morre (#15)
- Se o **jogador morre durante a luta** (ou, no futuro, todos os jogadores), o boss **vai embora**: efeito de saída (puf/fogo/suco conforme o boss, 1–2 s), some, **sem drops**, e o **santuário volta a ficar disponível**.
- Para invocar de novo, a oferenda passa a ser a de **reinvocar (3 itens comuns)** — **mesmo que o boss nunca tenha sido derrotado**. A **1ª vitória** continua dando ficha, material e liberações (e a 1ª oferenda com material do boss anterior continua sendo exigida só para a 1ª invocação **bem-sucedida de ponta a ponta**: depois que o boss foi invocado uma vez, as seguintes usam comuns).
- Os itens já colocados no altar são consumidos na invocação (como hoje). Salve o estado "já invocado alguma vez" por boss.

## 5. Stamina visível + pulo no deslize com momentum (#24)
- **Barra de stamina** curta e discreta (sob a Essência), que só aparece quando não está cheia (⚙️ regen 20/s depois de ⚙️ 1 s sem gastar). Correr gasta ⚙️ 8/s; pular ⚙️ 10.
- **Pular durante o deslize mantém o momentum** (velocidade do deslize vira impulso do pulo) e gasta ⚙️ **30 de stamina**. **Sem stamina suficiente:** o pulo sai normal, **sem** momentum. Impedir agachar+pular em loop: depois de um pulo com momentum, **novo deslize** só com stamina ≥ ⚙️ 30 e ⚙️ 0,4 s de intervalo.
- Mantenha as regras atuais do deslize (duração, inclinação) — só acrescente isso.

## 6. Nada renasce perto de construções (#2)
- No renascimento de recursos (3 dias) **e** em qualquer outro spawn de prop/recurso/inimigo-prop: **não nascer** a menos de ⚙️ 3 m de qualquer peça de construção, estação, baú, estrutura/NPC ou santuário. Se o ponto estiver bloqueado, **adie para o dia seguinte** (mantém o ID, sem perder). Vale também para construir **depois** (já existe: peças bloqueiam).

## Teste
`dev/validate_lote1`: vida×3 e golpes necessários, alcance novo e tolerância lateral, `economia.tres` aplicada (compra ×2, venda ×0,6, Ouro soma), boss some quando o jogador morre e santuário aceita 3 comuns, 1ª vitória ainda dá drops/liberação, stamina (gasto, regen, pulo no deslize com e sem stamina, sem loop), recurso não renasce a < 3 m de construção e renasce no dia seguinte. Placar.

## Checklist
- [ ] `mult_vida_recursos` (3,0) · [ ] `mult_alcance_golpe` (1,4) + tolerância · [ ] `economia.tres` central
- [ ] Boss sai quando o jogador morre; reinvocar com comuns · [ ] Stamina visível + pulo no deslize
- [ ] Sem respawn perto de construções · [ ] Números finais reportados · [ ] Validador · Nada além disso foi alterado
