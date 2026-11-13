# CozyHell3D — Central de Desenvolvimento

Repositório de **organização e documentação** do jogo **CozyHell3D** (Godot 4, primeira pessoa, low-poly).
O código do jogo fica no projeto Godot (`3dddddd`). Aqui ficam o roteiro, as decisões e a ficha de cada arma, inimigo e boss.

## Como usar

Abra uma conversa com o Claude neste repositório e escolha um assunto:

| Assunto | Onde está |
|---|---|
| 🗺️ Roteiro / próximas etapas | [ROADMAP.md](ROADMAP.md) |
| 🎮 Visão geral do jogo | [docs/jogo/visao-geral.md](docs/jogo/visao-geral.md) |
| 📐 Padrões que funcionaram | [docs/jogo/padroes.md](docs/jogo/padroes.md) |
| 📝 Decisões tomadas (e descartadas) | [docs/jogo/decisoes.md](docs/jogo/decisoes.md) |
| ⚔️ Armas | [docs/armas/](docs/armas/README.md) |
| 👑 Bosses | [docs/bosses/](docs/bosses/README.md) |
| 👾 Inimigos comuns | [docs/inimigos/](docs/inimigos/README.md) |
| 🎰 Objetos interativos | [docs/objetos/](docs/objetos/README.md) |
| ✋ Player (braços FPS) | [docs/player/bracos-fps.md](docs/player/bracos-fps.md) |
| 🛠️ Pipeline (Blender, sons, prompts Ziva) | [docs/pipeline/](docs/pipeline/README.md) |
| 🤖 Prompts entregues ao Ziva | [prompts/](prompts/README.md) |
| 📄 Modelos de ficha | [templates/](templates/) |

## Legenda de status

- ✅ Pronto (no jogo e testado)
- 🟡 Em andamento / parcial
- ⏳ Pendente
- ❌ Descartado

## Quem faz o quê

- **Gustavo** — direção, testes no jogo, decisões de design.
- **Claude** — modelos 3D (Blender via Python), sons sintetizados, prompts para o Ziva, documentação.
- **Ziva AI** — escreve o código GDScript dentro do Godot.
