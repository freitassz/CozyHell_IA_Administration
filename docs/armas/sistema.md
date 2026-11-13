# Sistema de armas — regras gerais

> ⚠️ **Rascunho.** Boa parte veio da planilha antiga e vai ser revista. O que vale está em [loop.md](../jogo/loop.md) e [decisoes.md](../jogo/decisoes.md).

## Nichos (12)
- **Corpo a corpo (5):** Rápida, Equilibrada, Pesada ("espadão"), Lança, Giro / Área.
- **À distância (7):** Shotgun, Rifle automático, Pistola / revólver, Sniper, Explosivo, Contínuo, Arremesso / Armadilha.

## Essência do Sonho ✅ (substitui "stamina de arma" e "energia")
- Barra única das armas: **recarregar** e **especial / tiro forte** gastam dela.
- Enche com dano de tiro, soco/corpo a corpo (muito mais) e regeneração natural.

## (rascunho antigo) Energia
- Munição infinita; armas com pente recarregam gastando energia da barra.
- Valores de partida (a testar, em `@export`): barra 100; 0,5 de energia por ponto de dano.
- Custo de recarga por nicho: pistola/arremesso 10 · sniper 15 · shotgun 20 · rifle 25 · explosivo 35.
- A definir: perde energia ao levar dano? Corpo a corpo enche mais?

## (rascunho antigo, em revisão) Calor (superaquecimento)
- Campos: `superaquece` (Sim/Não), tempo até superaquecer, resfriamento.
- Quem superaquece **não tem pente nem recarga**. Hoje: Mangueira, Lança-Chamas, Liquidificador.

## Status (4)
| Status | Efeito |
|---|---|
| Queimar | dano no tempo; derrete o gelo |
| Atordoar | interrompe |
| Eletrizar | — |
| Lentidão | acumula até 5x (−20% cada); no máximo congela ~3 s e descongela |

As armas **aplicam** e **exploram** status — é assim que "conversam".

## Campos do `WeaponData` (nomes para o código)
`dano`, `alcance_m`, `tempo_preparo_s`, `tempo_ativo_s`, `tempo_recuperacao_s`, `golpes_combo`, `bonus_ultimo_golpe`, `area`, `angulo_graus`, `knockback_m`, `atordoamento_s`, `perfura_alvos`, `movimento_ao_atacar`, `tempo_saque_s`, `dano_projetil`, `projeteis_por_tiro`, `cadencia_tps`, `pente`, `recarga_s`, `custo_energia_recarga`, `superaquece`, `tempo_superaquecer_s`, `resfriamento_s`, `alcance_eficaz_m`, `tipo_tiro`, `velocidade_projetil_ms`, `dispersao_graus`, `queda_dano_50_m`, `raio_explosao_m`, `tempo_carga_s`, `aplica_status`, `explora_status`, `especial_nome`, `especial_efeito`, `especial_cooldown_s`, `especial_custo_stamina`.

A coluna **DPS (calc.)** é só para comparar; não vai para o código.

## Casos especiais
- Contínuos: Cadência = ticks de dano por segundo.
- Arremesso: Recarga = tempo para pegar de volta.
- Relógio de Cuco: Pente = nº de bicadas; Recarga = tempo até poder pôr outro.

## Animação na mão (padrão do R08)
- Arma é GLB separado com rig próprio, presa no osso `Arma_R` (`BoneAttachment3D`, transform zerado).
- Ações com mesmo nome e duração nos dois GLB: `<Arma>_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar`.
- Velocidades: `vel_tiro = 0.40 * cadencia_tps` · `vel_recarga = 2.0 / recarga_s` · `vel_sacar = 0.40 / tempo_saque_s` · `vel_guardar = 0.30 / (tempo_saque_s * 0.75)`.
