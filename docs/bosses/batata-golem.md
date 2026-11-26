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

## Visual (para o pedido de modelagem)
Batata gorda e dourada (`#D9B26F`) com manchas marrom-claras, **braços e pernas de pedra** cinza-azulada clara (`#9FB4C7`), carinha simples com olhos de broto, **brotos verdes** (`#6FCF5A`) nas costas, raízes finas saindo dos pés. ~6 m, facetado, fosco, nada perto do preto. Animações: `Idle`, `Andar`, `Virar`, `Pisao`, `Soco_Martelo`, `Giro`, `Arremesso`, `Brotos_Quebrados`/`Desmoronar` (+ loop caído), `Levantar`, `Fase2`, `Morte`.

## Perguntas
1. Gostou da ideia (pontos fracos nas costas + dar a volta)? Se não, corto ou proponho outra.
2. Nome/subtítulo e as cores ok?
