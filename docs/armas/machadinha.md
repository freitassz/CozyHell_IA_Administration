# Machadinha Enferrujada — proposta da mecânica (para aprovar)

- **Raridade:** Raro · **Mãos:** 1 (V = soco com a esquerda) · **Status:** ✅ design aprovado · 🟡 mecânica ([prompt do Ziva](../../prompts/armas/PROMPT_ZIVA_MACHADINHA.md))
- Ideia do Gustavo: gameplay **mais fácil** que as outras — **sempre acerta**, mas **só de perto**; sai fazendo uma **curva da direita para a esquerda** como bumerangue, **acerta todos no caminho** (o alvo é só o destino) e **volta para a mão**. Enferrujada.

## Como funciona (proposta)
1. **Alvo:** ao clicar, o jogo escolhe o inimigo **mais próximo da mira** dentro do **alcance** (⚙️ 12 m) e de um **cone** à frente (⚙️ 35°).
   - Sem inimigo válido: ela voa **reto para a frente** até o alcance máximo e volta (pode errar).
2. **Ida:** sai da mão pela **direita**, faz uma curva e chega **no alvo** — teleguiada, então **sempre** chega nele mesmo que ele se mexa.
3. **Volta:** sai do alvo pela **esquerda** e volta para a mão (segue o jogador se ele andar).
4. **Acerta todos no caminho**, na ida e na volta, mas **cada inimigo leva só 1 acerto por arremesso** ✅.
5. **"Recarga" = esperar ela voltar.** Enquanto voa, a mão fica vazia e não dá para arremessar de novo. **Sem custo de Essência** (o limite é o alcance curto e o tempo de voo).
6. Velocidade ⚙️ ~30 m/s (ida + volta a 12 m ≈ 0,8 s).
7. Impacto: lascas, piscar, achatar/tranco, micro-pausa e tremida (o que já existe).

## Números iniciais ⚙️ (da planilha)
| Dano por acerto | Alcance | Cone | Velocidade | Essência por acerto | Especial |
|---|---|---|---|---|---|
| 30 | 12 m | 35° | 30 m/s | 4 | depois |

## Ajuda visual (proposta)
- Um **marcador** pequeno aparece em cima do inimigo que **seria o alvo** (antes de arremessar). Mostra que ela "trava" e deixa claro o alcance curto.

## Processo
Funcionamento primeiro com **visual provisório** (bloco girando no ar e na mão) → teste → modelo e animações (arremessar, pegar de volta) no chat de modelagem.

## Decidido
- 1 acerto por inimigo por arremesso · sem custo de Essência · marcador no alvo · botão direito mira normalmente.
