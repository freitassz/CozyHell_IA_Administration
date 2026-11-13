# Instruções para o Claude neste repositório

Este repo é a central de organização do jogo **CozyHell3D**. O usuário escreve em português; responda em português.

## Ao começar uma conversa
1. Leia `ROADMAP.md` e diga em que etapa estamos.
2. Pergunte qual assunto ele quer tratar (armas, boss, inimigo, objeto, player, pipeline…), se não estiver claro.
3. Leia **só** a ficha do assunto escolhido em `docs/`.

## Skills relacionadas
- `anthropic-skills:lowpoly-game-3d-blender` — modelagem, rig, animação, sons.
- `anthropic-skills:cozyhell-prompts-ziva` — prompts para o Ziva AI e sistema de armas.
Carregue a skill correspondente antes de modelar ou escrever prompt.

## Regras de documentação
- Cada arma/inimigo/boss/objeto tem **uma ficha** em `docs/<categoria>/`. Use os modelos de `templates/`.
- Ao terminar algo, **atualize**: a ficha, o índice da categoria (`README.md` da pasta), o `ROADMAP.md` e, se houve decisão de design, `docs/jogo/decisoes.md`.
- Prompts entregues ao Ziva vão para `prompts/<assunto>/` com o nome `PROMPT_ZIVA_<ASSUNTO>.md`.
- Os **números das armas** vivem na planilha "Cozy Hell — Sistema de Armas" (fonte da verdade). Não duplique valores aqui; registre só conceito, estado e decisões.
- Trabalhe por etapas, uma mudança por vez, e pense em economia de tokens.
- Commits em português, curtos e descritivos.
