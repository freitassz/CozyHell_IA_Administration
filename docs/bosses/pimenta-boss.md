# Pimenta Ardente (PepperBoss2)

- **Tipo:** boss · **Modelo:** `PepperBoss2` (já existe: corpo vermelho de abóbora/pimenta com chifres, cabo verde, olhos e boca de fogo, duas mãos flutuantes) · **Animações atuais:** `IDLE`, `ATTACK_FIREBALL`, `DEFENSE_FIRE`, `HURT`
- **Status:** 🟡 pacote pronto: [pedido de modelagem + sons](../../prompts/blender/PROMPT_BLENDER_PIMENTA_BOSS.md) · [prompt do Ziva](../../prompts/bosses/PROMPT_ZIVA_PIMENTA_BOSS.md)
- **Posição na progressão:** ❓ ainda não está na cadeia dos 5 bosses. Provisório: só pelo **ovo do F3**. Substitui o inimigo "Abóbora" da fase 2 (que não existe mais).

## Ideia do Gustavo
Boss de **etapas rígidas**. Fica **no ar a distância fixa** do jogador (nem mais perto, nem mais longe) e **dá a volta nele**. A cada ciclo faz **2 ataques sorteados** e, no 3º, solta uma **bola de fogo**. O jogador **rebate** a bola (golpe corpo a corpo): ela volta, acerta o boss e ele fica **atordoado** (hora de bater ou atirar). Se o jogador **erra**, ele **continua lançando bolas** até uma ser rebatida.

## Ataques (propostas do Claude, usando as animações do modelo)
| Ataque | Animação | O que faz | Aviso |
|---|---|---|---|
| **Chuva de brasas** | `Brasas` | brasas caem em volta do jogador (1ª em cima dele); Queimar | círculos vermelhos 1,2 s |
| **Anel de fogo** | `DEFENSE_FIRE` | escudo de fogo (invulnerável) e uma **onda de fogo baixa** que se expande: **pular por cima** evita | círculo crescente no chão 1,2 s |
| **Mãos esmagadoras** | `Maos_Enviar` | as **mãos** voam e **esmagam** o chão (2 mãos; 3 na fase 2) | círculos vermelhos 1,2 s |
| **Bola de fogo** (sempre o 3º) | `Lancar_Bola` | bola lenta e grande em direção ao jogador; **rebater** = soco/golpe/coronhada | boca acende + brilho 1,2 s |

- **Rebater:** só **corpo a corpo** (golpe de arma, soco V, coronhada) — tiros atravessam a bola. Bola rebatida volta teleguiada ao boss → **atordoado ~4 s** (desce a ~3 m, olhos apagados, dano ×2).
- **Errou:** a bola acerta o jogador ou o chão e o boss **lança outra** (depois de 4 erros seguidos a bola vem 30% mais lenta — ajuda).
- **Fase 2 (< 50%, sem texto):** mais rápido, brasas 9, 3 mãos, bola +20%, atordoado 3 s.
- Entrada: **"Pimenta Ardente" / "A Brasa do Sonho"**, barra laranja-fogo `#FF6A1F`, vida 2000 (ajustáveis).
