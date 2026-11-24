# Tomate Boss

- **Status:** 🟡 modelo + animações ✅ · progressão ✅ · luta: proposta · sons ⏳ · entrada ⏳
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

## Luta — proposta v1 (para aprovar)
Primeiro boss: **ensina** a ler avisos e a aproveitar a janela de dano. Usa só as animações que já existem.
| Ataque | Animações | Como funciona | Aviso |
|---|---|---|---|
| **Pulo esmagador** | `Jump_Start/Air/Land` | pula na direção do jogador e cai fazendo uma **onda de choque** (anel que se expande no chão) | círculo vermelho no chão onde vai cair (~1,2 s) |
| **Mordida em investida** | `Attack_Open/Hold/Close` | abre a boca (Pac-Man) e **avança** em linha reta mordendo; se bater numa árvore/pedra, **fica atordoado** | faixa vermelha no chão na direção da investida |
| **Cuspe de sementes** | `Attack_Open/Hold/Close` | cospe um leque de sementes lentas | boca abre e brilha antes |
| **Janela de dano** | `Stun_Start/Loop/End` | depois de **3 pulos** seguidos (ou ao bater na investida) ele cai cansado de pernas abertas por ~3 s, fica verde-claro e leva **dano ×2** | — |
| **Fase 2** (< 50% de vida) | — | mais rápido; a cada pulo nascem 2 tomates comuns | mensagem curta + pulso vermelho |

- Entrada de boss: título **"Tomate Gigante"**, subtítulo sugerido **"O Rei da Horta"**, barra **vermelho-tomate** `#E5484D`.
- Morte: `Death_Start` → explosão em pedaços (`tomato_boss_explosion.glb`, já existe) → drops da F4.
- Sons: pedido ao chat de modelagem (sons sintetizados) depois da luta aprovada.

## Ideias
- 
