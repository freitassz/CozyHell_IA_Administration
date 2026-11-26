# Batata-golem — "O Tubérculo de Pedra"

- **Boss 5** da cadeia (Tomate → Uva → Dragão → Pimenta → **Batata** → Deus). Santuário na **Pedreira**.
- **Status:** 🟡 **proposta do Claude** (se o Gustavo não gostar, pode ser cortado). Modelo antigo e folha de referência foram reprovados; começa do zero.
- Progressão: 1ª oferenda **Brasa Eterna + Minério de Ferro + Lágrima de Cebola** · dropa **Ficha Épica + Raiz de Pedra** · libera **Lendário** e **ergue o santuário final**.

## Ideia central: **pontos fracos nas costas**
Os outros bosses testam pulo, mergulho, rebater e orbitar. Este testa **movimento em volta do inimigo**: ele é lento e pesado, e só se fere **nos brotos de batata das costas**.
- O corpo é pedra (dano ×0,1). Os **3 brotos verdes** nas costas levam dano normal.
- Ele **vira devagar** para ficar de frente: o jogador **dá a volta** para atingir as costas.
- Quando os **3 brotos** são destruídos, ele **desmorona** ⚙️ 5 s (dano ×2 no corpo todo = a janela) e depois levanta e os brotos **crescem de novo**.

## Ataques (avisos ≥ 1,2 s, `Decal` vermelho, áreas redondas)
| Ataque | O que faz | Para quê |
|---|---|---|
| **Pisão** | levanta a perna; ao pisar sai um **anel curto de pedras** no chão (dá para pular) | punir quem fica na frente |
| **Soco-martelo** | soca o chão na frente do jogador e levanta **3 estacas de pedra em linha** que ficam ~8 s e **bloqueiam tiros e ataques dele** | cria cobertura |
| **Giro de braços** (360°) | só quando o jogador **fica nas costas por > 3 s**: olhos brilham, círculo grande, e ele gira com os braços — dá para pular por cima ou se esconder atrás de uma estaca | impede ficar parado nas costas |
| **Arremesso de pedra** | se o jogador está **> 15 m**, atira uma pedra em arco com círculo no ponto de queda | punir quem fica longe |
- **Fase 2 (< 50%, sem texto):** 5 brotos menores no lugar de 3, ⚙️ 25% mais rápido, soco-martelo faz 5 estacas.
- Entrada: **"Batata-golem / O Tubérculo de Pedra"**, barra cor de batata `#C9A66B`. Vida ⚙️ 2800.

## Visual detalhado — v2 (ajuste do Gustavo: mais simples, mais geométrico, assimétrico, manco)
> A 1ª versão gerada em imagem ficou "cartunesca demais" (rosto pintado, cicatrizes, simétrica, 3 brotos como coroa na cabeça). **A v2 troca detalhe "desenhado" por detalhe de formas geométricas.**

**Princípios**
- **Simples de longe, detalhado de perto em formas geométricas:** tudo feito de **blocos, prismas, pirâmides e poliedros facetados**, com **chanfros, encaixes, placas e "rebites" em cubinho**. **Nada pintado** (sem cicatriz desenhada, sem sombra pintada, sem degradê): só cor chapada por face.
- **Assimétrico:** **um braço enorme** e **um braço pequeno**; **pernas curtas e desiguais** → ele anda **mancando**.
- Estilo do jogo: facetado, fosco, sem textura, nada perto do preto (só o contorno).

**Silhueta:** tronco gigante e baixo, **corcunda** inclinada para a frente, **braço direito enorme** quase no chão, **braço esquerdo curto**, **pernas curtas** (a esquerda menor), **3 brotos nascendo da corcunda das costas** (não da cabeça: ficam atrás e abaixo da linha da cabeça, para dar para acertar por trás).
**Tamanho:** ~5 m de altura (6,2 m com os brotos), ~5 m de largura (ombros). Pernas ≈ 1/5 da altura: o corpo "senta" baixo e pesado.

| Parte | Descrição (geométrica) | Cores |
|---|---|---|
| **Tronco (batata)** | oval largo montado em **grandes facetas planas** (~10 faces visíveis); **"olhos de batata" = 5–6 poços hexagonais rasos** (inset) espalhados; **3 sulcos retos** talhados (em vez de cicatrizes); uma **placa de pedra** presa no peito com 4 rebites cúbicos | `#D9B26F`; poços `#B88A4A`; placa `#9FB4C7` |
| **Rosto (5 peças)** | **sobrancelha = 1 bloco trapezoidal** de pedra; **2 olhos = octógonos creme** com **pupila quadrada**; **nariz = pirâmide pequena**; **boca = fenda reta** (caixa rebaixada) com **2 dentes quadrados**. Sem expressões desenhadas: a cara de mal-humorado vem só da sobrancelha inclinada | olhos `#F3E9C8`, pupila `#6B4A2B` |
| **Braço direito (GRANDE)** | ~3× a massa do outro, chega ao chão: **ombro = poliedro (dodecaedro) grande** preso por 2 placas; **antebraço = 3 lajes empilhadas em degraus**; **punho = 4 blocos** com **placas de "nó dos dedos"** e rebites cúbicos. **Serve de muleta**: ele apoia o punho no chão ao andar | pedra `#9FB4C7`, quinas `#C4D3E0`, musgo `#8FD18A` só em 2 blocos |
| **Braço esquerdo (CURTO)** | ~60% do comprimento e fino: **ombro pequeno + 2 blocos + mão de 3 cubos**; pende junto ao quadril, meio torto | mesma pedra |
| **Pernas (CURTAS e DESIGUAIS)** | **direita:** coxa-cubo + bota larga (trapézio); **esquerda ~60% do tamanho**, mais grossa, com **cunha de pedra** (calço) sob o pé; 3 raízes finas (prismas longos) em cada pé | pedra; calço `#C4D3E0`; raízes `#EBDDB8` |
| **Costas / brotos (pontos fracos)** | **corcunda** com **3 brotos** em hastes grossas (prismas) de ~1 m, **3 folhas triangulares** cada e **ponta em cristal verde** (poliedro, emissivo pulsando); na base, um **"colar" de 4–5 placas de pedra** que se solta quando o broto é destruído | haste `#6FCF5A`, folhas `#4FA84A`, ponta `#B6F06A` |
| **Fase 2** | 5 brotos menores; **3 fendas retas** brilhando no tronco; olhos com brilho verde | `#B6F06A` |
| **Desmoronado** | placas e blocos soltos rolando; batata caída de lado; tocos bege no lugar dos brotos | `#EBDDB8` |

**Movimento (para as animações)**
- **Andar manco:** `tum` (punho direito apoia) → `tum` (perna direita passa) → **arrasta a esquerda curta** (pausa) — ritmo lento e irregular. **Idle** com o corpo **inclinado ~8° para o lado da perna curta** e respirando devagar.
- **Virar:** pivota pesado sobre a perna direita, arrastando a esquerda. Soco-martelo/giro usam o **braço grande**; o pequeno só balança.

**Materiais:** `BatataCorpo`, `Pedra`, `Musgo`, `Broto`, `BrotoBrilho` (emissivo), `Raiz`, `Olho`.
**Ossos:** `Raiz > Corpo > BracoD` (ombro, antebraço, punho), `BracoE` (2 segmentos), `PernaD`, `PernaE`, `Broto1–3` (2 segmentos), `Olhos`, `Boca`; âncoras `FX_PunhoD`, `FX_PeD/E`, `FX_Broto1–3`.
**Animações:** `Idle`, `Andar` (manco), `Virar`, `Pisao`, `Soco_Martelo`, `Giro`, `Arremesso`, `Brotos_Quebrados`→`Desmoronar`+`Caido` (loop)→`Levantar`, `Fase2`, `Morte`.
**Efeitos no Godot:** poeira nos passos e no apoio do punho, lascas, pulso dos brotos.

## Perguntas
1. Gostou da ideia (pontos fracos nas costas + dar a volta)? Se não, corto ou proponho outra.
2. Nome/subtítulo e as cores ok?
