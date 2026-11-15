# PROMPT ZIVA — F2.3: Limite do recuo na rajada + testes (fecha a fase do tiro)

## Contexto
Testando a Pistola rápida com `automatica = true`, segurando o botão o recuo **não tem limite**: a arma sobe até sair da tela e a **mão esquerda escondida aparece** (o `HandsVisual` gira inteiro, levando o braço esquerdo para dentro da tela).
Este é o último ajuste da fase do tiro.
- **Não mude o que não está pedido.** Rastro e lascas ficam como estão.
- **Faça uma etapa por vez e teste.**
- Comente o código em português.

---

## ETAPA 1 — Limite do recuo acumulado
Novos campos no `WeaponData`:
```gdscript
@export var recuo_arma_max_graus := 26.0     # ⚙️ giro máximo da arma somando a rajada
@export var recuo_arma_max_m := 0.10         # ⚙️ recuo máximo para trás
@export var recuo_camera_max_graus := 8.0    # ⚙️ subida máxima da câmera somando a rajada
```
- O recuo acumulado **satura suavemente** perto do máximo (cada tiro soma menos quanto mais perto do limite), em vez de parar seco. Exemplo:
  ```gdscript
  # Soma com saturação: quanto mais perto do máximo, menos o tiro empurra.
  atual = atual + pico * (1.0 - atual / maximo)
  atual = min(atual, maximo)
  ```
- Vale para arma e câmera, multiplicado por `forca_recuo` e × 0,6 mirando (como hoje).
- Valores por arma ⚙️:

| Arma | arma máx ° | arma máx m | câmera máx ° |
|---|---|---|---|
| Pistola rápida | 22 | 0,06 | 6 |
| Revólver | 26 | 0,08 | 8 |
| Escopeta | 26 | 0,12 | 8 |
| Sniper | 30 | 0,12 | 10 |
| Estilingue | 8 | 0,10 | 3 |

- **A mão esquerda nunca pode aparecer.** No máximo de cada arma, confira com captura que o braço esquerdo continua fora da tela. Se aparecer, baixe o máximo daquela arma (e me diga o valor) — **não** mova a pose escondida.

**Teste:** Pistola com `automatica = true`, segurar até esvaziar 3 pentes seguidos (recarregando) → a arma sobe até ~22° e para ali, a mira sobe até ~6°, a mão esquerda nunca aparece; ao soltar, tudo volta.

## ETAPA 2 — Arrumar os testes antigos
- `dev/validate_f21.gd` e `dev/validate_tiro.gd`: atualize os valores esperados para os da F2.2 (recuo novo, `knockback_m = 0`, empurrões dos especiais) e corrija a espera do teste "Coice recua o jogador" para aguardar **pela trava** (e não 0,3 s fixo), para passar em máquina lenta.
- Apague `dev/validate_soco_esquerdo.gd` (versão antiga sem uso).
- Rode todos os validadores da fase do tiro (`validate_tiro`, `validate_f21`, `validate_f22`, soco esquerdo) e me diga o placar de cada um.

---

## Checklist final
- [ ] `recuo_arma_max_graus`, `recuo_arma_max_m`, `recuo_camera_max_graus` com saturação suave
- [ ] Mão esquerda nunca aparece no recuo máximo (com captura)
- [ ] Validadores antigos atualizados; `validate_soco_esquerdo.gd` apagado
- [ ] Placar de todos os validadores da fase
- [ ] Nada além disso foi alterado
