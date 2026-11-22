# Sistema de corpo a corpo — proposta (para aprovar)

> Status: ✅ aprovado com ajuste · Prompt: [PROMPT_ZIVA_CORPO_A_CORPO](../../prompts/armas/PROMPT_ZIVA_CORPO_A_CORPO.md)
>
> **Ajuste do Gustavo:** **sem preparo** ("isso não é Dark Souls"). O clique já é o ataque; depois vem a pausa/recuperação, que é a janela do combo. O Martelo só "espera" se o jogador **escolher** segurar para carregar.
> Perguntas 1–5 assumidas com as propostas do Claude (V = soco/pancada com o cabo; botão direito sem função por enquanto; Martelo carregável; máx. 3 alvos contam essência; especiais depois).

## Como um golpe funciona
Botão esquerdo = golpe. Cada golpe tem **2 fases** (sem preparo):
1. **Ativo** — começa **no clique**: a janela em que o golpe acerta (arco à frente da câmera).
2. **Recuperação** — volta; um novo clique aqui **continua o combo**.

- **Combo:** clicar de novo dentro da janela emenda o próximo golpe; o **último golpe do combo** dá dano extra. Parou de clicar → o combo zera.
- **Área:** acerta os inimigos dentro de um **arco** (ângulo) e **alcance** à frente, até um número máximo de alvos.
- **Sem pente e sem recarga.** R não faz nada.
- **Essência:** cada inimigo acertado dá a "Essência por acerto" da arma (no máximo 3 inimigos contam por golpe).
- **Sensação de impacto:** micro-pausa de ~0,05 s no acerto + tremida curta de câmera + lascas/achatar/tranco que já existem.
- **Nível (Fundir):** o mesmo bônus de dano das outras armas.

## As três armas (valores iniciais ⚙️)
| Campo | Cutelo Desgastado | Facão de Mato | Martelo da Vovó |
|---|---|---|---|
| Estilo | rápido | médio | pesado |
| Mãos | 1 | 1 | 2 |
| Dano por golpe | 14 | 24 | 55 |
| Golpes no combo / bônus do último | 3 / ×1,5 | 2 / ×1,3 | 1 / — |
| Ativo · recuperação/janela de combo (s) | **0,12 · 0,35** (ajuste 1) | **0,24 · 0,70** (ajuste 1) | **0,48 · 2,80** (ajuste 1) |
| Acerta em | metade final do ativo (`inicio_acerto` 0,5) | idem | idem |
| Alcance (m) / arco (°) | 1,6 / 70 | 2,2 / 100 | 2,4 / 60 |
| Máx. de alvos | 2 | 3 | 4 |
| Andar enquanto golpeia | normal | ×0,8 | ×0,5 |
| Essência por acerto | 8 | 12 | 20 |
| Carregável | não | não | **sim**: segurar até 1 s; carga cheia = dano ×2 + **onda de choque** (raio 3 m) + **empurra** 2 m |
| Movimento do golpe | corte curto horizontal | corte diagonal largo | pancada de cima para baixo |

## Visual provisório (para testar antes de modelar)
- Um bloco simples na mão (no lugar da arma), com o **golpe feito por código**: o pivô da arma gira para trás no preparo, varre rápido no ativo e volta na recuperação, no formato de cada arma (horizontal, diagonal, de cima para baixo).
- Assim os **tempos** são testados jogando. Os tempos aprovados vão para o chat de modelagem, que faz as animações batendo exatamente com eles.

## Perguntas
1. **V (golpe rápido)** com arma corpo a corpo: Cutelo e Facão (1 mão) = soco com a esquerda; Martelo (2 mãos) = pancada com o cabo. Ou o V não faz nada nas armas corpo a corpo?
2. **Botão direito** com arma corpo a corpo: não faz nada por enquanto (no futuro pode virar **bloquear**)?
3. **Martelo carregável** com onda de choque e empurrão: aprova? (Seria o único corpo a corpo que empurra.)
4. **Máximo de 3 inimigos contando essência por golpe**: ok? (Evita encher a barra demais batendo num grupo.)
5. Algum especial (F) já para alguma das três, ou fica para depois?

## Teste 1 (Gustavo)
- Cutelo rápido demais → usa o tempo do Facão. Facão → dobro. Martelo → quádruplo. O golpe começa no clique e acerta na metade final da varrida.

## Teste 2 (Gustavo)
- O combo **não pode cortar** a animação: o clique durante o golpe fica guardado e o próximo golpe sai quando ele termina; depois há uma janela de combo de 0,3 s.
- **Preparo opcional por arma** (`tempo_preparo_s`): o Martelo tem 0,4 s (levantar); Cutelo e Facão não têm. No Martelo, segurar depois do preparo = carregar levantado.

## Ideias futuras
- **Bloquear** no botão direito (Gustavo gostou; pensar depois como usar).
