# Fundação: salvar/carregar, menu e criação de mundo (F1.7)

> Status: ✅ **implementado** (nov/2026) · Prompt: [PROMPT_ZIVA_FUNDACAO](../../prompts/fundacao/PROMPT_ZIVA_FUNDACAO.md)

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

## Achados da Etapa 0 (Ziva)
- Não existia contador de dias → criado `dia` (+1 ao amanhecer).
- Recursos e monumentos sem ID → **ID = tipo + posição (x, z) arredondada a 0,1 m**.
- Vacas, máquinas repostas, totem, grupos iniciais de inimigos e clima usavam RNG global → passam a usar a **seed** (mesma seed = mesmo mundo). Hordas noturnas podem continuar aleatórias.
- Itens salvos pelo `resource_path` (variantes de raridade compartilham o mesmo `id`).
- Morte antiga tirava só 10% do R$ → passa para 30% R$/sucata e 50% recursos.
- Cama só curava → passa a ser **ponto de renascer** e salvar o jogo.
- Uva e Totem não registravam derrota → passam a registrar (sem mudar regras de progressão; Totem não sobe tier).

## Como ficou no jogo
- Autoload `SaveManager`; `user://saves/<id>/mundo.json` + `estado.json`; escrita por arquivo temporário.
- Nó `MapaMudancas`: recursos coletados (com dia) e monumentos silenciados. Renascem em 3 dias, só com o jogador a 20 m ou mais.
- Vacas, totem, máquinas repostas, grupos iniciais e clima: RNG com `seed + offset + contador`.
- Bosses registram derrota (Tomate, Uva, Dragão, Totem) sem mudar o tier.
- Morte: Soneca 30% R$/sucata e 50% recursos; Pesadelo apaga o mundo. Cama = ponto de renascer + salva.

### Falta validar jogando
- [ ] Matar um boss pelo ovo do F3 → recarregar → continua derrotado.
- [ ] Esperar uma reposição de máquina (~15 min) → salvar/carregar → no mesmo lugar.
- [ ] Fechar o processo no meio de um amanhecer → carrega no estado do amanhecer.

### Observações
- Jogador assenta ~4 cm no chão ao carregar (física do motor, normal).
- Malhas de graveto/pedra ainda sorteiam o visual com RNG global (só aparência, posição é fixa).

## Regras para multiplayer (já valem aqui)
- O save pertence ao **host**.
- Dados de jogador guardados por **ID do jogador**, não "o player".
- Nada de estado salvo em singletons que assumem um jogador só.
