# PROMPT ZIVA — Lote 4A: terreno suave, montanhas variadas, grama que não flutua e grama cortável

## Contexto
Playtest: o terreno parece "textura mal renderizada" (formas duras de baixa resolução), as montanhas são todas iguais, a grama flutua nos penhascos e não reage a cortes/tiros. **Desempenho importa** (o notebook do Gustavo é fraco): prefira cálculo no shader e texturas pequenas; **reporte o FPS antes/depois** na cena de prévia.
- Modo rápido, com validador. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim (`@export`).
- ⚠️ Mudar o relevo muda a seed → **mundos antigos ficam incompatíveis** (construções podem ficar enterradas). Avise no relatório e deixe o `versao_save` registrar a versão do gerador.

## ETAPA 0 — Relatório curto
Como o terreno é colorido hoje (vertex color? splat? shader?), resolução/filtragem da textura de blend entre biomas, como a grama é gerada (MultiMesh? altura usada), e como o relevo/montanhas são gerados no `IslandGenerator` (ruídos e seeds).

## 1. Blend suave do terreno (#25)
- Remova o efeito "baixa resolução": o blend entre biomas e cores do terreno passa a ser calculado **por fragmento** no shader (mesmas funções/ruídos analíticos do gerador, `world_seed`), com transições suaves de ⚙️ 6–10 m, sem textura de blend de baixa resolução e sem filtro `nearest`.
- Estilo do jogo mantido: cores chapadas e foscas, **sem** textura fotográfica; só gradiente suave entre biomas + variação de cor de grande escala (ruído lento ⚙️ ±6% de luminosidade) para quebrar a monotonia.
- Cores base: Planície verde-limão claro, Floresta verde mais fundo, Pedreira cinza-azulado claro; encostas muito inclinadas (> ⚙️ 40°) misturam **pedra** (`#9FB4C7`), topos de montanha altos misturam um tom mais claro.

## 2. Montanhas variadas (#27)
- Adicione **tipos de relevo** escolhidos por um ruído de baixa frequência por região (com a seed), mantendo a ilha, o spawn plano e as áreas planas exigidas por estruturas (santuário do Dragão, NPCs):
  **pico** (ruído ridged/cone), **mesa/platô** (topo plano terraceado), **morro redondo** suave, **cordilheira** (alongada, domain-warp) e **penhasco** (degraus).
- Preferências por bioma ⚙️: Planície = morros suaves; Floresta = morros + cordilheiras baixas; Pedreira = mesas, picos e penhascos.
- Alturas máximas e inclinações mantêm o jogo caminhável (rampas), e o minimapa continua funcionando.

## 3. Grama que não flutua (#18)
- A altura de cada tufo vem da **mesma função analítica** do terreno (`get_height_at`) e a base fica **abaixo** da superfície (⚙️ −0,05 m); a inclinação segue a normal.
- **Não nascem tufos** em inclinação > ⚙️ 38°; entre 30° e 38° o tamanho cai suavemente a 0. Nada de grama em cima de rocha/estrutura/construção.

## 4. Grama cortável e chão "pelado" (#19)
- **Máscara de grama** em coordenadas do mundo (⚙️ 512×512 cobrindo 100 m ao redor do jogador, rolando com ele), usada pelo shader da grama (`discard` onde cortada) e pelo terreno (mistura para **terra clara** `#C9A66B` onde cortada).
- Pintam a máscara (círculo suave): **tiro** que acerta o chão ⚙️ raio 0,5 m · **golpe de arma cortante** (Cutelo, Facão, Martelo, Machadinha) que acerta o chão/passa rente ⚙️ raio 1,2 m · **explosões** ⚙️ o raio delas · **Lança-Chamas/Lampião**: queima grama (raio 1,5 m, terra **escura** `#8A6A3F`).
- A grama **volta** gradualmente em ⚙️ 3 minutos de jogo. Efeito **só visual** (não salva).
- Pool de pinturas (máx. ⚙️ 20 por segundo).

## Teste
`dev/validate_lote4a`: sem tufos acima de 38°, base abaixo do terreno, tipos de relevo presentes por bioma e spawn/áreas planas intactas, máscara corta a grama e pinta o chão, grama volta, FPS reportado. E `dev/terreno_preview.tscn`. Placar.

## Checklist
- [ ] Blend por fragmento, sem baixa resolução · [ ] 5 tipos de montanha por bioma, áreas planas intactas · [ ] Grama sem flutuar (≤ 38°)
- [ ] Máscara de corte + chão pelado (tiro, lâmina, explosão, fogo) e regrowth · [ ] Aviso de mundo antigo · [ ] Validador + prévia + FPS · Nada além disso foi alterado
