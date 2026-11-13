# Resposta ao relatório da Etapa 0 (limpeza)

Obrigado pelo relatório. Commit "antes da limpeza" feito. Pode seguir **etapa por etapa**, com estas decisões:

1. **Commit:** feito.
2. **Revólver na máquina:** sim. Adicione `revolver.tres` ao pool de **comuns** e troque `ARMAS_PADRAO` para conter só o revólver. A máquina tem que continuar funcionando (repetido → sucata).
3. **Crescimento sem enxada:** sim, tudo a 1x. Remova também `is_tilled` / `tilled_speed_factor` e a cena do canteiro da enxada. **Mantenha** o grupo `tillable_ground`. A mão nua continua cavando sementes enterradas.
4. **Tiers:** mantenha o `ProgressionManager` (ele vai ser reaproveitado depois para as fases de inimigos). Remova só o conteúdo `_t2`/`_t3`, faça `seed_spawner` e `night_spawn_manager` usarem **sempre o tier 1**, e **não mexa** ainda no `match variation_tier` dos inimigos.
5. **Sementes de chefe** (`boss_seed_2a`, `boss_seed_2b`): **não apague**. Só mude o `variation_tier` delas para 1.
6. **Testes em `dev/`:** teste que só testa coisa removida (loja, mesa, preview da mesa) → apague. Teste misto → remova só as referências aos itens que saíram (no `cacaniquel_test.gd`, troque `potato_cannon` pelo `revolver`).
7. **Adubo Turbo:** sai (era do sistema de crescimento). **Vendinha (sucata):** antes de remover, me diga **o que ela faz**. Se for onde o jogador vende itens por dinheiro, ela **fica**.

## Cuidados extras
- **Dano da pistola** (`player.gd` 49–51 e 1196–1199): antes de remover, confira se o **revólver usa esse mesmo código de tiro/dano**. Se usar, **não remova**; só me avise.
- **`slot_machine.gd`** (linhas 38–44): me diga o que é esse script (máquina antiga? máquina de acessórios?). Tire as armas placeholder da lista, mas **não remova o script**.
- **`give_starting_tools`:** tire só enxada e pá; o resto do kit inicial fica.
- **`island_generator.gd`:** remova a geração das Mesas de Contrato (`weapon_trader_count`), sem mexer no resto da geração.
- Encontros de monumento (`resources/encounters/`): verifique e troque qualquer `_t2`/`_t3` por `_t1`.
