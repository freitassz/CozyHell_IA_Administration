# Revisão geral do jogo

> Lista viva. Um item por vez. Status: 🔴 aberto · 🟡 proposta feita, falta confirmar · ✅ decidido (vai para `decisoes.md`) · ❌ descartado
> Propostas são opinião do Claude pensando no jogo, no público e na diversão — não são decisão.

## Resumo
| ID | Assunto | Status |
|---|---|---|
| H01 | História: sonho do fazendeiro que vira pesadelo | 🟡 |
| I01 | Mundo fofo × armas de fogo | 🟡 |
| I02 | O que é o "Hell" | 🟡 resolvido por H01 |
| I03 | Shading igual em tudo | 🔴 |
| I04 | Violência e feedback de acerto | 🟡 marcador + piscar no protótipo |
| I05 | Como mostrar dano em inimigos comuns (sem números, sem barra) | 🔴 |
| C08 | Soco rápido (V) com arma na mão | 🟡 fallback guardar→socar→sacar; mão esquerda real precisa de `AnimationTree` |
| C09 | **Visual e comportamento do tiro**: rastro amarelo parece errar; projétil visível (estilo Fortnite)? | 🔴 |
| N05 | Inimigo Abóbora não existe no código (fase 2) | 🔴 |
| T04 | `BracosFps.empurrar()` e animação `08_Empurrar` sem uso | 🔴 baixa |
| P01 | Máquina perde sentido depois de boas armas | ✅ |
| P02 | Ciclo do jogo / spawn de boss | 🟡 |
| P03 | Moedas | 🟡 |
| P04 | Fim da partida | ✅ |
| P05 | Morte | ✅ dois modos (detalhes 🟡) |
| P06 | Saltos de poder entre bosses | ✅ |
| C01 | Quantidade de corpo a corpo | ✅ lista de armas é rascunho, vai mudar |
| C02 | Escopo das armas | 🔴 |
| C03 | Munição/recarga | ✅ Essência do Sonho |
| C04 | Recurso do ataque especial | ✅ Essência do Sonho (opção B) |
| C05 | Raridade sem multiplicador | 🟡 |
| N01 | Os 5 bosses e bioma de cada | ✅ (falta o final) |
| N02 | ~8 inimigos com papéis diferentes | ⏸️ depois |
| R01 | Construção: estações × base | ✅ (falta lista de estações) |
| R02 | Sementes que viram inimigo | ✅ são as plantações = sistema de inimigos |
| M01 | Multiplayer | ✅ vai ter; Relay do Ziva é só para Web |
| M02 | Prompts do Ziva prontos para multiplayer | ✅ regra adotada |
| T01 | Projeto Godot versionado | ✅ |
| T02 | Prompts antigos fora do repo | 🔴 |
| P07 | Minérios e picaretas travados por fase do pesadelo | ✅ ideia (falta uso dos minérios) |
| P08 | Armas exclusivas de boss | ✅ ideia |
| P09 | Reinvocar boss com oferenda simples | ✅ |
| P10 | Sistema de armaduras (uso dos minérios) | 🔴 novo |
| P11 | Nome da Essência do Sonho / conflito do nome "Pesadelo" | 🔴 |
| A01 | Inventário do que já existe no jogo | ✅ |
| E07 | Arma repetida | ✅ Fundir (até 5) ou Desmanchar na bigorna |
| E08 | **Rework total dos santuários** (bosses, oferendas, posições; Golem de Raiz ≠ Batata-golem) | 🔴 |
| T03 | Erros antigos: UIDs inválidos em `ground_collectible.tscn`; `basis` sombreado em `ground_collectible.gd:113`; visual de graveto/pedra com RNG global; testes `dev/` quebrados ("dawn makes horde flee", `validate_shrines`, `cacaniquel_test`) | 🔴 baixa |
| E09 | Sementes de chefe só saem de chefes → santuários travados fora do criativo (resolver no rework E08) | ⏸️ |
| C07 | Fundir: nível por cópia + fusão por soma (nv3+nv2=nv5) | 🔧 aprovado, implementar depois |
| C06 | Superaquecimento de arma | 🟡 em aberto (já discutido, decidir depois) |
| E01 | Salvar/carregar | ✅ |
| E02 | Menu principal + criação de mundo (seed, Soneca/Pesadelo) | ✅ |
| E03 | Formas de ganhar arma | ✅ máquina + bigorna; Mesa → NPC futuro; loja ❌ |
| E04 | Sementes de chefe | ⏸️ ver no futuro |
| E05 | Comidas, fogueira, enxada, pá, pesca | ✅ resolvido |
| E06 | Inimigos por fases (sem Mutante/Ancestral) | ✅ |
| A02 | Máquina de acessórios | ✅ mantém; acessórios empilham com limite (detalhes 🟡) |
| N03 | Boss final (deus no céu?) | ⏸️ |
| N04 | Inimigos da fase 3 / Batata como inimigo | ⏸️ |

---

## H — História

### H01 🟡 Sonho do fazendeiro
- **Ideia do Gustavo:** tudo é o sonho de um fazendeiro; as plantas atacam porque ele é fazendeiro.
- **Análise:** é a melhor ideia da lista — explica o nome, o mundo fofo, os inimigos de comida **e** as armas absurdas. Hoje não está no jogo.
- **Proposta:** o sonho começa bom (cozy) e vira pesadelo (hell) a cada boss. Contar a história com pouco texto: tela inicial com o fazendeiro dormindo, uma frase na entrada de cada boss, mudança de céu/cor ao avançar, e um final no boss final (ele "acorda"? o pesadelo vence?). Ver [loop.md](loop.md).

## I — Identidade e estilo

### I01 🟡 Mundo fofo × armas de fogo
- **Proposta:** armas são **coisas de fazendeiro que viraram arma no sonho** — gambiarra da roça, proporção de brinquedo, cores da paleta do jogo, shader toon + contorno das mãos, efeitos coloridos (suco, sementes, rolhas). O R08 precisa de redesign visual (animações e `ArmaFps` continuam valendo).
- **Próximo passo:** um **guia de estilo de armas** (1 página com paleta, proporções, materiais) e testar no R08.

### I02 🟡 O "Hell"
- Resolvido por H01: Hell = pesadelo que cresce com a progressão.

### I03 🔴 Shading igual em tudo
- Mãos: toon + contorno. Inimigos/bosses: Principled. Modelos antigos: outro processo. Definir um material padrão, testar todos numa cena e listar quem destoa.

### I04 🔴 Violência e feedback de acerto
- Inimigo morre em suco, sementes e pedaços (sem sangue). Marcador de acerto na mira, som de acerto, inimigo pisca/achata. Em FPS, isso vale mais que o modelo da arma.

## P — Loop e progressão

### P01 🟡 Máquina depois de ter boas armas
- **Já existe:** repetida vira sucata. Isso resolve metade.
- **Proposta:** sucata vai para a **bigorna** melhorar armas, e a máquina ganha **níveis liberados pelos bosses** (ver P06). Toda rodada vale algo.

### P02 🟡 Ciclo do jogo / spawn de boss
- **Definido:** inimigos por spawn natural + pilares de inimigos; bosses por **pilares de boss com oferenda**.
- **Proposta:** a oferenda de cada boss é feita com o material do boss anterior → define a ordem sem travar o mundo.

### P03 🟡 Moedas
- **Proposta:** R$ (venda) → máquina. Sucata (repetidas) → bigorna e construção. Material de boss → melhorias altas e oferendas.

### P04 ✅ Fim da partida
- Igual Terraria: existe boss final, mas o mundo continua depois.

### P05 🔴 Morte
- O que se perde ao morrer? Muck = recomeça tudo; Terraria = perde parte do dinheiro e volta ao spawn.
- **Proposta:** como o mundo é persistente (Terraria), **não** apagar o progresso: renasce na cama do fazendeiro e perde parte do R$ carregado. Roguelike puro não combina com mundo persistente.

### P06 🟡 Saltos de poder entre bosses
- **Problema do Gustavo:** falta o "Terraria": matar um boss mudar o jogo e preparar para o próximo.
- **Proposta:** cada boss (1) abre um nível da máquina, (2) dropa um material único para a bigorna e a próxima oferenda, (3) aprofunda o pesadelo (cor do mundo, inimigos novos, minérios). Tabela em [loop.md](loop.md).

## C — Combate e armas

### C01 🟡 Corpo a corpo num jogo de tiro
- **Mudança na minha proposta anterior:** em vez de só cortar, dar um **papel**: golpe corpo a corpo enche muito mais a barra de energia ("corpo a corpo para recarregar, tiro para matar"). Mesmo assim, reduzir de 15 para ~5–6 armas corpo a corpo.

### C02 🔴 Escopo das armas
- Primeira versão jogável com ~12 armas; o resto em atualizações. Fica junto com N01 (as armas por nível da máquina).

### C03 🟡 Munição/energia
- Mantém a barra estilo Hollow Knight (✅ decidido antes).
- **Risco de espiral** (errou → sem energia → sem tiro). Proposta: corpo a corpo enche muito + regeneração lenta ou recarga lenta grátis com barra vazia. Pente não enche ao trocar de arma.
- **Precisa de protótipo** antes de arte: é a mecânica que mais define se o tiro é divertido.

### C04 🔴 Recurso do ataque especial
- **Atualização:** stamina de movimento ✅ (correr, pular). Máquina de cerveja ❌. O Gustavo quer uma barra própria para armas e pediu alternativas — ver a resposta do Claude de nov/2026 e decidir.

#### (histórico) Stamina e máquina de cerveja
- **Análise:** a máquina de cerveja não combina com o tom (e álcool restringe a classificação etária). Mas o problema real é que stamina ligada a arma é redundante com o cooldown do especial.
- **Proposta:** stamina só para correr/esquivar/pular, regenera sozinha. Especial só com cooldown. Máquina de cerveja ❌.

### C05 🟡 Raridade sem multiplicador
- Continua, mas agora a raridade também diz **em que nível da máquina** a arma aparece.

## N — Conteúdo

### N01 🟡 Os 5 bosses
- 3 biomas (Planície, Floresta, Pedreira) para 5 bosses. Rascunho de ordem:

| # | Boss | Bioma | Motivo |
|---|---|---|---|
| 1 | Tomate Boss | Planície | ataques simples (pulo, mordida), bom para ensinar |
| 2 | Uva-morcego | Floresta | voa: obriga a mirar para cima, testa armas de distância |
| 3 | Batata-golem | Pedreira | batata + pedra combinam; tanque |
| 4 | Dragão-Pitaya | cava por qualquer bioma | o mais complexo que existe hoje |
| 5 | **Final (novo)** | o pesadelo | precisa ligar à história (ex.: o Espantalho, o "dono" do pesadelo) |

- PepperBoss e CowMellonBossTikiTiki (antigos): virar inimigo forte/mini-boss ou sair.

### N02 🔴 ~8 inimigos com papéis
- Tabela de papéis (corpo a corpo rápido, atirador, voador, tanque, enxame, kamikaze, suporte, emboscada) e um inimigo por papel, distribuídos pelos biomas e níveis de pesadelo.

## R — Sistemas

### R01 🟡 Construção
- **Proposta:** separar **estações** (bancada, bigorna, Caixa de Venda — itens que se colocam em qualquer lugar e fazem parte da progressão) de **base** (paredes, decoração — opcional). A Caixa de Venda vira estação fabricável.

### R02 🟡 Sementes que viram inimigo
- **Análise:** concordo que é redundante com pilares + spawn natural. Manter custaria e seria pouco usado.
- **Proposta:** cortar como "spawn de inimigo" e **reaproveitar a ideia como oferenda de boss**: a oferenda é uma "semente amaldiçoada" plantada no pilar e o boss brota dela. Combina com fazendeiro e já usa algo que existe.

## M — Multiplayer

### M01 🔴 Decidir agora
- Público de jogos tipo Muck/Terraria joga muito em grupo. Retrofitar é caríssimo.
- Se "sim no futuro": nada de `Engine.time_scale` (a câmera lenta da entrada de boss quebra), estado num lugar só, mundo por seed, inimigos miram "jogador mais próximo", decidir roleta por jogador ou compartilhada, vida de boss escalando com jogadores.

### M02 🔴 Prompts do Ziva
- Se M01 = sim, todo prompt novo ganha uma seção de regras de multiplayer.

## T — Técnico

### T01 ✅ Projeto Godot no GitHub.
### T02 🔴 Subir cópias dos prompts antigos para `prompts/`.
