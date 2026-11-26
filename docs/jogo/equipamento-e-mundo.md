# Minérios, armaduras, NPCs e estruturas do mundo — proposta v1

> Status: 🟡 proposta do Claude (nov/2026) para aprovar/ajustar. Depois vira **2 prompts do Ziva**: (1) minérios + picaretas + fornalha + armaduras; (2) estruturas + NPCs.
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

## 3. Estruturas geradas no mundo (pela seed)
| Estrutura | Onde | O que tem | Modelo |
|---|---|---|---|
| **Casa abandonada** | Planície / Floresta | 1–2 **baús** com recursos, drops, R$; chance pequena de ficha Rara; ao abrir, uma **mini-horda** | `House` (já existe) |
| **Celeiro assombrado** | Floresta | horda maior ao entrar; **baú melhor**: acessório ou ficha | `House` ampliada (provisório) |
| **Mina abandonada** | Pedreira | entrada (`hole`) + **veios concentrados** de minério + inimigos + baú | `hole` + pedras (já existem) |
- Já existem e continuam: **Monumento** (pilar de inimigos), **santuários**, **caça-níquel** de armas e de acessórios, vacas-melancia.
- Quantidade e distância pela seed (⚙️ ~4 casas, 2 celeiros, 2 minas por mapa). **Saque do baú** salvo no save (como os outros baús).

## 4. NPCs (parados no mundo, por seed)
| NPC | Onde | O que faz |
|---|---|---|
| **Espantalho Trocador** | Planície, perto do spawn | troca itens por **fichas** de raridade (⚙️ 15 drops comuns + 50 R$ = Ficha Rara; só raridades já liberadas). É o "NPC das fichas" que o Gustavo aprovou |
| **Andarilho** | aparece num ponto da Floresta a cada ⚙️ 3 dias, fica 1 dia | **vende** peças de armadura e acessórios aleatórios por R$ (estoque muda a cada visita) |
- Diálogo mínimo: 1 frase + menu de troca/compra (sem texto longo). Modelo provisório (bloco/espantalho simples) até haver arte.

## Ordem de prompts do Ziva
1. **Minérios, picaretas, Fornalha, armaduras** (inclui bônus de conjunto e Cristal Lapidado).
2. **Estruturas e NPCs** (usa os baús e o save que já existem).

## Para decidir (se não responder, eu assumo as propostas)
1. Os 4 minérios (Ferro, Cobre, Ouro, Cristal do Sonho) e a regra "picareta pede drops da fase" estão bons?
2. Armaduras: totais por conjunto (15 → 75%) e os bônus de conjunto ok?
3. As 3 estruturas e os 2 NPCs ok? Cortar ou trocar alguma?
