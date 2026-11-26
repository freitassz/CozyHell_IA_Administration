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

## Visual detalhado (para o pedido de modelagem) — ✅ ideia aprovada pelo Gustavo, visual a avaliar
**Silhueta:** uma **batata gorda e corcunda**, com **braços e pernas de pedra** e **3 brotos verdes** crescendo nas costas. Reconhecível só pela forma.
**Tamanho:** ~6 m de altura (7,2 m com os brotos) e ~5 m de largura nos ombros (o jogador tem ~1,7 m).

| Parte | Descrição | Cores |
|---|---|---|
| **Tronco** | batata oval, larga na barriga, inclinada para a frente; facetada (~12 lados); "olhinhos" de batata como covinhas facetadas e cicatrizes onde a pedra encosta | dourado `#D9B26F`, manchas chapadas marrom-claro `#B88A4A` |
| **Rosto** | no alto do tronco: **testa de pedra** grossa (mal-humorado, mas fofo), **dois olhos grandes** redondos com pupila, **nariz de batatinha**, **boca em fenda** larga com 2 dentes quadrados de pedra | olhos creme `#F3E9C8` + pupila marrom `#6B4A2B`; pedra da testa cinza-azulada |
| **Braços** | de pedra, longos (quase tocam o chão), com **ombros redondos presos na batata como cascos** e **punhos enormes** de 3 blocos grossos; musgo claro nos ombros | pedra `#9FB4C7`, quinas mais claras `#C4D3E0`, musgo `#8FD18A` |
| **Pernas** | curtas e grossas, **pés largos de tijolo**; **raízes finas** saindo dos pés e se enterrando no chão | pedra igual; raízes bege `#EBDDB8` |
| **Costas / brotos (pontos fracos)** | **3 brotos grandes** (~1,2 m) em hastes grossas, cada um com 3 folhas largas facetadas e uma ponta brilhante; na base, um "colar" de pedra rachada que **se quebra quando o broto é destruído** | haste `#6FCF5A`, folhas `#4FA84A`, ponta `#B6F06A` (emissiva pulsando) |
| **Fase 2** | **5 brotos menores**; rachaduras no corpo com brilho verde-limão; olhos com brilho verde | `#B6F06A` |
| **Desmoronado** | pedras se soltam e rolam, batata caída de lado, raízes soltas, tocos bege no lugar dos brotos | `#EBDDB8` |

- **Estilo do jogo:** facetado, cores chapadas por vértice, **sem textura**, **fosco e sem reflexo**, nada perto do preto (só o contorno).
- **Efeitos no Godot (não no modelo):** poeira nos passos, lascas de pedra, pulso de brilho dos brotos.
- **Materiais:** `BatataCorpo`, `Pedra`, `Musgo`, `Broto`, `BrotoBrilho` (emissivo), `Raiz`, `Olho`.
- **Ossos (rig):** `Raiz > Corpo > BracoE/BracoD` (ombro, antebraço, punho), `PernaE/PernaD`, `Broto1–3` (2 segmentos, balançam), `Olhos`, `Boca`; âncoras `FX_PunhoE/D`, `FX_PeE/D`, `FX_Broto1–3`.
- **Animações:** `Idle`, `Andar`, `Virar` (lento), `Pisao`, `Soco_Martelo`, `Giro`, `Arremesso`, `Brotos_Quebrados`→`Desmoronar`+`Caido` (loop)→`Levantar`, `Fase2`, `Morte`.

## Perguntas
1. Gostou da ideia (pontos fracos nas costas + dar a volta)? Se não, corto ou proponho outra.
2. Nome/subtítulo e as cores ok?
