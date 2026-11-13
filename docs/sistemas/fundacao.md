# Fundação: salvar/carregar, menu e criação de mundo (F1.7)

> Status: ✅ decidido · Prompt: [PROMPT_ZIVA_FUNDACAO](../../prompts/fundacao/PROMPT_ZIVA_FUNDACAO.md)

## Por que agora
- O mundo é persistente (estilo Terraria), mas hoje **nada é salvo**.
- Cada sistema novo que nasce sem salvar vira retrabalho depois.
- Soneca/Pesadelo e seed variável precisam de uma tela de criação.

## Menu principal (proposta)
- **Novo mundo:** nome, seed (opcional; vazio = aleatória), modo **Soneca** ou **Pesadelo**.
- **Continuar / Carregar:** lista de mundos salvos (nome, modo, dias, bosses derrotados, data).
- **Opções:** volume, gráficos, controles (reaproveita o menu de pausa).
- **Sair.**
- (Futuro) **Multiplayer:** hospedar / entrar.

## O que é salvo (proposta)
| Grupo | O quê |
|---|---|
| Mundo | nome, seed, modo, dia e hora, clima |
| Progressão | bosses derrotados, raridades liberadas na máquina, fase de inimigos, vacas-melancia mortas |
| Mapa (só as **diferenças** da seed) | árvores/pedras/minérios coletados, monumentos limpos, santuários usados |
| Construções | tudo o que foi construído (posição, rotação, tipo) + conteúdo dos baús |
| Jogador | posição, vida, inventário, armaduras e acessórios equipados, R$, sucata, cama/ponto de renascer |
| Armas | nível de cada arma — o formato deve aceitar **nível por cópia** (ajuste C07 virá depois) |

Mundo procedural = **seed + diferenças**: não se salva o terreno inteiro, só o que mudou.

## Quando salva (proposta)
- Automático: ao **dormir na cama**, a cada **amanhecer** e ao **sair** pelo menu.
- Sem "salvar a qualquer momento" no modo Pesadelo (evita salvar/recarregar para fugir da morte).

## Decisões
1. ✅ **Pesadelo:** ao morrer, o **mundo é apagado** (Muck puro).
2. ✅ **Personagem dentro do mundo.** Em multiplayer, o host guarda o inventário de cada jogador no próprio mundo.
3. ✅ Recursos coletados **renascem** (padrão: 3 dias).
4. ✅ Mundos salvos **sem limite**.
5. ⚙️ Soneca (escolha do Claude, ajustável): perde 30% do R$/sucata e 50% dos recursos; armas, armaduras, acessórios e ferramentas ficam.

## Regras para multiplayer (já valem aqui)
- O save pertence ao **host**.
- Dados de jogador guardados por **ID do jogador**, não "o player".
- Nada de estado salvo em singletons que assumem um jogador só.
