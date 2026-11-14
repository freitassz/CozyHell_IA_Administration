# PROMPT ZIVA — F2.1: Ajustes do tiro (recarga, recuo, alcance, visual, projétil, impacto)

## Contexto
O protótipo do tiro (F2) foi testado e aprovado. O teste apontou ajustes.
- **Não mude o que não está pedido.** Essência, especiais, mira, fusão e save continuam como estão.
- **Faça uma etapa por vez e teste.**
- Comente o código em português.
- Tudo novo em `WeaponData` ou `@export`. Valores que eu escolhi: ⚙️.
- O soco com a mão esquerda **não** faz parte deste prompt (virá uma animação nova do Blender).

---

## ETAPA 1 — Recarga na tecla R + bug
- Investigue por que **às vezes a recarga não acontece** ao apertar o botão (conflito de tecla? bloqueada durante `_Atirar`/`_Cooldown`/saque? essência insuficiente sem aviso?). **Me diga a causa** no relatório.
- Ação `recarregar` na tecla **R**.
- Se a recarga for pedida durante o tiro/cooldown, **guarde o pedido** e recarregue assim que puder (não ignore o aperto).
- Recarga negada por essência deve sempre mostrar o aviso (Etapa 4 da F2).

**Teste:** apertar R logo depois de atirar sempre recarrega (com essência); sem essência sempre mostra o aviso.

## ETAPA 2 — Recuo com curva (por código)
O recuo atual da pistola de teste é a animação `_Atirar` acelerada e fica linear. Troque por **recuo procedural**: **sobe rápido e desce devagar**.
Novos campos no `WeaponData`:
```gdscript
@export var recuo_camera_graus := 1.5      # chute da câmera para cima
@export var recuo_lateral_graus := 0.3     # aleatório para os lados
@export var recuo_arma_m := 0.04           # arma vai para trás
@export var recuo_arma_graus := 6.0        # arma gira para cima
@export var recuo_subida_s := 0.04         # tempo para chegar no pico (rápido)
@export var recuo_volta_s := 0.22          # tempo para voltar (devagar, ease-out)
```
- Aplique num nó-pivô **acima** do visual da arma (não no `.glb`) e na câmera.
- Subida: interpolação rápida (`TRANS_QUAD`, `EASE_OUT`); volta: suave (`TRANS_SINE` ou mola, `EASE_IN_OUT`).
- Tiros seguidos **somam** o recuo antes de voltar (rajada sobe mais).
- Armas de teste: **não toquem** `_Atirar` acelerada; só recuo procedural + clarão. O revólver mantém sua animação com um recuo procedural leve por cima.
- Ao mirar, recuo × 0,6 ⚙️.

| Arma | câmera ° | lateral ° | arma m | arma ° | subida s | volta s |
|---|---|---|---|---|---|---|
| Revólver | 2,0 | 0,4 | 0,03 | 4 | 0,04 | 0,25 |
| Pistola rápida | 0,8 | 0,3 | 0,03 | 5 | 0,03 | 0,15 |
| Escopeta | 4,0 | 0,8 | 0,08 | 12 | 0,05 | 0,35 |
| Sniper | 5,0 | 0,2 | 0,10 | 10 | 0,05 | 0,45 |
| Estilingue | 0,5 | 0,1 | 0,05 | 2 | 0,06 | 0,20 |

**Teste:** a pistola "pula e assenta"; segurar o tiro sobe a mira aos poucos; a escopeta dá um coice forte.

## ETAPA 3 — Alcance infinito com queda de dano
Nenhum tiro tem mais limite curto: **quanto mais longe, menos dano, até no mínimo 1**.
Troque `alcance_m` e `queda_dano_50_m` por:
```gdscript
@export var alcance_eficaz_m := 30.0     # até aqui, dano cheio
@export var meia_vida_dano_m := 25.0     # a cada X metros depois do eficaz, o dano cai pela metade
@export var dano_minimo := 1.0
const ALCANCE_TECNICO_M := 1000.0        # limite só para o raycast/projétil não ir ao infinito

func dano_na_distancia(d: float, dano_base: float) -> float:
    if d <= alcance_eficaz_m:
        return dano_base
    var f := pow(0.5, (d - alcance_eficaz_m) / meia_vida_dano_m)
    return max(dano_minimo, dano_base * f)
```
- O bônus de nível e o multiplicador do especial são aplicados **antes** da queda.
- **Tiro fraco:** se o dano final for ≤ 10% do dano base ⚙️, toque um som diferente (um "plink" fraco; use um som existente com `pitch_scale` alto se não houver outro) e mostre o marcador de acerto **cinza**. Sinal `tiro_fraco(alvo, dano)`.

| Arma | eficaz m | meia-vida m |
|---|---|---|
| Revólver | 35 | 30 |
| Pistola rápida | 25 | 20 |
| Escopeta | 10 | 8 |
| Sniper | 150 | 120 |
| Estilingue | 25 | 30 |

**Teste:** acertar um inimigo muito longe com a escopeta dá 1 de dano, som "plink" e marcador cinza; a sniper continua forte longe.

## ETAPA 4 — Visual do tiro instantâneo
O rastro amarelo atual parece errar porque sai do cano enquanto o tiro sai do centro da tela.
- O **dano continua instantâneo** pelo raio da câmera.
- O visual vira uma **bala-rastro curta** (⚙️ 1,2 m de comprimento, emissiva) que viaja do **cano** (`BoneAttachment3D` do osso `Cano`) até o **ponto exato** acertado pelo raio da câmera, em ⚙️ 0,05–0,08 s.
- Errou sem colidir: vai até 300 m ⚙️ e some.
- Cor por arma: `@export var cor_rastro := Color(1, 0.9, 0.5)`.
- Use pool (sem criar/destruir nó a cada tiro).

**Teste:** atirando num inimigo parado, o rastro sempre termina **nele**.

## ETAPA 5 — Tiro projétil (inclui arco de estilingue)
Implemente `tipo_tiro = Projetil`:
```gdscript
@export var velocidade_projetil_ms := 60.0
@export var gravidade_mult := 0.0        # 0 = reto; 1 = gravidade normal (arco)
@export var tempo_vida_projetil_s := 5.0
@export var cena_projetil: PackedScene   # malha simples placeholder
```
- O projétil sai do cano em direção ao **ponto que o raio da câmera indica** (converge com a mira).
- Colisão por raycast entre a posição anterior e a atual a cada frame (não atravessar inimigo em alta velocidade).
- Dano usa a mesma `dano_na_distancia`, com a **distância percorrida**.
- Placeholder: rolha = cilindro curto bege; pedra do estilingue = icosfera low-poly cinza. Pool de projéteis.
- **Escopeta de teste** passa a ser projétil: ⚙️ velocidade 70 m/s, gravidade 0,3 (6 rolhas).
- Crie a arma de teste **"Teste — Estilingue"** (só F3, fora da máquina, visual do revólver):

| Dano | Proj. | Cadência | Pente | Recarga | Custo recarga | Essência/acerto | Velocidade | Gravidade | FOV mira | Especial |
|---|---|---|---|---|---|---|---|---|---|---|
| 35 | 1 | 1,5/s | 8 | 1,0 s | 5 | 3 | 35 m/s | 1,0 | 65 | — |

**Teste:** a pedra do estilingue faz um arco visível e é preciso mirar acima de alvos longe; as rolhas da escopeta voam visíveis.

## ETAPA 6 — Impacto (em modo de teste, para escolher jogando)
Tudo ligável/desligável para o Gustavo comparar. Cada inimigo ganha `@export var cor_impacto: Color` (padrão: cor principal do material dele).

1. **Efeito no acerto** — `@export_enum("Gotas", "Lascas", "Nenhum") var modo_impacto`:
   - **Gotas:** 6–10 gotinhas low-poly (icosfera pequena, `cor_impacto`) saindo do ponto do acerto no sentido contrário ao tiro, caindo com gravidade e encolhendo em 0,4 s. Sem mancha no chão.
   - **Lascas:** 4–6 pedacinhos facetados (triângulos/cunhas, `cor_impacto`) girando, caindo e encolhendo em 0,5 s.
   - Partículas **sem** cubos/quadrados; pool; no máximo 30 por segundo.
2. **Achatar** — `@export var achatar_ao_levar_dano := true`: escala do visual do inimigo vai a (1,15; 0,85; 1,15) e volta em 0,12 s.
3. **Tranco visual** — `@export var tranco_visual := true`: o **modelo** inclina ~10° para trás (no sentido do tiro) e volta em 0,15 s. **Não muda a posição** do inimigo. (O knockback real continua só pelo `knockback_m` da arma.)
4. **Erro:** tiro que acerta o chão/parede solta uma poeirinha (`poeira.png`, billboard alfa) pequena.
5. **Tecla de teste F6** (só em debug): alterna o `modo_impacto` (Gotas → Lascas → Nenhum) e mostra o nome no canto da tela por 1 s.

**Teste:** com F6 dá para comparar Gotas e Lascas no mesmo inimigo; achatar e tranco podem ser desligados no Inspector.

---

## Sinais novos
`tiro_fraco(alvo, dano)` · `projetil_acertou(alvo, dano, posicao)`

## Checklist final
- [ ] Causa do bug da recarga explicada e corrigida; recarga no R com pedido guardado
- [ ] Recuo procedural com curva (sobe rápido, desce devagar), soma em rajada, por arma
- [ ] Alcance infinito com queda até 1 de dano; som "plink" + marcador cinza no tiro fraco
- [ ] Rastro do instantâneo termina no ponto exato do acerto
- [ ] Projétil com velocidade e gravidade; escopeta virou projétil; Estilingue de teste com arco
- [ ] Impacto: Gotas / Lascas / Nenhum (F6), achatar e tranco visual ligáveis, poeira no erro
- [ ] Nada além disso foi alterado
