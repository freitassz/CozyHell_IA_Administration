# F2 — Protótipo do tiro (proposta para aprovação)

> Status: 🟡 aguardando aprovação do Gustavo. Depois vira `prompts/armas/PROMPT_ZIVA_PROTOTIPO_TIRO.md`.

## Objetivo
Descobrir se **atirar é divertido** com a Essência do Sonho **antes** de gastar com modelos, animações e sons.
No fim, o Gustavo joga e responde ao "Teste de diversão" (no fim deste documento).

## Dentro do escopo
1. Ficha de dados de arma (`WeaponData`)
2. Armas como **cópias** (nível por cópia + fusão por soma — ajuste C07)
3. Barra de **Essência do Sonho**
4. **Recarga** gastando essência
5. **Tiro forte** gastando essência
6. **3 armas de teste** (sem arte nova)
7. **Feedback de acerto** básico

## Fora do escopo (fica para depois)
Armas corpo a corpo · status (Queimar, Atordoar…) · superaquecimento (C06) · especial único por arma · modelos/animações novos · sons novos · máquina por boss · rede/multiplayer (mas o código segue as regras de multiplayer).

---

## 1. Ficha de dados (`WeaponData`)
Um `Resource` por arma. Nada de número fixo no código: o tiro lê a ficha.

| Campo | O que é |
|---|---|
| `nome`, `raridade` | |
| `tipo_tiro` | Instantâneo (hitscan) ou Projétil |
| `dano` | por projétil |
| `projeteis_por_tiro` | 1 = normal; >1 = escopeta |
| `dispersao_graus` | abertura do tiro |
| `cadencia_tps` | tiros por segundo |
| `pente` | balas por recarga |
| `recarga_s` | tempo de recarga |
| `custo_essencia_recarga` | quanto a recarga gasta |
| `alcance_m` e `queda_dano_50_m` | distância máxima e onde o dano cai à metade |
| `tempo_saque_s` | tempo para sacar |
| `knockback_m` | empurrão no inimigo |
| `forte_custo`, `forte_mult_dano`, `forte_perfura`, `forte_cooldown_s` | tiro forte |
| `cena_visual` | qual modelo usa (no protótipo, todas usam o revólver) |

## 2. Armas como cópias (ajuste C07)
- Arma **não empilha** mais: cada cópia ocupa um slot e tem o **seu** nível e o **seu** pente.
- Toda arma nasce **nível 1**. Na bigorna, **fundir soma os níveis** (nv3 + nv2 = nv5); máximo 5, excesso se perde (com aviso).
- Melhoria por nível (sobre o dano): nv2 +8% · nv3 +14% · nv4 +19% · nv5 +23%. ⚙️
- Desmanchar continua por cópia.
- O save passa a guardar nível e balas de cada cópia (save antigo é convertido sem quebrar).

## 3. Essência do Sonho
| Item | Valor inicial ⚙️ |
|---|---|
| Máximo | 100 (começa cheia) |
| Ganho por dano de **tiro** | +0,3 por ponto de dano |
| Ganho por dano de **soco** | +1,5 por ponto de dano (5x o tiro) |
| Regeneração natural | +2 por segundo (0 → 100 em 50 s) |
| Perde ao levar dano? | não (0) |

- HUD: barra lilás/roxo-claro abaixo da vida, com a marca do custo de recarga da arma na mão.
- Nome "Essência do Sonho" continua provisório (P11).

## 4. Recarga
- Munição é **infinita**, mas recarregar **gasta essência** (`custo_essencia_recarga`).
- Sem essência suficiente: **não recarrega** → clique seco, barra pisca vermelho, aviso "Sem essência". A regeneração natural garante que o jogador nunca fica travado para sempre.
- Trocar de arma **não enche o pente**; cada cópia lembra quantas balas tem.

## 5. Tiro forte
- Um botão próprio (proposta: **botão direito do mouse**; se ele já for usado para mirar, **tecla Q**).
- Gasta essência, **não gasta bala do pente**.
- Padrão para todas as armas no protótipo: **dano ×3, atravessa 3 inimigos, empurrão forte**, cooldown 1,5 s, custo 35.
- Visual: o mesmo clarão do tiro, maior e colorido (lilás). Especial **único por arma** vem depois.

## 6. Armas de teste (todas com o modelo do revólver, só pelo F3)
| Arma | Dano | Proj. | Cadência | Pente | Recarga | Custo recarga | Alcance |
|---|---|---|---|---|---|---|---|
| Revólver do Coveiro | valor atual | 1 | atual | 6 | atual | 10 | atual |
| Teste — Pistola rápida | 20 | 1 | 4/s | 10 | 1,2 s | 10 | 50 m |
| Teste — Escopeta | 8 | 6 (8°) | 1,2/s | 2 | 1,8 s | 20 | 20 m |
| Teste — Sniper | 90 | 1 | 0,7/s | 4 | 2,2 s | 15 | 120 m |

Valores de partida: a Etapa 0 traz a vida real dos inimigos e eu ajusto antes de implementar.

## 7. Feedback de acerto
- Marcador de acerto na mira (branco; **vermelho no abate**).
- Inimigo pisca branco por 0,08 s ao levar dano.
- Som de acerto (reaproveitar um som existente).
- Números de dano: **não** no protótipo (decidir depois).

---

## Etapas do prompt
| # | Etapa | Teste |
|---|---|---|
| 0 | **Relatório:** como o revólver atira e recarrega hoje, munição, teclas, HUD, `ArmaFps`, inventário, vida dos inimigos | — (Ziva para e espera) |
| 1 | `WeaponData` e revólver migrado para ele (sem mudar comportamento) | revólver igual a antes |
| 2 | Armas como cópias + fusão por soma + save convertido | 2 revólveres com níveis diferentes; nv3+nv2=nv5 |
| 3 | Barra de Essência (ganhos + regeneração + HUD) | atirar/socar enche; parado regenera |
| 4 | Recarga gastando essência | sem essência não recarrega; com essência sim |
| 5 | Tiro forte | dano ×3, atravessa, gasta 35, cooldown |
| 6 | 3 armas de teste no F3 | cada uma com sensação diferente |
| 7 | Feedback de acerto | marcador, piscar, som |

## Teste de diversão (o Gustavo responde depois de jogar)
1. Atirar é gostoso? O que falta (som, impacto, inimigo reagindo)?
2. A essência fez você **pensar** (recarregar × tiro forte) ou só atrapalhou?
3. Ficou sem essência alguma vez? Foi tenso (bom) ou frustrante (ruim)?
4. Socar para encher a barra fez sentido ou ninguém faria isso?
5. As 3 armas de teste pareceram armas **diferentes**?
6. Qual valor mudaria primeiro?
