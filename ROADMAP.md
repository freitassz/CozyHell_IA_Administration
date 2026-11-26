# Roteiro de desenvolvimento

> Atualize este arquivo sempre que uma etapa mudar de status.

## 🎯 Fase atual: F4 — Progressão ([proposta](docs/jogo/progressao.md))
Armas V1 prontas (nov/2026). Agora: bosses, santuários, oferendas e máquina por nível.
1. ✅ [Sistema de progressão](prompts/progressao/PROMPT_ZIVA_PROGRESSAO.md) (63/63) — falta ver ao vivo a explosão do ritual e o santuário final subindo
2. ✅ Boss 1 — Tomate Gigante (jogável; sons: [pedido](prompts/blender/PROMPT_BLENDER_SONS_TOMATE.md) → [Ziva](prompts/bosses/PROMPT_ZIVA_SONS_TOMATE.md))
3. 🟡 Boss 2 — Uva-morcego ([luta](prompts/bosses/PROMPT_ZIVA_UVA_MORCEGO.md) · sons: [pedido](prompts/blender/PROMPT_BLENDER_SONS_UVA.md) → [Ziva](prompts/bosses/PROMPT_ZIVA_SONS_UVA.md)) → depois inimigo Abóbora
> Modo rápido: bosses jogáveis primeiro; ajustes de cada um depois (P-08).
4. ❌ Batata-golem **cortada**. Ordem: Tomate → Uva → Dragão → Pimenta → Deus (final). Ajuste da cadeia: [prompt](prompts/progressao/PROMPT_ZIVA_REMOVER_BATATA.md)
5. 🟡 Pimenta Ardente (**boss 4 da cadeia**; [ajuste 2](prompts/bosses/PROMPT_ZIVA_PIMENTA_AJUSTE_2.md)) — pacote: [modelagem+sons](prompts/blender/PROMPT_BLENDER_PIMENTA_BOSS.md) · [Ziva](prompts/bosses/PROMPT_ZIVA_PIMENTA_BOSS.md)
4. ⏳ Dragão (ligar) → Batata-golem (refazer) → Final (criar)

> O projeto virou **hobby** do Gustavo (tempo livre): o ritmo é mais lento, o método é o mesmo.

## Histórico: revisão geral
Ver o que já existe, o que tirar, o que colocar e o que ajustar — antes de seguir com bosses e armas.
- Lista de trabalho: [docs/jogo/revisao.md](docs/jogo/revisao.md)
- Identidade do jogo: [docs/jogo/identidade.md](docs/jogo/identidade.md)

### Plano de ação
| Fase | O quê | Status |
|---|---|---|
| **F1 — Decisões** | ✅ loop, níveis da máquina, ordem dos bosses, reinvocação, Essência do Sonho, morte (Soneca/Pesadelo), construção, multiplayer, minérios → armaduras | ✅ quase |
| **F1.5 — Inventário** | Levantar tudo o que existe e decidir o destino ([inventario.md](docs/jogo/inventario.md)) | ✅ |
| **F1.6 — Limpeza** | Ziva removeu o que foi cortado (catálogo 101 → 76 itens) ([PROMPT_ZIVA_LIMPEZA](prompts/limpeza/PROMPT_ZIVA_LIMPEZA.md)) | ✅ |
| **F1.6b — Ajustes 1** | Fim do plantio, Barraca de Venda, Fundir/Desmanchar, santuário fixo ([PROMPT_ZIVA_AJUSTES_1](prompts/ajustes/PROMPT_ZIVA_AJUSTES_1.md)) | ✅ (falta teste ao vivo) |
| **F1.7 — Fundação** | Salvar/carregar + menu principal + criação de mundo (seed, Soneca/Pesadelo) — [fundacao.md](docs/sistemas/fundacao.md) · [PROMPT](prompts/fundacao/PROMPT_ZIVA_FUNDACAO.md) | ✅ (faltam 3 testes ao vivo) |
| **F2 — Protótipo do tiro** ([proposta](docs/armas/prototipo-tiro.md) · [prompt](prompts/armas/PROMPT_ZIVA_PROTOTIPO_TIRO.md)) | `WeaponData` + 3 armas com cubos/placeholder + barra de Essência do Sonho + troca de arma. Testar se é **divertido** antes de fazer arte | ✅ implementado e testado |
| **F2.1 — Ajustes do tiro** | Recarga R, recuo com curva, alcance infinito com queda, rastro novo, projétil + estilingue, impacto ([prompt](prompts/armas/PROMPT_ZIVA_AJUSTES_TIRO.md)) · animação do soco esquerdo (Blender) | ✅ testado |
| **F2.2 — Ajustes finais do tiro** | Lascas, bosses só piscam, recuo por arma, rastro de dia, automática, carregável ([prompt](prompts/armas/PROMPT_ZIVA_AJUSTES_TIRO_2.md)) | ✅ testado |
| **F2.3 — Fecha o tiro** | Limite do recuo na rajada (mão esquerda aparecia) + testes antigos ([prompt](prompts/armas/PROMPT_ZIVA_AJUSTES_TIRO_3.md)) | ✅ — **fase do tiro (F2) fechada** |
| **F3 — Guia de estilo** | [Guia](docs/armas/guia-estilo.md) ✅ · revólver do fazendeiro v2 (enferrujado, laranja claro) no jogo como **protótipo** do estilo ✅ — precisa de muito polimento (P-03) | ✅ fechada |
| **F4 — Progressão** | Níveis da máquina por boss, bigorna com sucata, Caixa de Venda como estação, pilares de boss com oferenda | ⏳ |
| **Antes da F5** | Atualizar a planilha de armas com os campos de [ficha-campos.md](docs/armas/ficha-campos.md) e revisar a lista oficial ([lista v3](docs/armas/lista-oficial-proposta.md) ✅) | ✅ planilha atualizada (Armas v1, Corpo a Corpo v1, Regras atuais) |
| **F5a — Armas de duas mãos** | Espingarda de Rolha → Metralhadora de Sementes → Rifle de Pressão ([pedido de modelagem](prompts/blender/PROMPT_BLENDER_ARMAS_DUAS_MAOS.md) ✅ · [prompt do Ziva](prompts/armas/PROMPT_ZIVA_ARMAS_DUAS_MAOS.md)) | ✅ no jogo (polir depois) |
| **F5b — Estilingue + corpo a corpo** | Estilingue ✅ no jogo · armas à direita ✅ · Corpo a corpo: [sistema](docs/armas/sistema-corpo-a-corpo.md) ✅ mecânica aceitável no jogo (bloco provisório) · modelos e polimento depois (P-05) | ✅ |
| **F5c — Machadinha** | Mecânica primeiro ([proposta](docs/armas/machadinha.md) ✅ · [prompt](prompts/armas/PROMPT_ZIVA_MACHADINHA.md)) → teste → modelo | 🟡 **agora** |
| **F5d — Fila de produção das armas** | Ordem dos prompts (todos prontos em `prompts/`): | ✅ **armas V1 prontas** (polir depois: P-06) |

**Fila (um por vez, testando entre eles):**
1. Ziva — [Machadinha](prompts/armas/PROMPT_ZIVA_MACHADINHA.md)
2. Ziva — [Tiros especiais: Queimar + Pregos + Rojão + Lampião](prompts/armas/PROMPT_ZIVA_TIROS_ESPECIAIS.md)
3. Ziva — [Armas contínuas: Lança-Chamas + Mangueira](prompts/armas/PROMPT_ZIVA_ARMAS_CONTINUAS.md)
4. Ziva — [Espantalho](prompts/armas/PROMPT_ZIVA_ESPANTALHO.md)
5. Modelagem (em paralelo, quando a mecânica da categoria estiver aprovada): [regras comuns](prompts/blender/PROMPT_BLENDER_REGRAS_ARMAS.md) + [corpo a corpo](prompts/blender/PROMPT_BLENDER_CORPO_A_CORPO.md) · [arremessáveis](prompts/blender/PROMPT_BLENDER_ARREMESSAVEIS.md) · [tiro 2ª leva](prompts/blender/PROMPT_BLENDER_ARMAS_TIRO_2.md)
6. Ziva — [integrar modelo](prompts/armas/PROMPT_ZIVA_INTEGRAR_MODELO.md) (reutilizável: cole os dados da modelagem)

| **F5 — Conteúdo** | Bosses na ordem definida, inimigos por papel e bioma, armas da 1ª versão (~12) | ⏳ |
| **F-Otimização** | Medir e melhorar FPS em PC fraco + menu de qualidade gráfica real ([otimizacao.md](docs/sistemas/otimizacao.md)) | ⏳ futuro |
| **F6 — História** | Abertura, frases dos bosses, mudança visual do pesadelo, final | ⏳ |

As etapas abaixo ficam **em espera** até F1 terminar; serão reordenadas pela ordem dos bosses.

## 🧰 Agora: minérios, armaduras, NPCs e estruturas
[Proposta](docs/jogo/equipamento-e-mundo.md) → 2 prompts do Ziva. Boss final (Deus): por último (decisão do Gustavo).

## Conteúdo (em espera)

| Etapa | Assunto | Status | Ficha |
|---|---|---|---|
| 0 | Base: skills atualizadas, roteiro salvo, este repositório | ✅ | — |
| 1 | Polir o caça-níquel no jogo (opcional: som do fogo por raridade, "plim" da arma) | 🟡 | [caca-niquel](docs/objetos/caca-niquel.md) |
| 2 | Tomate Boss — sons + prompt Ziva | ⏳ | [tomate-boss](docs/bosses/tomate-boss.md) |
| 3 | Uva-morcego — sons + prompt Ziva | ⏳ | [uva-morcego](docs/bosses/uva-morcego.md) |
| 4 | Milho — sons + prompt Ziva | ⏳ | [milho](docs/inimigos/milho.md) |
| 5 | Dragão-Pitaya segmentado — sons + prompt Ziva | ✅ | [dragao-pitaya](docs/bosses/dragao-pitaya.md) |
| 6 | Refazer a Batata-golem | ⏳ | [batata-golem](docs/bosses/batata-golem.md) |
| 7+ | Novos inimigos e bosses no pacote padrão; talvez os modelos antigos | ⏳ | [inimigos](docs/inimigos/README.md) |

## Trilha paralela: sistema de armas

| Etapa | O quê | Status |
|---|---|---|
| A1 | `WeaponData` (Resource) + inventário + troca com tempo de saque | ⏳ |
| A2 | Corpo a corpo (preparo/ativo/recuperação, área por tipo) | ⏳ |
| A3 | À distância (instantâneo, projétil, contínuo, arremesso; pente, recarga) | ⏳ |
| A4 | Barra de Essência do Sonho no HUD (recarga + especial) | ⏳ |
| A5 | Status (Queimar, Atordoar, Eletrizar, Lentidão/congelar) | ⏳ |
| A6 | Ataques especiais | ⏳ |
| A7 | Lendárias, uma por vez | ⏳ |
| — | Visual na mão: R08 Revólver (modelo + animações + `ArmaFps`) | ✅ |

## Trilha paralela: player

| O quê | Status |
|---|---|
| Braços FPS (mão nua: soco, guarda, pegar, gestos, pulo por mola) | ✅ |
| Poses próprias por item/arma | ⏳ |
| Entrada de boss (`boss_intro.tscn`) aplicada a **todos** os bosses | 🟡 |
