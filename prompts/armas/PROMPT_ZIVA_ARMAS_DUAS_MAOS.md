# PROMPT ZIVA — Armas de duas mãos: Espingarda de Rolha, Metralhadora de Sementes e Rifle de Pressão

## Contexto
O chat de modelagem entregou 3 armas novas com animações, já na pasta do jogo. Elas substituem as armas de teste "Escopeta" e "Sniper".
São as **primeiras armas de duas mãos**: a mão esquerda segura a arma o tempo todo, e o soco rápido (V) vira **coronhada**.
- **Não mude o que não está pedido.** O revólver, o soco esquerdo, a essência, a mira e o recuo continuam iguais.
- **Faça uma etapa por vez e teste.**
- Comente o código em português. Valores que eu escolhi: ⚙️.

## Arquivos
| Arquivo | Raiz | Para quê |
|---|---|---|
| `res://Blender/armas/espingarda/espingarda.glb` | `EspingardaRig` | Espingarda de Rolha |
| `res://Blender/armas/metralhadora/metralhadora.glb` | `MetralhadoraRig` | Metralhadora de Sementes |
| `res://Blender/armas/rifle_pressao/riflepressao.glb` | `RiflePressaoRig` | Rifle de Pressão |
| `res://Blender/bracos_novo/bracos.glb` | `BracosRig` | braços com as ações das 3 armas **e** do revólver (`revolver.glb` não mudou) |

- Cada arma vai presa no `BoneAttachment3D` do osso **`Arma_R`** com **transform zerado** (a escala 1,35 já vem na raiz do glb).
- Osso **`Cano`** na boca do cano, apontando para a frente (+Y), paralelo à câmera → origem do rastro/projétil.
- Ossos especiais (já animados, não mexer por código): Espingarda `Bomba`, `Rolha`, `Gatilho` · Metralhadora `Reservatorio`, `Gatilho` · Rifle `Alavanca`, `Chumbinho`, `Gatilho`.
- **Material:** textura assada → use `albedo_texture` (não vertex color) num material **toon fosco** igual ao dos braços (roughness 1, specular 0, metallic 0) **com o mesmo contorno**. Sem `EssenciaMagica`.

## Ações (30 fps) — tocar o **mesmo nome** nos braços e na arma, juntos
Prefixos: `Espingarda`, `Metralhadora`, `RiflePressao`.
| Ação | Duração | Notas |
|---|---|---|
| `<P>_Sacar` | 0,5 s (16 q) | |
| `<P>_Pose` | 2,0 s (61 q) | **loop** |
| `<P>_Atirar` | 0,1 s (4 q) | |
| `<P>_Cooldown` | Espingarda **0,5 s** (bombeia) · Metralhadora 0,1 s · Rifle 0,3 s | |
| `<P>_Recarregar` | Espingarda 1,8 s · Metralhadora 2,0 s · Rifle 2,2 s | eventos de munição abaixo |
| `<P>_Guardar` | 0,4 s (13 q) | |
| `<P>_Coronhada` | 0,6 s (19 q) | **impacto em 0,2 s** (quadro 7) |

Eventos da recarga (tempo da animação na velocidade 1x):
- **Espingarda:** rolha 1 entra em **0,70 s** (+1 bala), rolha 2 em **1,27 s** (+1 bala); bombeia em ~1,5 s.
- **Metralhadora:** pote recolocado em **1,33 s** → pente cheio aí.
- **Rifle:** bombeia em 0,37 s e 0,77 s; chumbinho entra em **1,63 s** → carregado aí.

---

## ETAPA 1 — Montar as 3 armas na mão
- Instancie os 3 glb no encaixe `Arma_R` (como o revólver), escondidos; só aparece a arma que está na mão.
- No `WeaponData`, garanta `cena_visual` e um campo `prefixo_anim: String` (revólver = `Revolver`).
- O `ArmaFps` passa a tocar `<prefixo>_*` da arma na mão, nos dois `AnimationPlayer`.
- Rastro/projétil saem do `BoneAttachment3D` no osso `Cano` **da arma na mão**.
- Material toon fosco + contorno (ver acima).
- Confira que o **revólver e o soco esquerdo continuam funcionando** com o `bracos.glb` novo.

**Teste:** trocar entre as 4 armas mostra a arma certa, com as duas mãos na arma nas 3 novas; o rastro sai da boca do cano de cada uma.

## ETAPA 2 — Fichas das armas (substituem as de teste)
Crie `ItemData` + `WeaponData` das 3 (no F3), com estes valores iniciais ⚙️:

| Campo | Espingarda de Rolha | Metralhadora de Sementes | Rifle de Pressão |
|---|---|---|---|
| Raridade | Comum | Comum | Raro |
| `tipo_tiro` | Projétil (rolha) | Projétil (semente) | Instantâneo |
| `dano` × `projeteis_por_tiro` | 8 × 6 | 9 × 1 | 90 × 1 |
| `dispersao_graus` | 8 | 3 | 0 |
| `cadencia_tps` | 1,2 | 9 | 0,7 |
| `pente` | 2 | 40 | 4 |
| `recarga_s` | 1,8 | 2,0 | 2,2 |
| `custo_essencia_recarga` | 20 | 25 | 15 |
| `essencia_por_acerto` | 0,8 | 0,5 | 5 |
| `alcance_eficaz_m` / `meia_vida_dano_m` | 10 / 8 | 25 / 20 | 150 / 120 |
| projétil: velocidade / gravidade | 70 / 0,3 | 80 / 0,15 | — |
| `fov_mira` | 68 | 60 | 30 |
| `automatica` | não | **sim** | não |
| `usa_duas_maos` | **sim** | **sim** | **sim** |
| `usa_animacao_tiro` | sim | sim | sim |
| `especial` | **Coice** (o da escopeta de teste) | nenhum | **nenhum** |
| recuo (`forca_recuo` e tabela) | igual à escopeta de teste | pistola de teste (automática), limites 18° / 0,05 m / 5° | igual à sniper de teste |

- Projétil da semente: crie `scenes/weapons/projeteis/semente.tscn` (icosfera pequena alongada, bege/marrom claro, placeholder).
- **Remova** as armas de teste "Escopeta" e "Sniper" (ItemData, WeaponData, saves de teste). **Mantenha** "Pistola rápida" e "Estilingue" de teste.

**Teste:** as 3 aparecem no F3 com os nomes certos e atiram com os valores da tabela.

## ETAPA 3 — Ritmo do tiro sem câmera lenta
O `ArmaFps` ajusta a velocidade para `Atirar + Cooldown = 1 / cadencia_tps`. No Rifle (0,7/s) isso deixaria o bombeio em **câmera lenta**.
- Regra nova: a velocidade de `Atirar`/`Cooldown` é `max(1.0, (atirar + cooldown) * cadencia_tps)` — **nunca abaixo de 1x**. Se sobrar tempo até o próximo tiro, a arma espera na `_Pose`.
- Vale para todas as armas (o revólver não deve mudar de ritmo; confira).

**Teste:** o Rifle bombeia em velocidade normal e espera; a Metralhadora segura a 9/s sem travar a animação.

## ETAPA 4 — Recarga com eventos de munição
- Recarga continua gastando a essência **no início**.
- A munição entra **nos momentos dos eventos** (tempo do evento ÷ velocidade da recarga), não no fim:
  - Espingarda: +1 em 0,70 s e +1 em 1,27 s;
  - Metralhadora: pente cheio em 1,33 s;
  - Rifle: pente cheio em 1,63 s.
- Se a recarga for **interrompida** (troca de arma, soco), fica a munição que já entrou.

**Teste:** interromper a recarga da espingarda depois da 1ª rolha deixa 1 bala no pente.

## ETAPA 5 — Coronhada (V nas armas de duas mãos)
- Com `usa_duas_maos = true`, **V** toca `<P>_Coronhada` nos **dois** players (braços e arma) — **não** usa o `AnimEsquerda`.
- Impacto em **0,2 s** pela posição da animação; mesmo ShapeCast do soco; dano = dano do soco × ⚙️ **1,5**; **+12 de essência** por acerto.
- Cooldown = duração da coronhada (0,6 s). Bloqueada no saque e na recarga (mesma regra do soco esquerdo). Depois volta para `<P>_Pose`.
- Remova o fallback antigo (guardar → socar → sacar) se nenhuma arma usar mais.

**Teste:** V com cada uma das 3 dá a coronhada, a mira continua livre, acerta no impacto e enche essência.

## ETAPA 6 — Máquina caça-níquel
- Adicione ao pool da máquina de armas: Espingarda (Comum), Metralhadora (Comum), Rifle de Pressão (Raro), junto do Revólver Enferrujado (Comum).
- Renomeie o item do revólver para **"Revólver Enferrujado"** e o especial dele para **"Repimboca"** (só o nome).

**Teste:** girar a máquina várias vezes sai as 4 armas.

---

## Checklist final
- [ ] 3 armas montadas no `Arma_R`, duas mãos visíveis, rastro/projétil saindo do `Cano` de cada uma
- [ ] Material toon fosco com `albedo_texture` + contorno
- [ ] Fichas criadas; Escopeta e Sniper de teste removidas; Pistola e Estilingue de teste mantidos
- [ ] Ritmo sem câmera lenta (`max(1.0, …)`); revólver com o mesmo ritmo
- [ ] Munição entra nos eventos da recarga; interrupção mantém o que entrou
- [ ] Coronhada no V para armas de duas mãos (impacto 0,2 s, ×1,5, +12 essência)
- [ ] 4 armas na máquina; Revólver Enferrujado e Repimboca renomeados
- [ ] Revólver e soco esquerdo funcionando com o `bracos.glb` novo
- [ ] Nada além disso foi alterado
