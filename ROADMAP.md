# Roteiro de desenvolvimento

> Atualize este arquivo sempre que uma etapa mudar de status.

## 🎯 Fase atual: revisão geral
Ver o que já existe, o que tirar, o que colocar e o que ajustar — antes de seguir com bosses e armas.
- Lista de trabalho: [docs/jogo/revisao.md](docs/jogo/revisao.md)
- Identidade do jogo: [docs/jogo/identidade.md](docs/jogo/identidade.md)

### Plano de ação
| Fase | O quê | Status |
|---|---|---|
| **F1 — Decisões** | ✅ loop, níveis da máquina, ordem dos bosses, reinvocação, Essência do Sonho, morte (Soneca/Pesadelo), construção, multiplayer, minérios → armaduras | ✅ quase |
| **F1.5 — Inventário** | Levantar tudo o que existe e decidir o destino ([inventario.md](docs/jogo/inventario.md)) | ✅ |
| **F1.6 — Limpeza** | Ziva removeu o que foi cortado (catálogo 101 → 76 itens) ([PROMPT_ZIVA_LIMPEZA](prompts/limpeza/PROMPT_ZIVA_LIMPEZA.md)) | 🟡 falta teste no jogo + commit |
| **F1.7 — Fundação** | Salvar/carregar + menu principal + criação de mundo (seed, Soneca/Pesadelo) | ⏳ próximo |
| **F2 — Protótipo do tiro** | `WeaponData` + 3 armas com cubos/placeholder + barra de Essência do Sonho + troca de arma. Testar se é **divertido** antes de fazer arte | ⏳ |
| **F3 — Guia de estilo** | Guia de armas (paleta, proporções, material toon) + redesign do R08 como teste + padrão de shading para todos (I03) | ⏳ |
| **F4 — Progressão** | Níveis da máquina por boss, bigorna com sucata, Caixa de Venda como estação, pilares de boss com oferenda | ⏳ |
| **F5 — Conteúdo** | Bosses na ordem definida, inimigos por papel e bioma, armas da 1ª versão (~12) | ⏳ |
| **F6 — História** | Abertura, frases dos bosses, mudança visual do pesadelo, final | ⏳ |

As etapas abaixo ficam **em espera** até F1 terminar; serão reordenadas pela ordem dos bosses.

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
