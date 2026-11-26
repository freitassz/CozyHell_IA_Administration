# PROMPT ZIVA — Andarilho (comerciante que aparece perto do jogador)

## Contexto
Um NPC itinerante que **chega do nada perto de você**, fica um tempo e vai embora. Usa o `NpcBase` do prompt anterior (`PROMPT_ZIVA_NPCS_GUIA_TRADER`) — **aplique aquele primeiro**. Placeholder: bloco com chapéu e uma mochila grande.
- Modo rápido, com validador. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim. Estado no **save**.

## Quando aparece
- **No amanhecer** de cada dia, chance ⚙️ 25%; **garantido** se passaram ⚙️ 4 dias sem aparecer (sorteio com `world_seed + 9201 + dia`).
- Surge a ⚙️ 25–40 m do **jogador mais próximo** (jogador local hoje), no chão, fora de construções e de estruturas, com um **"puf"** de partículas (sem cubos) e uma mensagem pequena "Um andarilho apareceu por perto" + ícone piscando uma vez no minimapa.
- **Fica até ⚙️ 20h** (anoitecer) daquele dia, ou vai embora (com "puf") se ficar a mais de ⚙️ 120 m de todos os jogadores por 60 s. Só 1 por vez.

## O que ele faz (menu com E)
Estoque sorteado ao chegar (⚙️ 6 ofertas), preços em **R$**:
- **Vende armaduras:** 2 peças aleatórias dos conjuntos **Madeira a Ouro** (nunca Cristal). Preço do conjunto ⚙️ Madeira 150 · Pedra 300 · Ferro 800 · Cobre 1500 · Ouro 2500 × peso da peça (peitoral 40%, capacete 25%, calça 20%, botas 15%).
- **Vende ferramentas:** 2 machados/picaretas **até a Picareta de Ferro** (nunca vende a que abre o próximo minério) ⚙️ 150–600 R$.
- **Vende drops de monstros:** 2 pilhas de drops comuns (⚙️ 5 un.) por ⚙️ 2× o preço de venda.
- **Compra drops de monstros** (qualquer um) por ⚙️ 1,5× o preço da Barraca de Venda; aplica o **bônus +15% de R$** do conjunto de Ouro.
- Itens vendidos saem do estoque; menu simples com "Comprar"/"Vender", R$ atual e lista do estoque.

## Estado salvo
Se está presente, posição, estoque restante, dia em que chegou e contador de dias sem aparecer.

## Teste
`dev/validate_andarilho`: chance e garantia, aparece a 25–40 m, sai às 20h ou ao ficar longe, estoque sem Cristal e sem a picareta de acesso, preços, compra/venda e bônus de Ouro, save/carregar, determinístico pela seed. Placar.

## Checklist
- [ ] Aparece perto com "puf", mensagem e ícone · [ ] Dura até 20h/longe · [ ] Vende e compra como acima
- [ ] Save e seed · [ ] Validador · Nada além disso foi alterado
