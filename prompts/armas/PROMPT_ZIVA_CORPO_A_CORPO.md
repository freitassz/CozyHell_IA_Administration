# PROMPT ZIVA — Sistema de corpo a corpo (Cutelo, Facão, Martelo da Vovó) com visual provisório

## Contexto
Vamos criar as **armas corpo a corpo**. Elas ainda **não têm modelo**: o objetivo é testar o **funcionamento e os tempos** jogando, com um **bloco** no lugar da arma e o golpe feito por código. Depois de aprovados, os tempos vão para o chat de modelagem.
Regra principal do Gustavo: **sem preparo/espera antes do golpe** — o clique **já é o ataque**. Depois do golpe vem a pausa (recuperação), que é a janela do combo.
- **Não mude o que não está pedido.** Armas de tiro, essência, recuo e posição das armas continuam iguais.
- **Faça uma etapa por vez e teste.**
- Comente o código em português. Tudo no `WeaponData` ou `@export`. Valores que eu escolhi: ⚙️.
- Regras de multiplayer: estado do golpe/combo é **de cada jogador**.

---

## ETAPA 1 — Dados do golpe no `WeaponData`
Novos campos (atualize também `docs`/ficha de campos se existir no projeto):
```gdscript
@export_enum("Tiro", "Golpe") var tipo_ataque := 0
@export var golpes_combo := 1
@export var bonus_ultimo_golpe := 1.0      # multiplica o dano do último golpe do combo
@export var tempo_ativo_s := 0.1           # começa NO CLIQUE: janela em que o golpe acerta
@export var tempo_recuperacao_s := 0.2     # pausa depois do golpe = janela para continuar o combo
@export var alcance_golpe_m := 2.0
@export var arco_golpe_graus := 90.0
@export var max_alvos := 3
@export var mult_andar_golpe := 1.0        # velocidade de andar durante o golpe
@export var max_alvos_essencia := 3        # quantos inimigos por golpe contam para a Essência
@export var hitstop_s := 0.05              # micro-pausa no acerto
@export var tremida_camera := 0.3          # força da tremida curta no acerto
@export_enum("Horizontal", "Diagonal", "Vertical") var forma_golpe := 0  # para o visual provisório
```
O dano usa `dano`, o nível (Fundir) e `essencia_por_acerto` que já existem. Armas de golpe não têm pente nem recarga.

## ETAPA 2 — O golpe
- **Botão esquerdo** com arma `Golpe`: o golpe começa **no mesmo frame do clique** (sem preparo).
- Durante `tempo_ativo_s`: acerta os inimigos dentro do **alcance** e do **arco** à frente da câmera, até `max_alvos` (cada inimigo só uma vez por golpe).
- Depois vem `tempo_recuperacao_s`. Um clique **durante a recuperação** (ou guardado nos últimos ⚙️ 0,1 s do ativo) emenda o **próximo golpe do combo**. O **último golpe** do combo multiplica o dano por `bonus_ultimo_golpe`. Sem clique até o fim da recuperação → combo volta ao 1º golpe.
- **Essência:** cada inimigo acertado dá `essencia_por_acerto`, contando no máximo `max_alvos_essencia` inimigos por golpe.
- **Impacto:** no acerto, micro-pausa (`hitstop_s`) — use uma pausa **local** (animação/visual do jogador e do inimigo acertado), **não** `Engine.time_scale` (regra de multiplayer) — + tremida curta de câmera + as lascas/achatar/tranco que já existem.
- Andar durante o golpe: × `mult_andar_golpe`.
- R não faz nada. F: sem especial por enquanto (comportamento de "arma sem especial").
- **V (golpe rápido):** arma de 1 mão → soco com a esquerda (como já existe); arma de 2 mãos → pancada com o cabo (use a mesma lógica da coronhada, sem animação nova por enquanto).
- **Botão direito:** não faz nada com arma de golpe (no futuro pode virar bloquear).

**Teste:** clicar acerta **na hora**; clicar no ritmo faz o combo inteiro; parar e clicar de novo recomeça o combo.

## ETAPA 3 — Visual provisório
- No lugar do modelo, um **bloco** (`BoxMesh` alongado, cor madeira/metal claro, fosco) preso no `Arma_R`, com a mão direita em pose de segurar (pose de guarda existente).
- O golpe é feito **por código** no pivô da arma (acima do recuo), conforme `forma_golpe`:
  - **Horizontal:** varre da direita para a esquerda durante o ativo e volta na recuperação.
  - **Diagonal:** de cima-direita para baixo-esquerda, mais largo.
  - **Vertical:** de cima para baixo (pancada).
- O movimento rápido acontece **dentro do `tempo_ativo_s`** (o bloco já começa a varrer no clique); a volta acontece na recuperação. Golpes seguidos do combo alternam o lado (vai e volta) ⚙️.

**Teste:** dá para "sentir" a diferença entre as três só pelo bloco.

## ETAPA 4 — Martelo carregável
- O Martelo é de golpe **carregável** (`carregavel = true`, `carga_max_s = 1.0` ⚙️).
- **Toque rápido** (soltar em menos de ⚙️ 0,15 s): pancada normal, golpeia ao soltar.
- **Segurar:** carrega (bloco sobe e treme um pouco, arco de carga na mira que já existe; andar × `carga_mult_andar`). **Soltar golpeia.**
- **Carga cheia:** dano × 2 + **onda de choque** no chão (raio ⚙️ 3 m, dano = 50% do golpe) + **empurra** os inimigos ⚙️ 2 m.
- Regras de cancelamento iguais às da carga das armas de tiro (V, F, troca de arma cancelam).

**Teste:** toque = pancada rápida; segurar 1 s = pancada forte com onda e empurrão.

## ETAPA 5 — As três armas (só no F3, fora da máquina por enquanto)
| Campo | Cutelo Desgastado | Facão de Mato | Martelo da Vovó |
|---|---|---|---|
| Raridade | Comum | Raro | Épico |
| `usa_duas_maos` | não | não | **sim** |
| `dano` | 14 | 24 | 55 |
| `golpes_combo` / `bonus_ultimo_golpe` | 3 / 1,5 | 2 / 1,3 | 1 / 1,0 |
| `tempo_ativo_s` / `tempo_recuperacao_s` | 0,08 / 0,18 | 0,12 / 0,35 | 0,12 / 0,70 |
| `alcance_golpe_m` / `arco_golpe_graus` | 1,6 / 70 | 2,2 / 100 | 2,4 / 60 |
| `max_alvos` | 2 | 3 | 4 |
| `mult_andar_golpe` | 1,0 | 0,8 | 0,5 |
| `essencia_por_acerto` | 8 | 12 | 20 |
| `forma_golpe` | Horizontal | Diagonal | Vertical |
| `carregavel` | não | não | **sim** |
| `hitstop_s` / `tremida_camera` | 0,03 / 0,2 | 0,05 / 0,3 | 0,08 / 0,6 |

## ETAPA 6 — Teste automático
Crie `dev/validate_corpo_a_corpo` cobrindo: golpe no frame do clique, combo completo e reinício, máx. de alvos, essência com limite, Martelo (toque × carga cheia com onda/empurrão), V e botão direito. Me diga o placar.

---

## Checklist final
- [ ] Campos de golpe no `WeaponData`
- [ ] Golpe começa **no clique** (sem preparo); recuperação = janela do combo
- [ ] Arco/alcance/máx. de alvos; essência com limite de 3 inimigos por golpe
- [ ] Hitstop local (sem `Engine.time_scale`) + tremida + lascas
- [ ] Bloco provisório com golpe por código (horizontal, diagonal, vertical)
- [ ] Martelo: toque = pancada; segurar = carga; cheia = ×2 + onda + empurra
- [ ] V e botão direito como combinado; R/F sem efeito
- [ ] 3 armas no F3; validador com placar
- [ ] Nada além disso foi alterado
