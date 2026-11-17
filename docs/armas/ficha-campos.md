# Ficha de arma (`WeaponData`) — campos atuais

> Referência para atualizar a planilha. Atualize sempre que um campo novo entrar.
> A planilha foi atualizada (nov/2026): abas **Armas v1**, **Corpo a Corpo v1** e **Regras atuais**.

## Identidade
| Campo | O que é |
|---|---|
| `nome`, `raridade` | |
| `cena_visual` | modelo usado |
| `usa_duas_maos` | sim → soco rápido vira **coronhada** (C15) |
| `usa_animacao_tiro` | sim → toca `_Atirar` (só o revólver hoje); não → só recuo procedural |

## Tiro
| Campo | O que é |
|---|---|
| `tipo_tiro` | Instantâneo ou Projétil |
| `automatica` | **sim** = segurar atira; **não** = um clique, um tiro |
| `carregavel` | sim = segurar puxa, soltar atira (estilingue, arco) |
| `dano`, `projeteis_por_tiro`, `dispersao_graus` | |
| `cadencia_tps` | tiros por segundo |
| `pente`, `recarga_s`, `custo_essencia_recarga` | |
| `essencia_por_acerto` | essência devolvida por projétil que acerta |
| `alcance_eficaz_m`, `meia_vida_dano_m`, `dano_minimo` | alcance infinito com queda até o mínimo |
| `tempo_saque_s`, `knockback_m` | |

## Projétil
`velocidade_projetil_ms`, `gravidade_mult`, `tempo_vida_projetil_s`, `cena_projetil`

## Carga (se `carregavel`)
`carga_max_s`, `carga_minima`, `carga_mult_velocidade`, `carga_mult_dano`, `carga_mult_andar`

## Recuo
`forca_recuo` (multiplicador geral), `recuo_camera_graus`, `recuo_lateral_graus`, `recuo_arma_m`, `recuo_arma_graus`, `recuo_subida_s`, `recuo_volta_s`

## Mira
`fov_mira`, `mult_dispersao_mira`

## Visual do tiro
`cor_rastro`, `largura_rastro`, `comprimento_rastro`

## Especial
`especial` (`EspecialArma` ou vazio = sem especial): `nome`, `custo_essencia`, `cooldown_s`, efeito próprio.

## Nível
Por cópia (nv1–nv5, fusão por soma); bônus de dano `[0, 8, 14, 19, 23]%`.
