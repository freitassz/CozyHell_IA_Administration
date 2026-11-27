# PROMPT ZIVA — Lote 2A: HUD intuitivo, ícones de itens, inventário com descrições e crafting claro

## Contexto
Playtest: o HUD não é intuitivo (não dá para saber o que é o dinheiro), os itens não têm imagem e faltam descrições. Regra de ouro do Gustavo: **comunicar por forma, cor e ícone, não por texto.** Placeholders visuais agora; o Gustavo faz arte depois.
- Modo rápido: tudo de uma vez, com **validador** e **cena de prévia**. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.

## ETAPA 0 — Relatório curto
Lista dos itens do jogo (ids, categoria, se têm ícone/malha), onde ficam HUD, inventário e crafting, e como as receitas são mostradas hoje.

## 1. Ícones automáticos de itens
- `IconeItem`: gera o ícone de **cada item** (cache): se o item tem malha/cena de mundo, renderiza num `SubViewport` 64×64 com fundo transparente, câmera 3/4 e luz suave; senão, um **placeholder** = forma da categoria (arma, ferramenta, armadura, recurso, comida/drop, minério, ficha, material de boss) na cor do item. Moldura colorida pela **raridade** (comum `#3DDC4A`, raro `#2F8BFF`, épico `#A23DFF`, lendário `#FFD21F`; itens sem raridade, cinza).
- Todo lugar que mostra item (hotbar, mochila, baú, crafting, NPCs, Trader, Andarilho, máquinas) usa `IconeItem`.

## 2. HUD de jogo (sem texto onde der)
- **Canto superior esquerdo:** **vida** = barra vermelha com ícone de coração; **Essência** = barra lilás com ícone de gota; **stamina** = barra fina verde-amarela, só visível quando não está cheia. Números pequenos dentro/ao lado só da vida.
- **Defesa:** ícone de **escudo** + número, só se > 0; ao lado, ícone do conjunto completo (sem texto "Conjunto: Ferro ✓").
- **Dinheiro e sucata:** linha com **moeda dourada** + número (R$) e **engrenagem cinza** + número (sucata), sempre no mesmo lugar; um **pulso** e "+N" flutuante curto no HUD (não no mundo) quando ganha.
- **Dia/hora:** ícone de **sol/lua** + hora, junto ao minimapa. **Clima/estados** (chuva, Queimar, Soneca/Pesadelo) = ícones pequenos ao lado.
- **Hotbar:** ícones + quantidade em número; slot selecionado com destaque; **nome do item selecionado** aparece ⚙️ 1,5 s acima da hotbar e some.
- **Mensagens de sistema** (liberações etc.) continuam, pequenas, centro-superior, ⚙️ 3 s. Remova o texto grande de debug que cobre a tela.

## 3. Inventário
- Grade de ícones (hotbar, mochila, armaduras, acessórios, baú). **Passar o mouse mostra um painel**: nome, **raridade (cor)**, **descrição curta**, quantidade, e por categoria:
  - **Armadura:** defesa da peça (%), defesa total do conjunto equipado, **bônus de conjunto** e quantas peças faltam; compara com a peça equipada (verde/vermelho).
  - **Arma:** nível (nvN), dano, cadência, pente, custo de Essência da recarga, especial (nome).
  - **Ferramenta:** nível e velocidade; **minério/material:** para que serve (1 linha).
  - **Acessório:** bônus por unidade e quantas empilhadas/limite.
- **Descrições:** campo `descricao` (PT, 1–2 linhas) em **todos** os itens. Gere descrições provisórias coerentes com o jogo em `res://resources/itens_descricoes.json` (editável pelo Gustavo, sem mexer em código); itens sem entrada mostram só o nome.

## 4. Crafting claro
- Abas por **estação** (Bancada, Bigorna, Fornalha) com ícone; lista de receitas: **ícone do resultado** à esquerda, **ingredientes como ícones** com "tem/precisa" (ex.: 8/10) **verde se tem, vermelho se falta**; botão Fabricar cinza se faltar; filtro "só o que posso fazer".
- Receitas que aceitam alternativas (ex.: "drop do Tomate ou Cenoura") mostram os ícones alternando.

## Teste
`dev/validate_hud`: todo item tem ícone, todo item tem descrição (0 faltando), tooltip de armadura com defesa e bônus, receitas com tem/precisa. E `dev/hud_preview.tscn` para o Gustavo olhar HUD, inventário e crafting na tela. Placar.

## Checklist
- [ ] `IconeItem` com moldura de raridade, usado em todo lugar · [ ] HUD com ícones (coração, gota, escudo, moeda R$, engrenagem, sol/lua)
- [ ] Inventário com painel de descrição e detalhes de armadura/arma/ferramenta · [ ] `itens_descricoes.json` para todos os itens
- [ ] Crafting com ícones e tem/precisa · [ ] Validador + prévia · Nada além disso foi alterado
