# Minérios, armaduras, NPCs e estruturas do mundo — proposta v1

> Status: ✅ **no jogo** (validadores 79/79, 84/84 e 51/51; visual ainda não conferido na tela). Aprovado pelo Gustavo (nov/2026). **3 prompts do Ziva:** [minérios+armaduras](../../prompts/mundo/PROMPT_ZIVA_MINERIOS_ARMADURAS.md) → [NPCs: Guia + Trader](../../prompts/mundo/PROMPT_ZIVA_NPCS_GUIA_TRADER.md) → [Andarilho](../../prompts/mundo/PROMPT_ZIVA_ANDARILHO.md). Placeholders agora; modelos depois (Gustavo).
> Hoje: 1 minério (Ferro); armaduras de Madeira/Pedra/Ferro (4 peças cada) com 5/10/16% **por peça**; 5 acessórios; estações Bancada, Bigorna, Fornalha, Baú, Cama, Fogueira.

## 1. Minérios (4) e picaretas — ganham propósito
Todos existem no mundo **desde o início** (Pedreira; os raros mais fundo/espalhados). **O que trava é a picareta**, que pede drops de inimigos de fases mais avançadas (ideia do Gustavo).
| Minério | Cor | Picareta necessária | Receita da picareta | Vira |
|---|---|---|---|---|
| **Ferro** (existe) | cinza-azul | Picareta de Pedra (início) | madeira + pedra | Barra de Ferro (Fornalha) |
| **Cobre** | laranja | Picareta de Ferro | barras de Ferro + drops da **fase 1** | Barra de Cobre |
| **Ouro** | amarelo (modelo `GoldStone` já existe) | Picareta de Cobre | barras de Cobre + drops da **fase 2** | Barra de Ouro |
| **Cristal do Sonho** | lilás `#B98CFF` | Picareta de Ouro | barras de Ouro + **Brasa Eterna** (boss Pimenta) *(troque pelo drop da fase 3 quando existir)* | Cristal Lapidado (Bancada; não funde) |
- Cada picareta também é mais **rápida** que a anterior.
- Minérios **renascem** como os outros recursos (3 dias).
- **Usos:** armaduras (principal), picaretas, e alguns itens. **Cristal do Sonho** também é o recurso das **receitas mágicas** futuras (ideia guardada).

## 2. Armaduras (4 peças: capacete, peitoral, calça, botas)
Conjunto completo reduz o dano total de ⚙️: **Madeira 15% · Pedra 30% · Ferro 45% · Cobre 55% · Ouro 65% · Cristal 75% (teto)**. Por peça: peitoral 40% do total, capacete 25%, calça 20%, botas 15%. (Substitui o 5/10/16% por peça de hoje.)
| Conjunto | Material | Onde se faz | **Bônus de conjunto (4 peças)** ⚙️ |
|---|---|---|---|
| Madeira / Pedra | madeira / pedra | Bancada | — |
| Ferro | 24 barras | Bigorna | +10% de vida máxima |
| Cobre | 24 barras | Bigorna | +6% de velocidade |
| Ouro | 24 barras | Bigorna | +15% de R$ ao vender |
| Cristal | Cristal Lapidado + barras de Ouro | Bigorna | **+25% de regeneração de Essência** |
- **Sem modelos 3D por enquanto:** na primeira pessoa não se vê a armadura; só ícones e a **Defesa** no HUD. (Visual só no multiplayer, no futuro.)
- Armaduras de boss (com Brasa Eterna, Escama de Pitaya etc.): **futuro**, junto com as armas exclusivas de boss.

## 3. Estruturas e NPCs — ✅ definidos pelo Gustavo
| NPC / estrutura | Onde | O que faz |
|---|---|---|
| **Guia dos Sonhos** (cabana) | **perto do spawn** | todas as **dicas** do jogo (como o Guia do Terraria): "o que fazer agora" dinâmico + tópicos |
| **Trader** (tenda) | Planície, 150–250 m do spawn | a cada **2 dias** (ciclo do jogo) oferece **2 trocas diferentes** de **materiais por fichas** das raridades já liberadas, sorteadas |
| **Andarilho** | **chega do nada perto do jogador** | vende/compra **armaduras, ferramentas e drops de monstros** por R$; fica até o anoitecer |
- ❌ Casa abandonada, celeiro assombrado e mina abandonada: **adiados** (não eram o que o Gustavo queria dizer com "estruturas").
- Já existem: Monumento, santuários, caça-níquel (armas e acessórios), vacas-melancia.

## Ordem de prompts do Ziva
1. **Minérios, picaretas, Fornalha, armaduras**.
2. **NPCs: base + Guia dos Sonhos + Trader**.
3. **Andarilho** (depois do 2).

## Para decidir (se não responder, eu assumo as propostas)
1. Os 4 minérios (Ferro, Cobre, Ouro, Cristal do Sonho) e a regra "picareta pede drops da fase" estão bons?
2. Armaduras: totais por conjunto (15 → 75%) e os bônus de conjunto ok?
3. As 3 estruturas e os 2 NPCs ok? Cortar ou trocar alguma?

## Como ficou (Ziva, nov/2026)
- **Minérios:** nível mínimo de picareta 1/2/3/4 (Ferro/Cobre/Ouro/Cristal); sem picareta suficiente nada cai ("Precisa de uma picareta melhor"). **Ferro agora também exige picareta** (antes dava com a mão). Pedreira: 40 Ferro, 24 Cobre, 8 Ouro, 4 Cristal; Planície/Floresta só Ferro e Cobre (15%).
- **Picaretas** velocidade 1,0/1,4/1,8/2,2×, todas na Bancada. Fornalha funde Cobre e Ouro (continua gastando 1 combustível a cada 15 s). Cristal Lapidado = 3 Cristais.
- **Armaduras:** 24 peças, teto 75%, bônus de conjunto (HUD mostra "Conjunto: Ferro ✓"). Madeira e Pedra não pedem mais Fibra.
- **Guia dos Sonhos:** cabana a 30–45 m do spawn; dicas em `resources/guia/dicas.json`.
- **Trader:** tenda na Planície; sem ficha liberada (antes do Tomate) não há trocas. Não filtra minérios por picareta (só por fase).
- **Andarilho Itinerante:** vende Machado (150), Picareta (250), Machado de Ferro (450); **não** vende a Picareta de Ferro (abre o Cobre).
- ⚠️ Mundos salvos antes dessa mudança podem ter recursos em posições diferentes (a ordem do sorteio mudou): **prefira um mundo novo**.
- ⚠️ O NPC do Trader aparece como "Andarilho" e o outro como "Andarilho Itinerante": **renomear o Trader** (ver revisão).
