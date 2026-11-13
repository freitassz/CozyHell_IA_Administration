# Registro de decisões

> Uma linha por decisão, com data quando possível. Inclui o que foi **descartado** para não ser proposto de novo.

## Princípios
- O jogo é **simples na essência**. Complexidade só quando deixa o jogo dinâmico.

## Estrutura (nov/2026)
- Mundo persistente estilo Terraria: boss final existe, mas o mundo continua.
- Bosses aparecem por **pilares de boss** com oferenda; inimigos por spawn natural + pilares.
- Construção de base é **opcional**.
- Arma repetida na máquina vira sucata.
- 3 biomas: Planície, Floresta, Pedreira.
- Projeto Godot versionado no GitHub.

## Progressão (nov/2026)
- Cada boss dropa **ficha de raridade** e **libera essa raridade na máquina** (Tomate → Raro).
- Cada boss dropa **material único**: próxima oferenda **ou** arma exclusiva de boss.
- Pesadelo = **progressão de jogo** (inimigos novos após certos bosses, como a Plantera), não mudança estética do mundo.
- 4 minérios existem desde o início; o acesso é travado pela **picareta**, feita com drops de inimigos de fases do pesadelo.
- Ordem dos bosses: Tomate → Uva-morcego → Dragão-Pitaya → Batata-golem → Final.
- Construção ganha mais importância (estações fazem parte da progressão).
- Morte: dois modos — **Pesadelo** (hardcore, estilo Muck) e **Soneca** (renasce perdendo parte dos itens e do dinheiro).
- Boss já derrotado pode ser reinvocado com oferenda **simples, de itens comuns**.
- Avanço do pesadelo é anunciado com animação pelo mundo + mensagem.
- Minérios servem para alguns itens e **principalmente armaduras**.
- **Multiplayer: vai ter**, se possível. Código novo já segue as regras de multiplayer (ver loop.md).
- Stamina = movimento (correr, pular etc.).
- **Essência do Sonho** (nome provisório): barra única das armas. Serve para **recarregar** e para o **especial/tiro forte**. Enche com tiros, socos (muito mais) e regeneração natural.
- A lista de 35 armas é **rascunho**; vai mudar bastante.

## Armas
- Raridade é **só etiqueta**, sem multiplicador; a força está nos números da arma.
- Golpe normal **não gasta stamina**; só o ataque especial gasta.
- Sem limite de slots: carrega quantas o inventário aguentar.
- Recarregar gasta **Essência do Sonho** (ver Progressão).
- ⚠️ A planilha de armas é **rascunho**: superaquecimento (em aberto) e outros detalhes dela estão em revisão.
- Status reduzidos a 4: Queimar, Atordoar, Eletrizar, Lentidão.

## ❌ Descartado
- Máquina de cerveja para recuperar stamina.
- Mudança estética do mundo inteiro a cada boss (pesadelo vira progressão de inimigos).
- Durabilidade, conserto com sucata, afiar, sujeira/enguiço.
- Combustível ou ingrediente para lendárias, fome da arma.
- Peso e carga, fraquezas por arma.
- Status Sangrar, Marcar, Molhar, Quebrar Defesa.
- `Monte_Terra` (montinho de terra no rastro do dragão) — ficou esquisito.
- Dividir o dragão em 2 corpos — preferido **1 corpo só**.
- Folha de referência da batata-golem ("paia").
- Braços: realista com dedos separados, "geométrico" de cubos, malha única por remesh.
