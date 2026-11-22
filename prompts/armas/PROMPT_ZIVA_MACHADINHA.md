# PROMPT ZIVA — Machadinha Enferrujada (arremesso teleguiado que volta) com visual provisório

## Contexto
Nova arma **Rara**, de **uma mão**: uma machadinha que é **arremessada**, faz uma **curva da direita para a esquerda** como bumerangue, **sempre chega no alvo**, **acerta todos no caminho** e **volta para a mão**. É a arma "fácil": nunca erra, mas só funciona **de perto**.
Ainda **sem modelo**: use um **bloco** (visual provisório) para testar o funcionamento.
- **Não mude o que não está pedido.**
- **Faça uma etapa por vez e teste.**
- Comente o código em português. Tudo em `WeaponData`/`@export`. Valores que eu escolhi: ⚙️.
- Multiplayer: o arremesso pertence ao jogador que jogou; a volta segue **esse** jogador.

---

## ETAPA 1 — Dados
Novo `tipo_tiro`: **"Arremesso teleguiado"**. Campos novos no `WeaponData`:
```gdscript
@export var cone_alvo_graus := 35.0         # cone à frente da mira para escolher o alvo
@export var velocidade_arremesso_ms := 30.0
@export var curva_lateral_m := 2.5          # quanto a trajetória abre para os lados (ida pela direita, volta pela esquerda)
@export var raio_acerto_caminho_m := 0.8    # largura do "caminho" que acerta inimigos
```
Ficha da arma **"Machadinha Enferrujada"** (Rara, só no F3 por enquanto):
| Campo | Valor ⚙️ |
|---|---|
| `dano` | 30 por acerto |
| `alcance_eficaz_m` | 12 (alcance do alvo) |
| `cone_alvo_graus` | 35 |
| `velocidade_arremesso_ms` | 30 |
| `pente` | 1 (a machadinha) |
| `custo_essencia_recarga` | **0** (a "recarga" é ela voltar) |
| `essencia_por_acerto` | 4 |
| `usa_duas_maos` | não (V = soco com a esquerda) |
| `fov_mira` | 62 (botão direito mira normalmente) |
| `especial` | nenhum (por enquanto) |

## ETAPA 2 — Escolha do alvo + marcador
- Enquanto a machadinha está na mão, o jogo procura o inimigo **mais próximo da mira** dentro de `alcance_eficaz_m` e do `cone_alvo_graus` (com linha de visão).
- Mostre um **marcador** pequeno em cima desse inimigo (ex.: um losango branco ⚙️, sempre virado para a câmera). Sem alvo válido → sem marcador.
- Mirar (botão direito) funciona como nas outras armas (zoom leve, mesmo cálculo do alvo).

**Teste:** passar a mira perto de inimigos a menos de 12 m mostra o marcador no mais próximo da mira; longe ou fora do cone, some.

## ETAPA 3 — Arremesso, ida e volta
- **Clique** com alvo: a machadinha sai da mão e vai até o alvo numa **curva pela direita** (curva Bezier: mão → ponto de controle à direita, deslocado por `curva_lateral_m` → alvo). Ela é **teleguiada**: o fim da curva acompanha o alvo se ele se mexer, então **sempre chega**.
- Ao chegar, **volta** pela **esquerda** (curva alvo → ponto à esquerda → mão), seguindo o jogador se ele andar.
- **Sem alvo:** voa **reto para a frente** até `alcance_eficaz_m` e volta pelo mesmo jeito (pode errar).
- Enquanto voa: a mão fica vazia (esconda o bloco da mão), **não** dá para arremessar de novo. Ao voltar, ela reaparece na mão (isso é a "recarga", sem gastar Essência).
- Trocar de arma com ela no ar: ela volta sozinha e reaparece quando a arma for sacada de novo.

## ETAPA 4 — Acertos
- Acerta **todo inimigo** que o caminho tocar (`raio_acerto_caminho_m`), na ida e na volta.
- **Cada inimigo só leva 1 acerto por arremesso** (se foi acertado na ida, a volta passa por ele sem dano).
- O alvo sempre leva o acerto (ao chegar, se ainda não levou).
- Cada acerto: `dano` (com nível/Fundir), `essencia_por_acerto`, lascas, piscar, achatar/tranco, micro-pausa e tremida curta (o que já existe).

**Teste:** 3 inimigos em fila no caminho levam 1 acerto cada; o alvo leva exatamente 1 acerto mesmo que a volta passe por ele.

## ETAPA 5 — Visual provisório
- Bloco pequeno achatado (cabo + lâmina, cor ferrugem clara, fosco) na mão direita, pose de segurar existente.
- No ar: o bloco **gira** rápido em torno do próprio eixo.
- Rastro leve opcional (o mesmo sistema de rastro, curto, cor ferrugem `#E07B39`).

## ETAPA 6 — Teste automático
`dev/validate_machadinha`: alvo/marcador (alcance, cone), sempre acerta o alvo em movimento, 1 acerto por inimigo por arremesso, sem alvo voa reto e volta, sem arremesso duplo, sem custo de Essência. Me diga o placar.

---

## Checklist final
- [ ] Tipo "Arremesso teleguiado" + campos novos; ficha da Machadinha no F3
- [ ] Marcador em cima do alvo (mais próximo da mira, 12 m, cone 35°)
- [ ] Ida pela direita até o alvo (teleguiada), volta pela esquerda até a mão
- [ ] Acerta todos no caminho, **1 acerto por inimigo por arremesso**
- [ ] "Recarga" = voltar, sem Essência; mão vazia enquanto voa
- [ ] Botão direito mira; V = soco com a esquerda
- [ ] Bloco provisório girando; validador com placar
- [ ] Nada além disso foi alterado
