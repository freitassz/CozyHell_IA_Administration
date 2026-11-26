# PROMPT ZIVA — NPCs: base de NPC + Guia dos Sonhos + Trader (estruturas pela seed)

## Contexto
Primeiros NPCs do jogo, cada um numa pequena **estrutura** colocada pela seed: o **Guia dos Sonhos** (perto do spawn, dicas como o Guia do Terraria) e o **Trader** (troca materiais por **fichas**). **Placeholders** (blocos simples, cores fortes, fosco); o Gustavo faz os modelos depois.
- Modo rápido, com validador. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.
- Estado no **save**. Mesma seed = mesmos lugares. Multiplayer: NPC é do mundo (compartilhado); interação por jogador.

## ETAPA 1 — Base de NPC
- `NpcBase` interagível: **E** abre um menu; nome flutuando acima; balanço leve; reaproveite o sistema de interação das estações. Menu simples (1 frase + botões). Fechar com ESC/E.

## ETAPA 2 — Guia dos Sonhos
- **Estrutura:** cabana pequena (⚙️ blocos simples; pode reaproveitar `House`) a ⚙️ 25–45 m do spawn, em terreno plano, **não em cima do spawn**.
- **Menu:** (a) **"O que fazer agora?"** — texto dinâmico pelo estado do `ProgressionManager`; (b) **Tópicos** (lista clicável).
- Conteúdo em arquivo editável `res://resources/guia/dicas.json` (textos curtos em português). Estado → dica:
  - nenhum boss: "O Tomate Gigante espera na Planície. No santuário, ofereça: drop do Tomate, da Cenoura e do Pimentão."
  - Tomate derrotado: Uva → Floresta, oferenda "Casca do Tomate + drop da Cenoura + drop do Pimentão".
  - Uva derrotada: Dragão-Pitaya → Planície (área aberta), "Semente de Uva Sombria + Lágrima de Cebola + drop do Milho".
  - Dragão derrotado: Pimenta Ardente → Floresta (clareira), "Escama de Pitaya + Molho de Pimenta + Lágrima de Cebola".
  - Pimenta derrotada: o santuário final se ergueu no centro do mapa (oferenda "Brasa Eterna + Escama de Pitaya + Semente de Uva Sombria"; o boss ainda não existe).
  - Genéricas: reinvocar boss = 3 drops comuns; ficha = giro garantido na máquina.
- **Tópicos** (cada um 2–4 linhas): Controles (esquerdo atira/golpeia, direito mira, R recarrega, F especial, V golpe rápido, Q solta item) · Essência do Sonho (enche com tiros e socos, gasta em recarga e especial) · Máquina caça-níquel e Fundir/Desmanchar na bigorna · Minérios e picaretas (Ferro → picareta inicial; Cobre → Picareta de Ferro; Ouro → Picareta de Cobre; Cristal do Sonho → Picareta de Ouro) · Armaduras e bônus de conjunto · Cama e salvar · Noite e hordas · Modos Soneca/Pesadelo · Barraca de Venda · O Trader e o Andarilho.
- Sem texto de fase de boss; só no menu do Guia.

## ETAPA 3 — Trader
- **Estrutura:** tenda/barraca placeholder na **Planície**, a ⚙️ 150–250 m do spawn, plana, **1 por mundo** ⚙️.
- **Ciclo de 2 dias do jogo:** `ciclo = floor((dia-1)/2)`. A cada novo ciclo (no amanhecer) o Trader oferece **2 trocas diferentes**, sorteadas com `world_seed + 9001 + ciclo` (determinístico). Cada troca: **pedir materiais → 1 ficha**; pode ser feita **1 vez** por ciclo.
- **Ficha da troca:** só de raridades **já liberadas** pela progressão (Rara, Épica ou Lendária), pesos ⚙️ 60/30/10 limitados às liberadas; as 2 trocas devem ser **diferentes** (raridade ou custo) quando possível.
- **Custo (2–3 tipos de material, quantidades ⚙️)**, sorteado de um pool que o jogador **já consegue ter**:
  | Ficha | Pool de materiais | Quantidade total |
  |---|---|---|
  | Rara | drops comuns da fase 1 (Tomate, Cenoura, Pimentão), Madeira, Pedra, Barras de Ferro | ~20 itens |
  | Épica | Barras de Cobre/Ouro, drops da fase 2 (Cebola, Milho), Cristal do Sonho (bruto) | ~14 itens |
  | Lendária | Cristal Lapidado, Barras de Ouro | ~10 itens |
  (se um item do pool ainda não é obtível — fase/minério/picareta não alcançados — não entra no sorteio.)
- **Menu:** mostra as 2 trocas (ícones + quantidades), botão **Trocar** (cinza se faltar material), contagem "novas trocas em <tempo>". Troca feita fica marcada "Feita".
- Estado salvo: ciclo atual, trocas e quais já foram feitas.

## ETAPA 4 — Teste
`dev/validate_npcs`: Guia (dica certa em cada estado de progressão; abre tópicos), estruturas pela seed (distâncias, planas, mesma seed = mesmo lugar), Trader (2 trocas diferentes, determinístico por ciclo, só raridades liberadas e materiais obtíveis, 1 vez por troca, renova no ciclo novo, save/carregar). Placar.

## Checklist
- [ ] `NpcBase` com menu · [ ] Guia: estrutura perto do spawn, dicas dinâmicas, tópicos, `dicas.json`
- [ ] Trader: estrutura na Planície, ciclo de 2 dias, 2 trocas, fichas das raridades liberadas, 1 vez por troca
- [ ] Save e seed · [ ] Validador · Nada além disso foi alterado
