# PROMPT ZIVA — Lote 3A: árvores que caem, pedras e arbustos que quebram, drops com forma

## Contexto
Playtest: as árvores têm pouca copa e deixam **cepo**; pedras e arbustos somem sem graça; os drops no chão são **blocos amarelos** sem sentido. Placeholders agora (o Gustavo faz modelos depois). **Desempenho importa** (o notebook dele é fraco): use pools, partículas curtas e `MultiMesh` quando der.
- Modo rápido, com validador. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim (`@export`).
- Multiplayer: efeitos derivam da direção do golpe e do estado do recurso (que já é do mundo); nada de `Engine.time_scale`.

## ETAPA 0 — Relatório curto
Como árvores/pedras/arbustos/minérios são criados e destruídos hoje (cenas, vida, drop, cepo), e como o item no chão (`ground_collectible`/`dropped_item_pickup`) é desenhado.

## 1. Árvores
- **Copa maior sem engrossar o tronco:** escala só da folhagem ⚙️ ×1,5 (largura e altura), tronco igual; ajuste a colisão da copa para não bloquear andar por baixo (colisão só no tronco).
- **A cada golpe:** balanço curto (⚙️ 0,25 s, mais forte ao longe da base) + algumas folhas soltando (partículas de folha low-poly, **sem cubos**, pool).
- **Ao quebrar (vida 0): a árvore CAI** para a direção **do golpe** (oposta ao jogador): o tronco gira em torno da base ~90° em ⚙️ 1,3 s com aceleração (ease-in), **bate no chão** com poeira, tremida leve (mais forte perto) e folhas esparramadas. Desligue a colisão da árvore ao começar a cair.
- O drop (madeira) **sai do tronco caído**; o tronco encolhe e some em ⚙️ 3 s. **Sem cepo** (remova o toco); o ponto fica limpo.
- Continua valendo: ID = tipo + posição, renasce em 3 dias, nada renasce perto de construção.

## 2. Pedras e minérios
- A cada golpe: tremida curta + **lascas** (pool). Em **66%** e **33%** da vida a pedra **perde um pedaço** (troca para uma escala menor ⚙️ 0,85 / 0,7 e solta uma lasca grande).
- Ao quebrar: **3–4 fragmentos** que rolam e encolhem em ⚙️ 1 s + poeira; o drop sai no meio. Veios de minério: igual + **brilho** na cor do minério (Ferro cinza-azul, Cobre laranja, Ouro amarelo, Cristal lilás).

## 3. Arbustos
- A cada golpe: balanço. Ao quebrar: **puf de folhas** (partículas) e o arbusto **murcha/encolhe** em ⚙️ 0,4 s. Cores seguem o arbusto.

## 4. Drops no chão com forma (#3)
- Troque os blocos amarelos por **`DropVisual`**: uma **forma por categoria** (reaproveite o gerador de placeholders do `IconeItem` do Lote 2A se já existir; senão crie `FormaItem` e faça o `IconeItem` usá-lo):
  madeira = tora curta · pedra = rochinha · minério = rochinha na cor do minério · Tomate = esfera vermelha · Cenoura = cone laranja · Pimentão = alongado vermelho · Cebola = bulbo · Milho = espiga · ficha = disco na cor da raridade · material de boss = forma própria na cor do boss · arma/ferramenta/armadura = silhueta da categoria.
- Cada drop **gira devagar e flutua** (⚙️ 0,15 m), com **sombra** (Decal pequeno). Raridade Raro+ ganha uma **coluninha de luz fina** (⚙️ 0,7 m) na cor da raridade. Pilhas > 1 mostram 2–3 cópias menores juntas.
- **Coleta:** a ⚙️ 2 m o drop **voa até o jogador** e some com um brilho; sinal `item_coletado(item, qtd)` (para sons). Sem texto.
- Pool de drops; máximo ⚙️ 60 ativos (os mais antigos somem se passar disso).

## Teste
`dev/validate_lote3a`: copa ×1,5 e tronco igual; árvore cai na direção do golpe (oposta ao jogador), sem cepo; pedra perde pedaços em 66/33% e quebra em fragmentos; arbusto encolhe; drops com forma por categoria, coluna de luz em Raro+, coleta por atração, limite de 60. E `dev/natureza_preview.tscn` para ver tudo na tela. Placar.

## Checklist
- [ ] Copa ×1,5 sem engrossar o tronco · [ ] Queda na direção do golpe, sem cepo · [ ] Pedras com estágios e fragmentos · [ ] Arbustos com puf
- [ ] `DropVisual` por categoria, luz por raridade, coleta por atração · [ ] Validador + prévia · Nada além disso foi alterado
