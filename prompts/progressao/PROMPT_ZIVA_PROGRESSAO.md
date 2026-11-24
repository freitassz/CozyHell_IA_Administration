# PROMPT ZIVA — F4: Sistema de progressão (santuários com ritual, oferendas, drops, fichas, máquina por nível, fase do pesadelo)

## Contexto
Hoje os santuários (`SHRINE_DEFS`) estão em modo `# TEMP` (3 sementes de chefe, 5 bosses antigos), a máquina sorteia qualquer raridade e não existe fase do pesadelo. Agora entra a **progressão de verdade**: cada boss pede uma oferenda, dropa uma ficha e um material, e libera algo.
Dá para testar tudo com os **ovos do F3**, mesmo com bosses ainda sem luta completa.
- **Não mude o que não está pedido.** Faça **uma etapa por vez** e teste. Comente em português. ⚙️ = valor escolhido por mim.
- **Tudo o que for estado vai para o save** (grupo `salvavel`). Mesma seed = santuários nos mesmos lugares.
- Multiplayer: progressão é **do mundo** (compartilhada); itens saem do inventário de **quem** interagiu.

## ETAPA 0 — Relatório curto (siga em frente se não houver bloqueio)
Me diga: o drop atual de cada inimigo (Tomate, Cenoura, Pimentão, Cebola, Milho; Abóbora existe?), as cenas dos bosses (Tomate Gigante, Uva, Dragão-Pitaya, Totem; existe Batata-golem?) e onde a máquina escolhe a raridade.

## ETAPA 1 — Itens novos
`ItemData` com ícone/malha provisória (formas simples, cores fortes, fosco):
- **Fichas:** Ficha Rara (azul `#2F8BFF`), Ficha Épica (roxa `#A23DFF`), Ficha Lendária (amarela `#FFD21F`).
- **Materiais de boss:** Casca do Tomate, Semente de Uva Sombria, Escama de Pitaya, Raiz de Pedra, Material Final (nome provisório).

## ETAPA 2 — `ProgressionManager` novo
- Guarda: **bosses derrotados**, **raridades liberadas** (começa só Comum), **fase do pesadelo** (começa 1), **santuário final erguido** (não/sim). Tudo no save (substitui o `current_world_tier`/`BOSS_STAGE` antigo; converta saves antigos sem quebrar).
- Tabela de bosses (um `Resource` por boss ou um dicionário bem comentado):

| id | Santuário (bioma) | 1ª oferenda (3 itens) | Reinvocar (3 itens) | Dropa | Libera |
|---|---|---|---|---|---|
| `tomate` | Planície | drop do Tomate, drop da Cenoura, drop do Pimentão | 3× drop do Tomate | Ficha Rara + Casca do Tomate | raridade **Raro** |
| `uva` | Floresta | Casca do Tomate, drop da Cenoura, drop do Pimentão | 3× drop da Cenoura | Ficha Rara + Semente de Uva Sombria | **fase 2** |
| `dragao` | Planície (área aberta ⚙️ ≥ 40 m de raio plano o bastante) | Semente de Uva Sombria, drop da Cebola, drop do Milho | 3× drop do Milho | Ficha Épica + Escama de Pitaya | raridade **Épico** |
| `batata` | Pedreira | Escama de Pitaya, Minério de Ferro, drop da Cebola | 3× drop da Cebola | Ficha Épica + Raiz de Pedra | raridade **Lendário** + **ergue o santuário final** |
| `final` | centro do mapa ⚙️ | Raiz de Pedra, Escama de Pitaya, Semente de Uva Sombria | (depois) | Ficha Lendária + Material Final | fim da campanha (só registrar) |
| `totem` (secreto) | — | — (10 vacas-melancia, como hoje) | — | Ficha Épica | nada |

- Cenas: Tomate Gigante, Uva-morcego, Dragão-Pitaya e Totem existentes. **Batata-golem ainda não existe:** use a cena do Golem de Raiz como **substituto `# TEMP`**. **Final:** ainda não existe → o santuário final não invoca nada por enquanto (mensagem "Ainda não…").
- Remova do jogo os santuários antigos da **Hidra Picante** e do **Espantalho Vulcânico** (mova cenas para `res://_arquivo/`).

## ETAPA 3 — Santuários e o ritual
- Um santuário por boss da tabela, colocado **pela seed** no bioma indicado (determinístico). Ficam no mapa para sempre.
- **Ritual:** ao apertar **E** no santuário, o jogo **coloca 1 item por vez** da oferenda, **pegando direto do inventário** (não precisa estar na mão), na ordem da tabela.
  - Usa a **1ª oferenda** até aquele boss ser derrotado; depois, a de **reinvocar**.
  - Faltando o próximo item: mensagem curta "Falta: <item>".
  - Cada item colocado aparece **girando em volta do altar** (órbita ⚙️ raio 1,2 m, altura do altar), com um **rastro** (mesmo sistema de rastro, cor do item ou lilás `#B98CFF`).
  - Com os **3 itens**: eles **voam para o centro do santuário**, **explodem** (clarão + partículas, sem dano) e o **boss é invocado** (entrada de boss existente, se houver).
  - Itens já colocados ficam no altar (e no save) até completar. Bloqueado enquanto o boss daquele santuário estiver vivo.
- **Santuário final:** existe desde o início, **meio enterrado** (só o topo para fora). Não aceita itens. Quando `batata` for derrotado: **sobe do chão** (⚙️ 4 s, tremida + poeira) e passa a aceitar a oferenda (o boss final ainda não existe).

## ETAPA 4 — Drops e liberações
- Ao morrer, o boss **dropa** no chão a ficha e o material (itens coletáveis), registra a derrota e aplica o que libera.
- Liberar raridade ou fase: **mensagem na tela** (ex.: "A máquina agora sorteia armas **Raras**"; "O pesadelo se aprofunda…") + efeito no mundo ⚙️ (pulso lilás no céu por ~3 s + tremida leve). Só na **1ª** derrota.

## ETAPA 5 — Máquina por nível + fichas
- A máquina de armas só sorteia raridades **liberadas**. Chances base ⚙️ Comum 60 / Raro 28 / Épico 10 / Lendário 2, **redistribuídas** só entre as liberadas.
- **Ficha:** com a ficha na mão, usar na máquina = **1 giro garantido** daquela raridade (sem gastar R$; consome a ficha). Funciona mesmo que a raridade ainda não esteja liberada.

## ETAPA 6 — Fase do pesadelo nos inimigos
- Fase 1: Tomate, Cenoura, Pimentão. Fase 2: + Cebola, Milho, Abóbora.
- Vale para o spawn natural, as hordas noturnas e os monumentos. **Abóbora** ainda não existe → pule-a (`# TEMP`) até existir.

## ETAPA 7 — Teste automático
`dev/validate_progressao`: ritual (1 item por E, falta item, 3 itens invocam), 1ª oferenda × reinvocar, drops, liberação de raridade e fase, máquina só sorteia liberadas, ficha garante a raridade, santuário final sobe após `batata`, save/carregar mantém tudo. Placar.

## Checklist
- [ ] Fichas e materiais · [ ] `ProgressionManager` novo, salvo, com conversão do save antigo
- [ ] Santuários pela seed por bioma; Hidra e Espantalho Vulcânico arquivados; Batata = Golem de Raiz `# TEMP`
- [ ] Ritual: 1 item por E do inventário, órbita com rastro, 3 itens voam/explodem/invocam
- [ ] Santuário final meio enterrado que sobe depois do boss 4
- [ ] Drops + mensagens/efeito de liberação · [ ] Máquina por nível + fichas
- [ ] Fase do pesadelo nos spawns · [ ] Validador com placar · Nada além disso foi alterado
