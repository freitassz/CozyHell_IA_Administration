# Padrões que funcionaram (usar sempre)

## Coisas no chão
- Sempre **`Decal`**, nunca disco plano (o terreno é torto e o disco flutua).
- Posicionar por raycast, `size.y` alto (4–8), `upper_fade`/`lower_fade` 0,3.
- `cull_mask` **só no terreno**. Várias peças = raycast por item.
- Marcador padrão de área: `decal_alvo_mergulho.png` (branco, pintado por `modulate`).

## Leitura de perigo
- Vermelho forte `Color(1, 0.18, 0.15)`; amarelo some na grama.
- Telegraph: decal preenchido e listrado + coluna de luz (BoxMesh unshaded com gradiente) + piscar acelerando + branco nos últimos 0,1 s.
- Mostrar a área segura e os limites (grade fina e borda).

## Justiça para o jogador
- Aviso de ≥ ~1,2 s em ataques de área.
- Áreas **redondas**; espaços seguros grandes; no máximo 1 dano por onda.
- Janela previsível de revidar depois do ataque.
- Ataque especial: chance base + **garantia** (se não saiu em 2 ataques, o próximo é ele). Ataques forçados não contam.

## Partículas
- Nada de cubos, quadrados, discos ou bolhas sólidas.
- Terra: torrões low-poly girando e encolhendo + poeira billboard (`poeira.png`) + graminhas.
- Elétrico: clarão + raios piscando + rede de raios + faíscas esticadas (`particle_flag_align_y`) + uma `OmniLight3D`.

## Desempenho
- Pool de decals/colunas/efeitos; limite de efeitos 3D por onda (ex.: 20 raios); **um** som por onda.

## Bosses
- Entrada genérica `boss_intro.tscn` (faixas de cinema, título + subtítulo, câmera lenta) e barra genérica `boss_barra.tscn` (nome, cor, rastro branco, marcador de fase).
- Invulnerável durante a entrada.
- Só ataca de novo com o corpo pronto.
- Janela de ataque clara (ex.: cabeça presa com dano multiplicado).

## Godot (regras para o Ziva)
- Nunca editar o `.glb`: cena wrapper + achar nós por tipo (`find_children`).
- `BoneAttachment3D` nos ossos `FX_*`; emissores de partículas fora do modelo, copiando só a posição.
- Loops por código (`loop_mode = LOOP_LINEAR`), encadear por `animation_finished`, blend 0,1 s ao sair de loop.
- Troca de cor por `set_surface_override_material` (cor de material não exporta do Blender).
