# PROMPT ZIVA — Estilingue de Forquilha + armas mais para a direita

## Contexto
1. O **Estilingue de Forquilha** ganhou modelo e animações próprios no chat de modelagem (pasta `res://Blender/armas/estilingue/`). Ele substitui a arma de teste "Estilingue" (que usava o visual do revólver). É de **duas mãos**: a esquerda segura a forquilha, a direita puxa o elástico.
2. Hoje todas as armas aparecem **no meio da tela**. O Gustavo quer as armas **mais para a direita do corpo** (como na maioria dos FPS: embaixo à direita).

- **Não mude o que não está pedido.**
- **Faça uma etapa por vez e teste.**
- Comente o código em português. Valores que eu escolhi: ⚙️.

---

## ETAPA 0 — Conferir o estilingue (relatório curto)
Leia o `estilingue.glb` e o `bracos.glb` e me diga:
- nó raiz do estilingue e **em que osso ele deve ser preso** (`Arma_R` ou outro);
- lista das ações `Estilingue_*` com **duração** (s) e nº de quadros;
- ossos especiais (ex.: `Bolsa`, `Pedra`, `Cano`).

Se o Gustavo colar os **dados do chat de modelagem**, use-os. Se não, use estes padrões e me avise: pedra **sai no início** do `_Atirar`; **coronhada** com impacto em **0,2 s**; pedra nova entra no **fim** do `_Cooldown`; pente enche no **fim** do `_Recarregar`.
Pode seguir para a Etapa 1 sem esperar, se não houver dúvida.

## ETAPA 1 — Montar o estilingue
- Instancie o `estilingue.glb` no encaixe indicado (transform zerado), como as outras armas; prefixo de animação `Estilingue`.
- Crie o `ItemData` **"Estilingue de Forquilha"** usando o **mesmo `WeaponData`** do estilingue de teste (valores atuais), com:
  - `usa_duas_maos = true` (V = `Estilingue_Coronhada`, golpe com a forquilha, mesma regra das outras: dano do soco × 1,5, +12 de essência);
  - `cena_visual` = estilingue, `prefixo_anim = "Estilingue"`, `usa_animacao_tiro = true`.
- Remova o item de teste "Teste — Estilingue" (e o `WeaponData` de teste se ficar órfão). **Mantenha** a "Pistola rápida" de teste.
- Material: o mesmo toon fosco com contorno das outras armas (use a textura do glb se vier assada).

**Teste:** o estilingue aparece na mão com as duas mãos; V dá o golpe com a forquilha.

## ETAPA 2 — Puxar controlado pela carga
- Enquanto o jogador **segura** o botão (carga de `carga_minima` até 1,0), a ação `Estilingue_Puxar` fica **parada** no tempo `carga_normalizada × duração` nos **dois** players (braços e arma) — com `seek` e velocidade 0, não tocando normalmente.
  - `carga_normalizada` vai de 0 (botão acabou de ser apertado) até 1 (carga cheia em `carga_max_s`).
- Ao **soltar**: toca `Estilingue_Atirar` (blend 0) e a pedra (projétil) sai no momento indicado (Etapa 0).
- Cancelar a carga (R, V, F, troca de arma) volta para `Estilingue_Pose` sem atirar (regras de interação que já existem).
- Depois do tiro: `Estilingue_Cooldown` (pedra nova na bolsa) e volta para a pose.
- Recarga: `Estilingue_Recarregar`; pente enche no momento indicado.

**Teste:** segurar o botão estica o elástico aos poucos (meio segundo = meio puxado); soltar atira; soltar na hora atira fraco e perto; carga cheia vai longe.

## ETAPA 3 — Armas mais para a direita (todas)
- Crie um nó-pivô **acima** do pivô de recuo das armas (o recuo continua funcionando por cima), por exemplo `PosicaoArma`, entre `HandModels` e `HandsVisual`.
- Novos campos no `WeaponData`:
  ```gdscript
  @export var offset_posicao := Vector3(0.0, 0.0, 0.0)   # deslocamento da arma na tela (x = direita, y = cima, z = frente)
  @export var offset_rotacao_graus := Vector3(0.0, 0.0, 0.0)  # leve giro para o cano apontar para a mira
  ```
- Ao sacar cada arma, aplique o offset dela no `PosicaoArma` (com uma transição suave de ~0,15 s ⚙️ ao trocar de arma).
- Ponto de partida ⚙️ (ajuste com captura de tela): armas de **duas mãos** `offset_posicao = (0.12, -0.04, 0.0)` e `offset_rotacao_graus = (0, -3, 0)` (gira o cano um pouco para o centro); **revólver** `(0.06, -0.02, 0.0)` e `(0, -2, 0)`.
- O rastro e o projétil continuam saindo do osso `Cano` e indo para o **ponto da mira** (não mexer nessa conta).
- Confira com captura, para cada arma, que:
  - a arma fica **embaixo à direita**, como num FPS comum;
  - a **mão esquerda escondida** do revólver continua fora da tela (o soco esquerdo depende disso);
  - nada fica cortado de um jeito feio na borda da tela.
- Ao **mirar** (botão direito), aproxime a arma do centro: interpole o offset até ⚙️ 40% do valor (a arma "vem" para o meio ao mirar).

**Teste:** com cada arma, a arma está à direita; mirando ela vem para mais perto do centro; o rastro continua terminando no alvo; o soco esquerdo do revólver não mostra a mão antes da hora.

## ETAPA 4 — Máquina caça-níquel
- Adicione o **Estilingue de Forquilha** (Comum) ao pool da máquina de armas.

---

## Checklist final
- [ ] Relatório do estilingue (encaixe, ações, ossos)
- [ ] Estilingue de Forquilha na mão, duas mãos, V = golpe com a forquilha
- [ ] "Teste — Estilingue" removido; Pistola rápida de teste mantida
- [ ] `Estilingue_Puxar` controlado pela carga nos dois players; soltar atira no momento certo
- [ ] `PosicaoArma` + `offset_posicao`/`offset_rotacao_graus` por arma; armas embaixo à direita; mais ao centro ao mirar
- [ ] Mão esquerda escondida do revólver continua fora da tela; rastro ainda termina no alvo
- [ ] Estilingue na máquina
- [ ] Nada além disso foi alterado
