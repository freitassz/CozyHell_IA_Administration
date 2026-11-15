# PROMPT ZIVA — F2.2: Ajustes finais do tiro

## Contexto
A F2.1 foi testada jogando. Estes são os ajustes finais para fechar a fase do tiro.
- **Não mude o que não está pedido.**
- **Faça uma etapa por vez e teste.**
- Comente o código em português.
- Valores que eu escolhi: ⚙️ (tudo em `WeaponData` ou `@export`).
- **Tudo tem que conversar:** veja a tabela de interações no fim e respeite-a.

---

## ETAPA 1 — Remover os efeitos antigos dos inimigos
- No `vegetable_enemy` (e em qualquer outro inimigo com o mesmo código), remova o **knockback próprio de 0,3 m** e o **"suco" antigo** ao levar dano.
- O empurrão real passa a vir **só** do `knockback_m` da arma/especial. O efeito visual vem **só** do `ImpactoFx`.

**Teste:** tiro normal de pistola não empurra o inimigo; o especial do revólver (que tem knockback) empurra.

## ETAPA 2 — Impacto: só Lascas, maiores; bosses só piscam
- Fica **só o modo Lascas**. Remova o modo Gotas e a tecla F6 de teste (mantenha a opção "Nenhum" só no código, desligada).
- Lascas maiores: `@export var escala_lasca := 1.6` ⚙️ (multiplica o tamanho atual).
- **Achatar** e **tranco visual** valem **só para inimigos comuns**. **Bosses** recebem **apenas a piscada branca** (sem achatar, sem tranco). Use o grupo/classe de boss já existente (`boss.gd` ou grupo `bosses`).
- As lascas continuam em bosses também (na `cor_impacto` deles).

**Teste:** Tomate comum achata e tranca; boss Tomate Gigante (ovo do F3) só pisca; lascas visíveis a ~15 m.

## ETAPA 3 — Força do recuo por arma
O recuo visual da pistola e da sniper ficou parecido. Cada arma precisa ter um recuo próprio e bem diferente.
- Novo campo: `@export var forca_recuo := 1.0` — multiplica **todos** os valores de recuo daquela arma (câmera e arma). É o "botão rápido" para ajustar.
- Confira se existe algum **limite (clamp)** ou suavização que deixa as armas parecidas; se existir, remova ou mova para o `WeaponData`.
- Novos valores ⚙️:

| Arma | forca_recuo | câmera ° | arma ° | arma m | volta s | Sensação |
|---|---|---|---|---|---|---|
| Pistola rápida | 1,0 | 1,2 | **14** | 0,03 | 0,22 | a arma **pula para cima** a cada tiro, câmera pouco |
| Revólver | 1,0 | 3,0 | **20** | 0,05 | 0,32 | mais forte que a pistola |
| Escopeta | 1,0 | 4,0 | 18 | 0,09 | 0,35 | coice para trás |
| Sniper | 1,0 | 6,0 | **24** | 0,10 | 0,50 | o tiro mais forte |
| Estilingue | 1,0 | 0,5 | 3 | 0,05 | 0,20 | quase nada (escala com a carga, Etapa 6) |

**Teste:** atirando uma vez com cada arma, dá para **ver** a diferença: pistola sobe rápido e leve, revólver mais, sniper muito.

## ETAPA 4 — Rastro visível de dia
De manhã, o rastro se perde no ambiente claro.
- Novos campos: `@export var largura_rastro := 0.06` ⚙️ e `@export var comprimento_rastro := 2.0` ⚙️.
- Rastro com **duas camadas**: núcleo quase branco + borda na `cor_rastro`, mais saturada. Cor padrão nova ⚙️: `Color(1.0, 0.55, 0.15)` (laranja forte, contrasta com céu e grama clara).
- Sem depender só de emissão (de dia o brilho não aparece): material **unshaded**.

**Teste:** às 9h, atirando para o céu e para a grama, o rastro é fácil de ver.

## ETAPA 5 — Tiro automático
- Novo campo: `@export var automatica := false`.
  - `true`: **segurar o botão** atira na `cadencia_tps` até soltar, acabar o pente ou a essência negar a recarga.
  - `false`: um clique = um tiro (como hoje).
- Nas automáticas, o recuo **soma** enquanto o botão está segurado (a mira sobe aos poucos) e volta quando solta.
- Armas atuais: todas `false`. Para testar, ligue `automatica` na Pistola rápida pelo Inspector (e volte para `false`).

**Teste:** com `automatica = true`, segurar esvazia o pente e a mira sobe; com `false`, segurar dá um tiro só.

## ETAPA 6 — Armas carregáveis (estilingue, arco)
Segurar puxa mais e o tiro vai mais longe.
- Novos campos:
  ```gdscript
  @export var carregavel := false
  @export var carga_max_s := 1.0            # tempo para carga total
  @export var carga_minima := 0.3           # força se soltar na hora (30%)
  @export var carga_mult_velocidade := Vector2(0.5, 1.6)  # projétil: x = carga mínima, y = carga cheia
  @export var carga_mult_dano := Vector2(0.6, 1.3)
  @export var carga_mult_andar := 0.7       # velocidade de andar enquanto puxa
  ```
- Segurar o botão de tiro **puxa**; soltar **atira**. Força = de `carga_minima` até 1,0 em `carga_max_s`.
- Velocidade do projétil e dano são interpolados pela força (vai mais longe com a carga cheia).
- Enquanto puxa: arma recua um pouco para trás no pivô (proporcional à carga) e aparece um **arco de carga** pequeno ao redor da mira.
- Recuo do disparo escala com a força.
- **Estilingue de teste:** `carregavel = true`, `carga_max_s = 1.0` ⚙️, `velocidade_projetil_ms = 35` (passa a ir de 17,5 a 56 m/s).

**Teste:** estilingue solto na hora cai perto; carregado até o fim vai bem mais longe e dá mais dano.

---

## Como tudo conversa (regras)
| Situação | Regra |
|---|---|
| `carregavel` e `automatica` juntos | `carregavel` vence; `automatica` é ignorada |
| Carregando + **mirar** (botão direito) | pode; zoom e dispersão de mira valem normalmente |
| Carregando + **recarregar** (R) | cancela a carga sem atirar e recarrega |
| Carregando + **soco rápido** (V) | cancela a carga e soca |
| Carregando + **especial** (F) | cancela a carga e usa o especial |
| Carregando + **trocar de arma** | cancela a carga |
| Pente vazio ao tentar puxar/atirar | tenta recarregar (regra da essência) |
| Automática + pente acaba | para de atirar e tenta recarregar se o botão continuar segurado |
| Recuo | soma em rajada (automática); escala com a força (carregável); × 0,6 mirando; × `forca_recuo` |
| Essência por acerto | igual para todos os modos (`essencia_por_acerto` por projétil que acerta) |
| Queda de dano | sempre pela distância (percorrida, no projétil) |

## Checklist final
- [ ] Knockback 0,3 m e suco antigos removidos dos inimigos
- [ ] Só Lascas (escala 1,6); sem Gotas e sem F6
- [ ] Achatar e tranco só em inimigos comuns; bosses só piscam
- [ ] `forca_recuo` + novos valores; pistola, revólver e sniper visivelmente diferentes
- [ ] Rastro maior, duas camadas, unshaded, laranja; visível de dia
- [ ] `automatica` funcionando (segurar atira e soma recuo)
- [ ] `carregavel` funcionando no estilingue (puxar, arco de carga, mais longe e mais dano)
- [ ] Regras de interação da tabela respeitadas
- [ ] Nada além disso foi alterado
