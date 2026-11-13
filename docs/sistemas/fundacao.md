# Fundação: salvar/carregar, menu e criação de mundo (F1.7)

> Status: 🟡 proposta do Claude. Itens ❓ precisam de decisão antes do prompt do Ziva.

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
| Jogador | posição, vida, inventário, armaduras e acessórios equipados, nível das armas, R$, sucata, cama/ponto de renascer |

Mundo procedural = **seed + diferenças**: não se salva o terreno inteiro, só o que mudou.

## Quando salva (proposta)
- Automático: ao **dormir na cama**, a cada **amanhecer** e ao **sair** pelo menu.
- Sem "salvar a qualquer momento" no modo Pesadelo (evita salvar/recarregar para fugir da morte).

## Decisões abertas
1. ❓ **Pesadelo: o que acontece ao morrer?**
   - A) O mundo é **apagado** (Muck puro).
   - B) O **personagem** perde tudo e recomeça, mas o mundo e as construções ficam.
2. ❓ **Personagem separado do mundo** (Terraria: leva o personagem para outro mundo) ou **personagem dentro do mundo** (mais simples; cada mundo tem seu jogador)?
   - Proposta: **dentro do mundo**. Em multiplayer, o host guarda o inventário de cada jogador no próprio mundo.
3. ❓ Árvores e pedras coletadas **renascem** com o tempo ou somem para sempre?
4. ❓ Quantos mundos salvos ao mesmo tempo? (proposta: sem limite)

## Regras para multiplayer (já valem aqui)
- O save pertence ao **host**.
- Dados de jogador guardados por **ID do jogador**, não "o player".
- Nada de estado salvo em singletons que assumem um jogador só.
