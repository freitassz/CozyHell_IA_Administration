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

## Inventário (nov/2026)
- Armas por **máquina caça-níquel** e **bigorna**. Mesa de Contrato sai agora; a troca de itens por arma pode virar **NPC** no futuro.
- **Loja** (`unlock_pistol`) removida.
- Armas placeholder removidas (Pistola, Rifle, Escopeta, Canhão de Batatas, Espadas, Foice, Marreta). Fica o **Revólver**; o resto segue a planilha (que ainda será atualizada).
- Plantações **são** os inimigos. Chuva deixa inimigos mais fortes/rápidos; acelerar crescimento foi descartado.
- Moedas = R$ do HUD. Pilar de boss já existe. Hoje só existe 1 minério (ferro).

- Inimigos por **fases**: 1 = Tomate, Cenoura, Pimentão; 2 = Cebola, Milho, Abóbora; 3 em aberto. Variantes Mutante/Ancestral **descontinuadas**.
- **Totem de Melancia** = boss secreto (matar 10 vacas-melancia).
- Boss final: ideia de um deus no céu (a desenvolver); Espantalho Vulcânico como reserva.
- Sementes de chefe: em aberto.
- Enxada e pá removidas. Vara de pesca: futuro, prioridade muito baixa.
- Drops de inimigo (comidas) são placeholders; cozinhar na fogueira no futuro.
- Acessórios: caça-níquel próprio mantido; empilham com **limite por tipo** e **bônus decrescente** por cópia; podem ser retirados.
- Batata como inimigo: em aberto.
- **Arma repetida não vira sucata automaticamente** e não dá bônus automático (o `grant_weapon_bonus` antigo sai). Na **bigorna** o jogador escolhe:
  - **Fundir:** consome 1 cópia, a arma sobe de nível (máx. **5**); cada nível melhora **um pouco** os status base, com melhoria decrescente (não é 5x de dano).
  - **Desmanchar:** consome 1 cópia e dá sucata.
  - 🔧 Ajuste futuro aprovado: nível **por cópia** (não por tipo) e fusão **por soma** (nv3 + nv2 = nv5, máx. 5). Ver `docs/armas/sistema.md`.
- Armas continuam **descartáveis**: o normal é trocar por uma melhor.
- Santuário **fica no mapa** depois do boss para reinvocar.
- Santuários terão **rework total** (oferendas, bosses, posições).
- **Plantio pelo jogador descontinuado** (com enxada e pá).
- **Vendinha descontinuada** como objeto do mapa: vender passa a ser uma **construção** que o jogador constrói.
- Santuários = pilares de boss (5 no jogo hoje).
- **Seed define o mundo inteiro:** mesma seed = mesmo mapa, vacas, totem, máquinas e clima. Para outro mundo, outra seed. Só o que reage ao jogador em tempo real (hordas noturnas) pode variar.
- **Fundação:** personagem dentro do mundo; mundos sem limite; recursos renascem; salva na cama, ao amanhecer, ao sair e ao fechar; sem salvar manual.
- **Pesadelo:** morreu, o mundo é apagado. **Soneca:** renasce perdendo parte do R$/sucata e dos recursos.
- Mesa de Contrato vira **NPC futuro** que troca itens por **fichas de raridade**.

## Armas
- Raridade é **só etiqueta**, sem multiplicador; a força está nos números da arma.
- Golpe normal **não gasta stamina**; só o ataque especial gasta.
- Sem limite de slots: carrega quantas o inventário aguentar.
- Recarregar gasta **Essência do Sonho** (ver Progressão).
- ⚠️ A planilha de armas é **rascunho**: superaquecimento (em aberto) e outros detalhes dela estão em revisão.
- Status reduzidos a 4: Queimar, Atordoar, Eletrizar, Lentidão.

## ❌ Descartado
- Variantes de inimigo Mutante/Ancestral.
- Enxada e pá (sistema de plantar).
- Loja `unlock_pistol`.
- Chuva acelerando o crescimento das plantações.
- Armas placeholder antigas.
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
