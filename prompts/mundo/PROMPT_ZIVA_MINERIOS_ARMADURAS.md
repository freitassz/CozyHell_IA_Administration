# PROMPT ZIVA — Minérios novos, picaretas, Fornalha e armaduras (6 conjuntos com bônus)

## Contexto
Hoje só existe o minério de **Ferro**. Vamos ter 4 minérios no mundo (Pedreira e pelo mundo), picaretas por nível que travam o acesso, e armaduras com bônus de conjunto. **Use placeholders** (formas simples, cores fortes, fosco; o Gustavo faz os modelos depois).
- Modo rápido: tudo de uma vez, com **validador**. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim (tudo em `@export`/Resource).
- Tudo que tem estado vai para o **save**. Recursos seguem a regra do mapa: **ID = tipo + posição (0,1 m)**, renascem em 3 dias, **pela seed**.

## ETAPA 0 — Relatório curto (siga se não houver bloqueio)
Como funcionam hoje: `resource_node` e as tabelas de bioma (`resources/biomes`), Picareta e Picareta de Ferro, a Fornalha, as armaduras existentes (como a Defesa é calculada, slots) e o `GoldStone`/`Stone` (modelos).

## ETAPA 1 — Itens e minérios
| Minério (bruto) | Barra/forma | Cor placeholder | Nível mínimo da picareta |
|---|---|---|---|
| Minério de **Ferro** (existe) | Barra de Ferro (Fornalha) | cinza-azul | 1 |
| Minério de **Cobre** (novo) | Barra de Cobre (Fornalha) | laranja `#E58A3A` | 2 |
| Minério de **Ouro** (novo) | Barra de Ouro (Fornalha) | amarelo `#F2C94C` (use o `GoldStone`) | 3 |
| **Cristal do Sonho** (novo) | **Cristal Lapidado** (Bancada: 3 Cristais do Sonho → 1 Lapidado; **não funde**) | lilás `#B98CFF` | 4 |
- Veios como `resource_node` com **nível mínimo**; bater com picareta fraca: **nada cai**, mensagem curta "Precisa de uma picareta melhor" + som de tonk.
- **Onde nascem (pela seed, tabelas de bioma):** Pedreira (principal): Ferro comum, Cobre médio, Ouro raro (veios menores e mais fundos/afastados), Cristal muito raro ⚙️. Fora da Pedreira só **pouco**: Ferro e Cobre em Planície/Floresta (⚙️ 15% da densidade da Pedreira), Ouro e Cristal **só** na Pedreira. Renascem em 3 dias como os demais recursos.
- Cada minério solta ⚙️ 1–2 unidades por veio.

## ETAPA 2 — Picaretas por nível (travam o acesso)
| Picareta | Nível | Velocidade | Receita (onde) |
|---|---|---|---|
| Picareta (existente) | 1 | 1,0× | já existe |
| Picareta de Ferro (existente: **troque a receita**) | 2 | 1,4× | 10 Barras de Ferro + 4 do drop do Tomate + 4 do drop da Cenoura + 4 do drop do Pimentão (Bancada) |
| **Picareta de Cobre** (nova) | 3 | 1,8× | 10 Barras de Cobre + 6 Lágrimas de Cebola + 6 do drop do Milho (Bancada) |
| **Picareta de Ouro** (nova) | 4 | 2,2× | 10 Barras de Ouro + 2 Brasa Eterna (Bancada) |
- Troque as receitas antigas sem perder picaretas que o jogador já tenha (save). Minérios novos só são coletáveis com o nível certo.

## ETAPA 3 — Fornalha
- Passa a fundir Minério de Cobre e Minério de Ouro em Barras (⚙️ 1 minério + 1 carvão → 1 barra, mesmo tempo do Ferro). Cristal do Sonho **não** entra na Fornalha.

## ETAPA 4 — Armaduras (6 conjuntos × 4 peças = 24)
Redução total com o **conjunto completo** (⚙️): **Madeira 15% · Pedra 30% · Ferro 45% · Cobre 55% · Ouro 65% · Cristal 75% (teto)**. Peso por peça: **peitoral 40% · capacete 25% · calça 20% · botas 15%** do total do conjunto (ex.: peitoral de Ferro = 18%).
| Conjunto | Material (conjunto) | Onde se faz | **Bônus de conjunto (4 peças)** ⚙️ |
|---|---|---|---|
| Madeira / Pedra | madeira / pedra | Bancada | — |
| Ferro | 24 Barras de Ferro | Bigorna | +10% de **vida máxima** |
| Cobre | 24 Barras de Cobre | Bigorna | +6% de **velocidade** |
| Ouro | 24 Barras de Ouro | Bigorna | +15% de **R$ ao vender** (Barraca de Venda e NPCs) |
| Cristal | 8 Cristais Lapidados + 16 Barras de Ouro | Bigorna | +25% de **regeneração de Essência** |
- Os conjuntos de Madeira/Pedra/Ferro **já existem**: ajuste os números para estes totais e converta armaduras já equipadas/no inventário.
- A **Defesa** do HUD soma as peças equipadas (teto 75%) e mostra um ícone/linha "Conjunto: <nome> ✓" quando completo.
- Receita por peça = material do conjunto × peso da peça. Ícones placeholder (cor do material). **Sem modelo 3D** (invisível em 1ª pessoa).
- Os bônus se aplicam e saem ao equipar/desequipar; salvos junto do equipamento.

## ETAPA 5 — Teste
`dev/validate_minerios_armaduras`: nível mínimo bloqueia/solta, picareta por nível, Fornalha (Cobre/Ouro) e Cristal Lapidado, receitas (incluindo drops de fase), defesa por peça e por conjunto (teto 75%), cada bônus de conjunto, minério pela seed (mesma seed = mesmos veios), renasce em 3 dias, save/carregar. Placar.

## Checklist
- [ ] 3 minérios novos nos biomas (Pedreira + pouco fora), nível mínimo, mensagem de picareta fraca
- [ ] Picaretas Cobre e Ouro; receitas novas (com drops de fase/Brasa Eterna)
- [ ] Fornalha Cobre/Ouro; Cristal Lapidado na Bancada
- [ ] 24 peças de armadura, totais por conjunto, teto 75%, bônus de conjunto · [ ] Save/seed/renascimento · [ ] Validador · Nada além disso foi alterado
