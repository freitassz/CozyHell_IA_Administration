# PROMPT ZIVA — Pimenta Ardente: Ajuste 1 (escudo, brasas, onda baixa, fogo no personagem)

## Contexto
Testando a Pimenta Ardente, o Gustavo pediu 4 ajustes. Modo rápido: tudo de uma vez, validador cobrindo cada item. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.

## 1. Só leva dano atordoado (escudo)
- **Fora do atordoado, o boss tem uma barreira de fogo** (esfera/casca translúcida laranja em volta, facetada, fosca) que **bloqueia todo dano**: tiros, golpes, soco, coronhada, explosões, Queimar, tudo. Ao ser acertada: **pisca** forte no ponto do impacto + som "plink" (use o som de tiro fraco, mais agudo) e o marcador de acerto fica **cinza**. Nada de dano, Essência ou hitstop no boss.
- A barreira **quebra** quando a bola rebatida o acerta (estilhaços laranja, sem cubos) e o boss fica atordoado (janela de dano, como já está: ⚙️ 4 s; fase 2: 3 s). Ao acordar, a barreira **se refaz** (anima de ⚙️ 0,5 s).
- A bola rebatida **atravessa** a barreira (é o que a quebra). O anel de fogo deixa de ter um escudo próprio: a barreira já cobre isso.
- Como só dá para bater na janela, **reajuste a vida**: ⚙️ 1200 (e o dano ×2 no atordoado continua). Me diga quantos ciclos (bolas rebatidas) leva para matar com o revólver.
- Sinais: `barreira_bloqueou(pos)`, `barreira_quebrou`, `barreira_refeita`.

## 2. Chuva de brasas mais forte
- **Área maior:** raio de cada brasa ⚙️ 1,5 → **2,6 m** × `escala` (o círculo de aviso no chão cresce junto).
- **Mais rápidas:** o aviso no chão continua com **1,2 s** (continua escapável), mas a **queda** das brasas depois do aviso passa a ⚙️ **0,45 s** (hoje é mais lenta). Dano e Queimar iguais.
- Quantidade (6; 9 na fase 2) e dano iguais.

## 3. Onda de fogo baixa (dá para pular)
- Reduza a **altura da onda** de ⚙️ 1,0 m para **0,35 m**. A colisão da onda deve acertar **só quem está com os pés abaixo de 0,35 m** (jogador no chão). Meça a altura do pulo do jogador e garanta que a onda fique em **no máximo 40% dela**.
- O visual da onda também fica com essa altura (facetado, baixo), para o jogador **ver** que dá para pular. Largura, velocidade, 20 de dano e Queimar iguais.

## 4. Fogo no personagem sem tampar a tela
- Quando o jogador está queimando (**Queimar**, vale para a Pimenta e para qualquer outra fonte), a tela **não pode ser coberta por chamas**.
- Novo efeito: só uma **moldura fina de chamas nas bordas da tela** (⚙️ no máximo 12% da largura/altura de cada lado), pouco opaca (⚙️ 0,35) e **centro 100% limpo**, mais um ícone de chama pequeno perto da vida.
- O dano de Queimar e a duração continuam iguais.
- Se existir um efeito antigo de fogo em tela cheia, remova-o.

## Teste
Atualize `dev/validate_pimenta`: barreira bloqueia tiro/golpe/soco/Queimar; rebater quebra e abre a janela; barreira refaz; brasas com raio 2,6 e queda de 0,45 s; onda de 0,35 m não acerta quem pula; moldura de fogo sem cobrir o centro. Placar.

## Checklist
- [ ] Barreira (bloqueia tudo, quebra ao rebater, refaz) · [ ] Vida reajustada + ciclos para matar
- [ ] Brasas: raio 2,6 e queda 0,45 s (aviso 1,2 s) · [ ] Onda 0,35 m, dá para pular
- [ ] Fogo só nas bordas · [ ] Validador · Nada além disso foi alterado
