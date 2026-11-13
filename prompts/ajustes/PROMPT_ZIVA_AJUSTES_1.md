# PROMPT ZIVA — Ajustes 1: fim do plantio, Barraca de Venda, Fundir/Desmanchar na bigorna, santuário fixo

## Contexto
A limpeza anterior foi concluída. Agora vamos fazer 4 ajustes de design.
- **Não mude o que não está pedido.**
- **Faça uma etapa por vez e teste** antes de seguir.
- O **revólver** tem que continuar funcionando igual (sacar, atirar, recarregar, dano).
- Comente o código em português.
- Valores que eu escolhi estão em `@export` e podem ser ajustados.

## Arquivos que provavelmente serão tocados
| Arquivo | Para quê |
|---|---|
| `scripts/player/player.gd` | tirar ação de plantar e cavar sementes |
| `farming_plot.gd`, `seed_spawner.gd`, `buried_seed.gd` | sistema de plantio (sai) |
| `resources/items/seeds/` | sementes normais e base (saem); **sementes de chefe ficam** |
| `inventory_component.gd` | tirar `grant_weapon_bonus`; guardar nível das armas |
| `shop_stall.*`, `shop_ui.*`, `island_generator.gd`, `crafting_recipes.gd` | Vendinha → Barraca de Venda construível |
| UI da bigorna (`structure_ui.open_anvil`) | abas Fundir e Desmanchar |
| `SHRINE_DEFS` / script do santuário | santuário não some |

---

## ETAPA 1 — Remover o sistema de plantio
O jogador não planta mais nada. Os inimigos continuam nascendo pelo spawn natural (`npc_spawner`), hordas noturnas, monumentos e santuários.
- Remova a ação de plantar do jogador (`_do_plant`, `_plant_on_ground` e o que só servia a elas) e os textos de plantio do HUD.
- Remova o `seed_spawner` (item de semente aleatória que nasce no chão) e as sementes enterradas (`buried_seed`, cavar com mão nua).
- Remova o `farming_plot` se ele só servir ao plantio.
- Apague as **sementes normais** (`*_t1`) e as **sementes base** ("Semente de X").
- **Mantenha** as sementes de chefe (`boss_seed_*`): ainda são a oferenda dos santuários até o rework.
- Se encontrar algo **fora do plantio** que dependa desses scripts (ex.: spawn de inimigos), **pare e me avise** antes de remover.

**Teste:** o jogo roda uma noite inteira sem erro; inimigos continuam aparecendo (dia, noite, monumento); F3 não lista sementes normais/base; não existe mais semente no chão.

## ETAPA 2 — Vendinha vira "Barraca de Venda" construível
- A Vendinha **não nasce mais no mapa**: tire a geração dela do `island_generator`.
- Crie o item construível **"Barraca de Venda"** usando a cena/UI atual da Vendinha, construída do mesmo jeito que a Bancada/Bigorna.
- Receita na **Bancada**: `@export` com padrão **20 Madeira + 10 Pedra**.
- A UI continua com "Vender 1", "Vender Tudo" e "Vender todos os drops".
- **Tire da Barraca o desmanche de armas** (ele vai para a bigorna na Etapa 3).

**Teste:** construir a barraca, vender um drop e receber R$; o mundo novo não tem Vendinha espalhada.

## ETAPA 3 — Bigorna: Fundir e Desmanchar (substitui o bônus de repetida)
**Remova o `grant_weapon_bonus` por completo** (armas e ferramentas). Pegar uma arma repetida agora só soma +1 na quantidade dela no inventário, sem bônus.

Na UI da bigorna, adicione duas abas: **Fundir** e **Desmanchar**.

### Fundir
- Só aparece para armas com **quantidade ≥ 2**.
- Consome **1 cópia** e sobe o **nível da arma** em +1. Nível de 0 a **5** (máximo).
- O nível é **por tipo de arma** (ex.: "revólver nível 3"). Guarde num dicionário no `inventory_component` (`nivel_arma[item_id]`).
- Cada nível melhora **um pouco** os status base, com melhoria **decrescente**:
  ```gdscript
  # Melhoria de cada nível (somada). Nível 5 = +26% no total, não 5x.
  @export var melhoria_por_nivel: Array[float] = [0.08, 0.06, 0.05, 0.04, 0.03]

  func multiplicador_arma(item_id: StringName) -> float:
      var n: int = nivel_arma.get(item_id, 0)
      var total := 1.0
      for i in n:
          total += melhoria_por_nivel[i]
      return total
  ```
- Hoje aplique esse multiplicador **no dano** (`enemy_damage`) onde o bônus antigo era aplicado (revólver e tiro genérico). Quando o sistema de armas novo existir, outros status entram também.
- Mostre o nível no nome da arma (ex.: "Revólver do Coveiro +3") na UI da bigorna e no inventário.
- No nível 5, o botão Fundir fica desativado ("Nível máximo").

### Desmanchar
- Consome **1 cópia** da arma e dá **sucata** pela tabela que a Vendinha usava (2–30 por raridade).
- Se for a **última cópia**, peça confirmação ("Você vai perder esta arma e o nível dela").
- Ao desmanchar a última cópia, o nível daquela arma volta a 0.

**Teste:** pegar 3 revólveres pela máquina → fundir 2 vezes → nível +2, dano 1,14x; desmanchar a última → pede confirmação, recebe sucata, revólver some. Soco e ferramentas não ganham mais bônus por repetida.

## ETAPA 4 — Santuário não some
- Depois que o boss é invocado, o santuário **continua no mapa** e pode ser usado de novo (mesma oferenda de hoje).
- Não deixe invocar de novo enquanto o boss daquele santuário estiver vivo.
- Marque com `# TEMP: rework total dos santuários`. **Não mude** exigências, recompensas nem posições.

**Teste:** invocar o Tomate Gigante, matar, voltar ao santuário e invocar de novo; tentar invocar com o boss vivo → bloqueado.

---

## Checklist final
- [ ] Plantio removido (ação, sementes normais/base, semente no chão, enterradas); inimigos continuam nascendo
- [ ] Sementes de chefe mantidas
- [ ] Vendinha não nasce no mapa; Barraca de Venda construível (20 Madeira + 10 Pedra) vende normalmente
- [ ] `grant_weapon_bonus` removido
- [ ] Bigorna com Fundir (até nível 5, melhoria decrescente) e Desmanchar (com confirmação na última cópia)
- [ ] Santuário fica no mapa e reinvoca; bloqueado com boss vivo
- [ ] Revólver funciona igual a antes
- [ ] Nada além disso foi alterado
