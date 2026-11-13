# Roteiro de desenvolvimento

> Atualize este arquivo sempre que uma etapa mudar de status.

## 🎯 Fase atual: revisão geral
Ver o que já existe, o que tirar, o que colocar e o que ajustar — antes de seguir com bosses e armas.
- Lista de trabalho: [docs/jogo/revisao.md](docs/jogo/revisao.md)
- Identidade do jogo: [docs/jogo/identidade.md](docs/jogo/identidade.md)

As etapas abaixo ficam **em espera** até a revisão definir loop, estilo e escopo.

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
| A3 | À distância (instantâneo, projétil, contínuo, arremesso; pente, recarga, superaquecimento) | ⏳ |
| A4 | Barra de energia no HUD + custo da recarga | ⏳ |
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
