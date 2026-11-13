# Resposta ao relatório da Etapa 0 (fundação)

Relatório excelente. Pode seguir para a **Etapa 1**, uma etapa por vez, com estas decisões:

1. **Dia:** sim, crie o contador `dia` no `DayNightCycle`, somando +1 no `day_started` (amanhecer). Mundo novo começa no **dia 1**. Salve `dia` e `hour`.
2. **ID dos recursos:** sim, ID = **tipo + posição (x, z) arredondada a 0,1 m**. Vale para árvores, pedras, minérios, arbustos, coletáveis de chão, carvão e **monumentos**. Guarde também os parâmetros do gerador que afetam posições junto com a seed no save (para detectar se um save antigo ficou incompatível — se ficar, avise no log em vez de quebrar).
3. **Objetos com RNG global:** de acordo. Salve **tipo + posição** de vacas-melancia vivas, máquinas repostas e totem. Salve também `cowmellon_kills` e `_finished` do `WatermelonBossTrigger`. **Inimigos vivos e itens no chão não são salvos.** Salve o clima (`is_raining`, `_rain_hours_left`, `_days_until_check`).
4. **Totem de Melancia e Uva:** **não mude as regras de progressão** (elas vão ser refeitas depois). Só garanta que **todo boss** (Tomate, Uva, Dragão, Totem e os dos santuários) fique **registrado como derrotado** em `defeated_bosses` ao morrer, para o save. O **Totem é boss secreto e não deve subir o tier**: registre a derrota sem passar pelo `BOSS_STAGE`.
5. **Morte:** sim, troque para os valores do plano (30% do R$, 30% da sucata, 50% dos recursos/drops). Mantenha o resto do fluxo atual (limpar inimigos perto do ponto, espera de 2,5 s, restaurar vida).
6. **Itens:** sim, salve o `resource_path` do `ItemData`. Se ao carregar o caminho não existir mais (item removido ou movido), **pule o item e avise no log**, sem travar o carregamento.

## Pontos extras
- **Cama = ponto de renascer:** ao usar a cama, além de curar, ela passa a definir o **ponto de renascer** do jogador (salvo). Se a cama for destruída, volta ao spawn do mundo. Usar a cama também **salva o jogo** (Etapa 7).
- **Monumentos:** salve só `CLEARED`. Um monumento `ACTIVE` ao salvar volta como `IDLE` ao carregar.
- **Fornalha:** na Etapa 4, confira onde ficam de verdade os slots dela (combustível, entrada, saída) e salve junto com a construção.
- **Santuários:** não precisam de estado salvo agora (são reutilizáveis).
- `_on_respawn_timeout` órfão no `island_generator`: **não mexa**.
