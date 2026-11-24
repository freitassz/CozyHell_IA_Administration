# Tomate Boss

- **Status:** ✅ luta no jogo (52/52 no validador; falta jogar na ilha com o jogador real) · 🟡 sons ([pedido](../../prompts/blender/PROMPT_BLENDER_SONS_TOMATE.md) → [Ziva](../../prompts/bosses/PROMPT_ZIVA_SONS_TOMATE.md))
- **Tamanho:** ~5 m · **Etapa do roteiro:** 2

## Modelo
6 gomos, cálice de 6 folhas, olhos brancos, pálpebras bravas, boca Pac-Man de casca dupla, 4 pernas (largas em cima, finas e arredondadas embaixo).

## Animações
- `Idle`
- `Jump_Start` / `Jump_Air` / `Jump_Land`
- `Attack_Open` / `Attack_Hold` (loop) / `Attack_Close`
- `Stun_Start` / `Stun_Loop` / `Stun_End` (cai de pernas abertas, olhos fechados; o verde-claro é feito no jogo)
- `Death_Start` → explosão `tomato_boss_explosion.glb`

## Progressão ✅ (F4)
Santuário na Planície · 1ª oferenda: drop do Tomate + drop da Cenoura + drop do Pimentão · dropa Ficha Rara + Casca do Tomate · libera **Raro** na máquina.

## Luta — ✅ aprovada (prompt: [PROMPT_ZIVA_TOMATE_GIGANTE](../../prompts/bosses/PROMPT_ZIVA_TOMATE_GIGANTE.md))
Primeiro boss: **ensina** a ler avisos e a aproveitar a janela de dano. Usa só as animações que já existem.
| Ataque | Animações | Como funciona | Aviso |
|---|---|---|---|
| **Pulo esmagador** | `Jump_Start/Air/Land` | pula na direção do jogador e cai fazendo uma **onda de choque** (anel que se expande no chão) | círculo vermelho no chão onde vai cair (~1,2 s) |
| **Mordida em investida** | `Attack_Open/Hold/Close` | abre a boca (Pac-Man) e **avança** em linha reta mordendo; se bater numa árvore/pedra, **fica atordoado** | faixa vermelha no chão na direção da investida |
| **Linguada** ✅ (já existe no jogo; substitui o cuspe) | — | a língua pode **prender** o jogador (comportamento atual; o Ziva descreve) | boca abre/brilha antes |
| **Janela de dano** | `Stun_Start/Loop/End` | depois de **3 pulos** seguidos (ou ao bater na investida) ele cai cansado de pernas abertas por ~3 s, fica verde-claro e leva **dano ×2** | — |
| **Fase 2** (< 50% de vida) | — | mais rápido; **a cada 2 pulos** nascem 2 tomates comuns | **sem texto**: só animação/efeito do boss |

- Entrada de boss: título **"Tomate Gigante"**, subtítulo sugerido **"O Rei da Horta"**, barra **vermelho-tomate** `#E5484D`.
- Morte: `Death_Start` → explosão em pedaços (`tomato_boss_explosion.glb`, já existe) → drops da F4.
- Sons: pedido ao chat de modelagem (sons sintetizados) depois da luta aprovada.

## Ideias
- 

## Como ficou (Ziva, nov/2026)
- Vida 1500; atordoado dano ×2 por 3 s, verde-claro. Pesos: pulos 2, investida 1, linguada 1; garantia depois de 2 ataques.
- Pulo: 3 pulos, círculo 1,2 s, onda em anel até 6 m (20 de dano; quem está pulando não leva).
- Investida: faixa 1,2 s, 14 m/s até 18 m, 25 + empurrão; bate em obstáculo = atordoado; sem chão à frente, para.
- **Linguada:** estica numa direção travada; acerta = 15; **se bater no cenário, a língua fica presa** e o boss fica parado e vulnerável 3 s (é o "pode ficar preso"). Aviso: boca abrindo e brilhando 0,8 s (menor que a regra de 1,2 s — conferir jogando).
- Fase 2 sem texto: Stun curto + pulso vermelho + tremida + barra piscando; 25% mais rápido; 2 tomates a cada 2 pulos (máx. 6). Só troca de fase fora de ataque.
- Entrada "Tomate Gigante / O Rei da Horta"; barra `#E5484D` com marcador em 50%; usa a barra nova (não o `boss_hud` antigo).
- Terreno também na camada visual 19 (para os avisos pintarem só o chão). `debug_mode` desligado.
