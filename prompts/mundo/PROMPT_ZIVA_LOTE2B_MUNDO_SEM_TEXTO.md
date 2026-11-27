# PROMPT ZIVA — Lote 2B: tirar textos do mundo, caça-níquel escuro, auras dos santuários, bug da cama

## Contexto
Playtest: textos flutuando sobre as coisas poluem; o caça-níquel mostra os itens antes de ativar; os santuários não se distinguem; apareceu um texto gigante "Cama (recarregando…)" cobrindo a tela. Tudo deve ser **óbvio sem escrever na tela**.
- Modo rápido, com validador. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.

## 1. Sem textos sobre as coisas
- Remova **todos os `Label3D`/textos flutuantes** acima de: estações (Bancada, Bigorna, Fornalha, Baú, Cama, Fogueira, Barraca de Venda), máquinas caça-níquel, santuários, monumentos ("Acordar Inimigos [E]"), NPCs (nome e "[E] Falar com …"), portas/estruturas. Mantenha só os de **debug** (modo criativo F3).
- No lugar: ao **olhar a ≤ ⚙️ 3 m** de algo interagível, aparece **um ícone pequeno de interação** no centro-baixo da mira: círculo com a tecla **E** e, ao lado, o **ícone do tipo** (engrenagem=estação, moeda=compra/venda, balão=NPC, cama, baú…). O preço/custo aparece como **moeda + número** (ex.: caça-níquel 🪙 25). O detalhe fica no **menu** que abre.
- **Bug "Cama (recarregando…)":** esse texto gigante some; o recarregar da cama vira um **anel de progresso** pequeno no ícone de interação (cinza enquanto recarrega).
- Nome de NPC: sem texto; cada NPC se distingue pela **forma/cor** (placeholder) e por um **ícone flutuante discreto** (Guia = "?", Trader = fichas, Andarilho = mochila) que só aparece perto.

## 2. Caça-níquel escuro
- A **tela** do caça-níquel (material `TelaRoleta`) fica **totalmente escura** (⚙️ `#10131C`, fosca) em repouso: **sem ícones, X, "?" nem glifo**. Ao ativar: a roleta aparece girando; ao terminar mostra o item; depois de ⚙️ 3 s apaga de novo (fade 0,3 s). Vale para a máquina de armas e a de acessórios.

## 3. Auras dos santuários (boss reconhecível de longe)
- Cada santuário ganha uma **aura** em vez de depender da estátua: **coluna de luz translúcida** (⚙️ 14 m de altura, raio 1,2 m, `unshaded`) + partículas subindo + **anel no chão** (Decal), na cor do boss: **Tomate `#E5484D` · Uva `#7B3FA0` · Dragão `#E0337E` · Pimenta `#FF6A1F` · Final `#FFD21F`**.
- Estados: **pronto** (aura média, pulsando devagar); **itens no altar** (aura mais forte e as partículas aceleram conforme completa 1/3, 2/3, 3/3); **boss vivo** (aura vermelha-escura intensa, santuário bloqueado); **boss já derrotado** (aura **fraca** — dá para reinvocar com itens comuns). **Santuário final selado:** aura dourada **muito fraca** até subir.
- **Minimapa:** ícone na cor do boss. Sem texto no mundo.
- Visível de longe (⚙️ 120 m); não pode tapar a visão (colunas finas, opacidade ≤ 0,35).

## Teste
`dev/validate_lote2b`: nenhum `Label3D` visível nas categorias acima (fora debug), ícone de interação aparece a ≤ 3 m, anel de progresso na cama, tela do caça-níquel escura em repouso e aceita em giro, auras por boss com cor/estado, ícone no minimapa. Placar.

## Checklist
- [ ] Textos do mundo removidos · [ ] Ícone de interação (E + tipo + preço em moeda) · [ ] Bug da cama corrigido (anel)
- [ ] Caça-níquel: tela escura até ativar · [ ] Auras por boss com estados · [ ] Ícone no minimapa · [ ] Validador · Nada além disso foi alterado
