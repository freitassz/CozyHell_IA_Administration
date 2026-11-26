# Batata-golem — "O Tubérculo de Pedra"

- Era o boss 5 da cadeia (Tomate → Uva → Dragão → Pimenta → **Batata** → Deus). Santuário na Pedreira.
- **Status:** ❌ **CORTADO do jogo** (nov/2026: "não está fluindo"). Mantido aqui só como arquivo. A ideia dos **pontos fracos nas costas / dar a volta no inimigo** pode ser reaproveitada em outro boss.
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

## Visual — v3 (segue o **desenho do Gustavo**; anexar o desenho como referência no pedido de modelagem)
> Ainda mais simples que a v2: o desenho manda. Formas **geométricas facetadas**, cor chapada, nada pintado.

**O que o desenho mostra**
- **Corpo:** uma batata **muito irregular e quadradona**, quase tão larga quanto alta, cheia de **calombos** (um nos cantos de cima, outro na lateral), sem pescoço nem cabeça separada.
- **Braço grande:** pende de um lado como uma **clava/presunto**: **fino no ombro e bem grosso embaixo (o punho)**, e **passa da base do corpo, chegando ao chão**.
- **Bracinho:** do outro lado, **curto e fino**, só pende até a altura da cintura, com a pontinha arredondada.
- **Pernas:** **dois tocos minúsculos** embaixo, curtos e estreitos, quase sem perna — o corpo fica **rente ao chão**. (Para o manco: uma é **um pouco mais curta** que a outra.)
- **Rosto:** **dois olhos chatos e largos** (retângulos de cantos arredondados, olhar cansado) sob **uma sobrancelha grossa e inclinada** que cruza os dois (cara de mal-humorado); **boca = uma linha reta curta**. Nada de nariz nem dentes.
- **Brotos:** as **pontas dos brotos aparecem nos cantos de cima**; eles **nascem nas costas** (corcunda), 3 no total.

**Tradução para o modelo**
| Parte | Descrição (geométrica) | Cores |
|---|---|---|
| **Corpo** | bloco-batata de **grandes facetas planas e irregulares** (~8–10 faces), **2–3 calombos** como poliedros colados; **3 sulcos retos** e **4 poços hexagonais rasos** como únicos detalhes | `#D9B26F`; poços/sulcos `#B88A4A` |
| **Rosto (3 peças)** | **2 placas largas de cantos chanfrados** (olhos, creme) + **1 laje de sobrancelha** inclinada cobrindo as duas + **1 caixa rebaixada** fina (boca). Pupila = um quadradinho em cada olho (opcional) | olhos `#F3E9C8`, pupila `#6B4A2B`, sobrancelha pedra `#9FB4C7` |
| **Braço grande** | **ombro estreito** que **engrossa em degraus**: 3 lajes empilhadas cada vez maiores até um **punho-bloco enorme** (3–4 blocos), com 2–3 placas e rebites cúbicos; chega ao chão (**vira muleta**) | pedra `#9FB4C7`, quinas `#C4D3E0`, musgo `#8FD18A` em 1–2 blocos |
| **Bracinho** | **2 blocos finos + uma mão de 2–3 cubinhos**, pendendo torto | mesma pedra |
| **Pernas** | **2 tocos** de bloco (um mais curto, com **cunha** sob o pé), 2–3 raízes finas em cada | pedra; raízes `#EBDDB8` |
| **Brotos** | 3 hastes de prisma saindo da **corcunda**, 3 folhas triangulares cada, **ponta em cristal verde** (emissivo pulsando); na base, **colar de 4–5 placas** que se solta ao quebrar | haste `#6FCF5A`, folhas `#4FA84A`, ponta `#B6F06A` |
| **Fase 2** | 5 brotos menores + 3 fendas retas brilhando no corpo | `#B6F06A` |
| **Desmoronado** | blocos soltos, batata caída, tocos bege no lugar dos brotos | `#EBDDB8` |

**Proporções:** corpo ~4,5 m de largura × ~4 m de altura; braço grande ~5 m (toca o chão) com punho de ~1,8 m; bracinho ~1,5 m; pernas ~0,8 m; **total ~5 m** (6 m com os brotos).
**Movimento:** **andar manco** (punho grande apoia, perna passa, arrasta a curta, pausa); parado, **inclinado ~8°** para o lado da perna curta. Ataques fortes usam o **braço grande**; o bracinho só balança.
**Materiais:** `BatataCorpo`, `Pedra`, `Musgo`, `Broto`, `BrotoBrilho` (emissivo), `Raiz`, `Olho`.
**Ossos:** `Raiz > Corpo > BracoGrande` (ombro, antebraço, punho), `BracoPequeno`, `PernaD`, `PernaE`, `Broto1–3` (2 segmentos), `Olhos`; âncoras `FX_Punho`, `FX_PeD/E`, `FX_Broto1–3`.
**Animações:** `Idle`, `Andar` (manco), `Virar`, `Pisao`, `Soco_Martelo`, `Giro`, `Arremesso`, `Brotos_Quebrados`→`Desmoronar`+`Caido`(loop)→`Levantar`, `Fase2`, `Morte`.
**Efeitos no Godot:** poeira nos passos e no apoio do punho, lascas, pulso dos brotos.

## Perguntas
1. Gostou da ideia (pontos fracos nas costas + dar a volta)? Se não, corto ou proponho outra.
2. Nome/subtítulo e as cores ok?
