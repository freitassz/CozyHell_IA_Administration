# PROMPT ZIVA — Lote 3B: fauna pacífica (vaca-melancia reformulada, porcos, pássaros no céu)

## Contexto
O mundo está parado. Vamos dar vida com animais **pacíficos**, em placeholders (blocos coloridos facetados; o Gustavo faz os modelos depois). **Desempenho importa:** só animais a ≤ ⚙️ 60 m do jogador processam; no máximo ⚙️ 20 ativos; pássaros em `MultiMesh`.
- Modo rápido, com validador. **Não mude o que não está pedido** (o Totem de Melancia com 10 vacas continua igual). Comente em português. ⚙️ = valor escolhido por mim. Posições **pela seed**; estado do que morreu no save (como as vacas hoje).

## ETAPA 0 — Relatório curto
Como a vaca-melancia (`cow_mellon`) funciona hoje (vida, movimento, spawn, contagem para o Totem, grupo `cows`) e o que o `NpcSpawner` faz com animais.

## 1. Vaca-melancia: rework + drop
- **Comportamento:** pacífica. **Pasta** (anda devagar, para ⚙️ 3–8 s, balança a cabeça), vive em bandos pequenos (⚙️ 1–3). Ao ser ferida **foge em zigue-zague** ⚙️ 4 s a ⚙️ 6 m/s e volta a pastar. Vida ⚙️ 60. **Continua contando para as 10 do Totem** (não mude a contagem nem o ID por posição de nascimento).
- **Drop novo:** **Fatia de Melancia** (⚙️ 1–2): item **consumível** — segurar o botão esquerdo ⚙️ 0,8 s com ela na mão (anel de progresso, sem texto) **cura ⚙️ 20 de vida** e dá ⚙️ +10% de velocidade por 10 s. Placeholder: meia-lua verde/vermelha.
- Visual: mantenha o modelo atual; só ajuste animação de pastar/fugir se for simples (balanço do corpo por código).

## 2. Porcos (novo)
- Pacíficos, rosa claro `#F4A6B8`, bloco facetado com focinho e rabinho placeholder. Andam em **grupos de 2–4** em Planície e Floresta (⚙️ ~1 grupo por 150×150 m), pastam como a vaca, **fogem** ao serem feridos. Vida ⚙️ 40.
- **Drop:** **Carne de Porco** (⚙️ 1–2): consumível igual, **cura ⚙️ 15** (sem bônus). Também serve de material para o Trader/Andarilho (vende por R$).
- Morreu: respawna **no dia seguinte** no mesmo ponto de pasto (sem salvar o animal vivo; salve só "morto no dia X").

## 3. Pássaros no céu (ambiente)
- **Bandos** de 3–6 pássaros pequenos (placeholder: "V" achatado em cor clara `#F2F2E8`, batendo asas por shader/MultiMesh) **circulando** a ⚙️ 35–70 m de altura em volta de pontos fixos (pela seed), mudando de direção devagar. Só existem a ≤ ⚙️ 200 m do jogador (limite ⚙️ 12 pássaros visíveis).
- **Reação:** tiro ou explosão a ≤ ⚙️ 30 m **espalha** o bando (voam para longe e voltam em ⚙️ 20 s). Não têm vida nem drop; não atrapalham mira (sem colisão).
- Somem à noite (⚙️ 20h–5h) e a chuva forte os faz descer (opcional).

## 4. Sinais (para sons depois)
`animal_ferido(tipo, pos)` · `animal_morreu(tipo, pos)` · `consumivel_usado(item)` · `bando_espalhou(pos)`.

## Teste
`dev/validate_lote3b`: vaca pasta/foge e ainda conta para o Totem, drop Fatia de Melancia cura 20 e dá velocidade, porcos em grupos pela seed (mesma seed = mesmos pontos), foge, Carne de Porco cura 15, respawn no dia seguinte, pássaros só perto e só de dia, espalham com tiro, limite de ativos, save/carregar. E `dev/fauna_preview.tscn`. Placar.

## Checklist
- [ ] Vaca pacífica (pasta/foge) + Fatia de Melancia consumível · [ ] Porcos + Carne de Porco · [ ] Bandos de pássaros no céu (MultiMesh), reagem a tiro
- [ ] Limites de desempenho · [ ] Totem de Melancia intacto · [ ] Validador + prévia · Nada além disso foi alterado
