---
name: "cozyhell-prompts-ziva"
description: "Escrever prompts para o Ziva AI implementar inimigos, bosses, armas, ataques, efeitos e sons no jogo CozyHell3D (Godot 4), já conhecendo o jogo, o sistema de armas, os padrões e o que deu certo ou errado."
---

# Prompts para o Ziva AI — CozyHell3D

O usuário (Gustavo) faz o jogo **CozyHell3D** em **Godot 4 (GDScript)**. Quem escreve o código no projeto é o **Ziva AI**, uma IA dentro do Godot. O meu papel é escrever **prompts** que o Ziva siga sem errar e, quando precisar, entregar os **arquivos de apoio**: texturas, malhas de efeito (GLB) e sons.

A modelagem 3D (personagens, rig, animações) é da skill `lowpoly-game-3d-blender`. Use as duas juntas quando o pedido tiver modelo e lógica.

O usuário escreve em português, gosta de trabalhar **por etapas** e testa no jogo antes de pedir o próximo ajuste.

## Central do projeto (ler primeiro)

- Tudo o que foi decidido está no repositório **`freitassz/CozyHell_IA_Administration`** (branch `main`). **Em conflito, o repositório vence esta skill.** Ordem: `docs/jogo/decisoes.md` e `docs/jogo/loop.md` > resto do repo > esta skill > planilha de armas.
- Arquivos-chave: `ROADMAP.md` (fase atual), `docs/jogo/revisao.md` (pendências com ID), `docs/jogo/inventario.md` (o que existe no jogo), `docs/armas/ficha-campos.md` (campos do `WeaponData`), `docs/armas/guia-estilo.md`, `docs/sistemas/fundacao.md` (save).
- Prompts do Ziva ficam em `prompts/<assunto>/PROMPT_ZIVA_<ASSUNTO>.md`; pedidos para o chat de modelagem em `prompts/blender/PROMPT_BLENDER_<ASSUNTO>.md`.
- **Fluxo:** o chat de administração escreve o pedido de modelagem → o **chat de modelagem** (skill `lowpoly-game-3d-blender`) faz o modelo/animação e devolve dados (nomes, durações, impactos, ossos) → o Gustavo traz para cá → escrevo o prompt do Ziva.
- Padrão que funcionou: **Etapa 0 = relatório** (o Ziva só investiga e para); eu respondo as decisões num arquivo `RESPOSTA_*.md`; depois ele segue etapa por etapa e devolve placar dos validadores em `dev/`.

## O jogo (o que já sei)

- **Godot 4**, em primeira pessoa, low-poly colorido, com grama clara verde-limão e terreno **irregular** (morros).
- HUD: vida, dinheiro (R$), sucata, defesa, dia/hora e minimapa. Tem **modo criativo** (F3) que dá itens tipo “Ovo: Dragão-Pitaya (Boss)” para spawnar bosses.
- Pastas do projeto (raiz `3dddddd`): `Blender`, `enemies`, `scenes`, `scripts`, `SFX`, `VFX`, `shaders`, `Terrain`, `ui`, `resources`, `addons`.
- Os assets que eu entrego vão para `C:\Users\Gustavo\Documents\jogo 3d\CozyHell3D\3dddddd\Blender\<subpasta do asset>\`. Grave com `device_commit_files` e mande também no chat.
- O usuário pode conectar a **pasta do projeto inteira** (`3dddddd`). Quando ela estiver conectada:
  - leia **só** o necessário com `device_bash` (`grep -n`, `sed -n`, `wc -l`), nunca o projeto todo;
  - escreva o prompt com os **nomes reais** de cenas, nós, funções e sinais;
  - não edite o código do jogo: quem implementa é o Ziva.
- Quando a pasta não estiver conectada, mande o Ziva **procurar** os pontos no código ("procure o `anim.play(...)`") em vez de supor nomes.
- **Cores de raridade:** comum `#3DDC4A`, raro `#2F8BFF`, épico `#A23DFF`, lendário `#FFD21F`.
- **Coordenadas:** o Blender (x, y, z) vira Godot (x, z, −y). Os modelos são feitos com a frente em −Y no Blender, que é +Z no Godot. Peças de corrente usam a frente em −Z no Godot (`Basis.looking_at`).
- O usuário **muda a escala** dos bosses (o dragão ficou 3x). Todo prompt deve ter **uma variável `escala`** e dizer o que multiplica por ela.
- **História:** é o **sonho de um fazendeiro**; as plantas se revoltam contra ele. Cozy = sonho; Hell = pesadelo que avança com a progressão.
- **Loop (Terraria/Muck):** mundo **persistente**; coletar → vender na **Barraca de Venda** (construída pelo jogador) → R$ → **máquina caça-níquel** de armas (e máquina de acessórios) → bigorna → boss. Cada boss libera uma raridade na máquina e dropa material único; a Uva-morcego libera a **fase 2 de inimigos**.
- **Biomas:** Planície, Floresta, Pedreira. 1 minério hoje (ferro); plano: 4, travados por picareta.
- **Inimigos por fase:** 1 = Tomate, Cenoura, Pimentão · 2 = Cebola, Milho, Abóbora (a Abóbora ainda não existe no código) · 3 em aberto. **Sem** variantes Mutante/Ancestral (removidas). Vaca-melancia: 10 mortas → boss secreto Totem de Melancia.
- **Removidos do jogo:** plantio pelo jogador, enxada, pá, sementes comuns, loja (`unlock_pistol`), Mesa de Contrato (código em `res://_arquivo/weapon_trader/`, vira NPC futuro de fichas de raridade), armas placeholder antigas, números de dano flutuantes, `grant_weapon_bonus`.
- **Save (feito):** autoload `SaveManager`, `user://saves/<id>/mundo.json` + `estado.json` (`versao_save` 2), sistemas no grupo `salvavel` com `salvar()/carregar()` e `CHAVE_SAVE`. Menu principal, Novo Mundo (nome, seed, modo), Carregar/Apagar. Salva na cama, ao amanhecer, ao sair e ao fechar. **Todo sistema novo com estado precisa entrar no save.**
- **Seed define o mundo inteiro:** tudo que é colocado no mundo usa `RandomNumberGenerator` com `world_seed + offset`. IDs estáveis = tipo + posição arredondada a 0,1 m. Só o que reage ao jogador em tempo real (hordas noturnas) pode ser aleatório.
- **Modos:** **Soneca** (renasce na cama perdendo 30% R$/sucata e 50% recursos) e **Pesadelo** (morreu, o mundo é apagado).
- **Multiplayer virá:** nada de `Engine.time_scale` global, nada de "o player" único (dados por ID de jogador, `"local"` hoje), inimigos miram o jogador mais próximo.
- **Desempenho:** o jogo roda com FPS baixo em PC fraco (pendência T05). Evite custo por frame; use pools.

## Sistema de armas (estado nov/2026)

**A planilha "Cozy Hell — Sistema de Armas" é RASCUNHO** (lista de 35 armas e números vão mudar; será atualizada antes da criação das armas, item A03). Os campos reais do código estão em `docs/armas/ficha-campos.md`. Não trate nada da planilha como decidido.

### Princípios (decididos)
- Jogo **simples na essência**. Descartado: durabilidade, conserto, afiar, sujeira, combustível, peso/carga, fraquezas por arma, máquina de cerveja, "stamina de arma".
- **Raridade só na cor do nome** (Terraria). Sem multiplicador. O poder vem dos números/mecânica.
- **Stamina** = só movimento (correr, pular).
- **Essência do Sonho** (nome provisório): barra única das armas (HUD lilás `#B98CFF`). Enche com **acerto de tiro** (`essencia_por_acerto`, por arma), **soco** (+12 por acerto) e regeneração lenta (0,75/s). **Recarregar** e o **especial** gastam dela. Sem essência: recarga negada com aviso.
- **Munição infinita**; pente por **cópia** de arma; trocar de arma não enche o pente.
- **Superaquecimento:** em aberto (C06).
- Armas são **cópias** (não empilham): nível nv1–nv5 por cópia; **Fundir** na bigorna soma níveis (nv3+nv2=nv5, excesso perdido com aviso); bônus de dano `[0, 8, 14, 19, 23]%`; **Desmanchar** dá sucata.

### Controles
Botão esquerdo atira · **direito mira** (FOV `fov_mira`, dispersão × `mult_dispersao_mira`, andar × 0,6) · **R** recarrega (pedido guardado se estiver atirando) · **F** especial (algumas armas não têm) · **V** soco rápido · Q solta item.

### Como o tiro funciona hoje
- `WeaponData` (`resources/weapons/weapon_data.gd`) lido por tudo; nada de número fixo.
- **Tiro misto:** `Instantaneo` (dano pelo raio da câmera; **rastro** de 2 camadas unshaded do osso `Cano` até o ponto exato, pool) ou `Projetil` (`ProjetilPool`, velocidade, `gravidade_mult`, converge com a mira, raycast por frame).
- **Alcance infinito com queda:** dano cheio até `alcance_eficaz_m`, cai pela metade a cada `meia_vida_dano_m`, mínimo `dano_minimo` (1). Tiro fraco (≤10% ou preso no mínimo) → "plink" + X cinza.
- **Recuo procedural** (`recuo_arma.gd`): câmera no `Head`, arma no `HandsVisual`; sobe rápido, desce devagar; `forca_recuo` + limites `recuo_*_max_*` com **soma saturada**; mirando × 0,6. Durante a recarga da automática o recuo desce até 0. A mão esquerda escondida **nunca** pode aparecer.
- `automatica` (segurar atira; retoma após a recarga) · `carregavel` (segurar puxa, soltar atira; arco de carga na mira; mais longe/mais dano) · carregável vence automática; R/V/F/troca cancelam a carga.
- `usa_animacao_tiro` (só o revólver toca `_Atirar`); as outras só recuo procedural.
- **Especiais** = `EspecialArma` (Resource com `executar()`), `especial = null` = sem especial. Testes: Tiro do Coveiro (revólver), Coice (escopeta), Tiro Carregado (sniper, empurra até 3 m).
- **Knockback:** tiro normal **não empurra** (`knockback_m = 0`); só especiais com `empurrao_m`.
- **Impacto:** `ImpactoFx` só **Lascas** (`escala_lasca` no Player), `cor_impacto` por inimigo; **achatar + tranco visual só em inimigos comuns**, bosses **só piscam**. Marcador de acerto (X branco; vermelho no abate). **Sem números de dano.**
- Armas de teste (só F3, fora da máquina): Pistola rápida, Escopeta (rolhas), Sniper, Estilingue (carregável) — todas com o visual do revólver.

### Escrevendo prompt de arma
- Peça campos novos **no `WeaponData`** e atualize `docs/armas/ficha-campos.md`.
- Toda arma nova de **uma mão** deve esconder a mão esquerda na pose do revólver (soco `Soco_Esquerdo_Arma`); de **duas mãos**: `usa_duas_maos = true` e o V vira **coronhada** (animação própria).
- **Peça mágica é opcional** (criatividade livre). Se a arma tiver uma (`EssenciaMagica`), ela acende na recarga e no especial.
- Siga os padrões do jogo e "Não mude o que não está pedido".

## Formato do prompt (sempre)

Arquivo `.md` com nome `PROMPT_ZIVA_<ASSUNTO>.md`, salvo na pasta do asset.

1. **Título + contexto curto:**
   - o que já existe e funciona;
   - o que vamos fazer;
   - **"Não mude o que não está pedido"**;
   - "Faça uma etapa por vez e teste".
2. **Tabela de arquivos**, com caminho e para que serve cada um.
3. **Dados exatos:**
   - nomes de animações com duração e loop;
   - ossos/âncoras com posição no Godot;
   - materiais por `resource_name`;
   - medidas;
   - fórmulas.
4. **ETAPAS numeradas.** Cada etapa traz o que fazer, trechos de GDScript quando houver risco de errar, os `@export` com valores padrão e um **Teste**.
5. **Sinais** com nome e parâmetros: os sons e outros sistemas ligam neles.
6. **Checklist** final com `[ ]`, terminando em "Nada além disso foi alterado".
7. "Comente o código em português."

Regras de escrita:

- **Prompt de ajuste** (o sistema já existe): curto, só os pontos pedidos, com a causa provável do bug explicada em uma linha.
- **Prompt de sons separado** (`PROMPT_ZIVA_SONS_*.md`):
  - liga cada arquivo a um sinal ou `anim.play` existente;
  - diz onde o som toca: "no lugar" (player criado fora do boss e liberado no `finished`) ou "preso" (filho do nó);
  - dá `unit_size` e `max_distance`;
  - pede tudo com `volume_db` 0, porque os níveis já vêm equilibrados.
- Quando eu tomar uma decisão que o usuário não especificou, coloque em `@export` e **avise na resposta**.
- Godot: achar nós **por tipo** (`find_children`), usar cena wrapper e **nunca editar o .glb**. Loops por código (`loop_mode = LOOP_LINEAR`), encadear pelo `animation_finished` e usar blend de 0,1 s ao sair de loop.

## Padrões do jogo que funcionaram (usar sempre)

- **Marcador de ataque:** `decal_alvo_mergulho.png` (branco, pintado pelo `modulate`) é o **marcador padrão de área de ataque**.
- **Coisas no chão = `Decal`**, nunca disco plano. O terreno é torto e o disco flutua.
  - Posicione pelo raycast, com `size.y` alto (4–8) e `upper_fade`/`lower_fade` 0,3.
  - `cull_mask` **só no terreno**, para não pintar o boss nem o jogador.
  - Quando houver várias peças (torrões, casas de tabuleiro), faça **raycast por item**.
- **Leitura de perigo:** vermelho forte `Color(1, 0.18, 0.15)` contrasta com a grama clara; amarelo some nela.
  - Telegraph = decal preenchido e listrado + **coluna de luz** (BoxMesh unshaded com gradiente vertical) + piscar acelerando + **branco nos últimos 0,1 s**.
  - Mostre também a área segura e os limites: grade fina e borda.
- **Justiça para o jogador:**
  - aviso de pelo menos ~1,2 s em ataques de área;
  - área de ataque **redonda** (no quadrado, a diagonal é pior);
  - espaços seguros grandes;
  - no máximo 1 dano por onda;
  - ataques que dão **janela previsível de revidar** depois.
- **Frequência de ataque especial:** chance base + **garantia** ("se não saiu em 2 ataques, o próximo é ele"). Ataques "forçados" em sequência não contam.
- **Partículas bonitas:** sem cubos ou quadrados.
  - Terra: torrões low-poly (mesh) girando e encolhendo no fim, poeira billboard macia (`poeira.png`, alfa, não aditivo) e graminhas.
  - Elétrico: clarão rápido + raios que piscam + rede/casca de raios + faíscas esticadas (`particle_flag_align_y`) + uma `OmniLight3D` só.
  - Nada de disco ou bolha sólida.
- **Desempenho:** pool de decals/colunas/efeitos, limite de efeitos 3D por onda (ex.: 20 raios) e **um** som por onda em vez de um por item.
- **Bosses:**
  - **entrada** com cena genérica `boss_intro.tscn` (faixas de cinema, título + subtítulo, câmera lenta via `Engine.time_scale` com tween que ignora o time scale) e **barra** genérica `boss_barra.tscn` (nome, cor, rastro branco, marcador de fase);
  - invulnerável durante a entrada;
  - "só ataca de novo com o corpo inteiro escondido/pronto";
  - janela de ataque clara (ex.: cabeça presa, com dano multiplicado).
- O que **não** funcionou: `Monte_Terra` (montinho de terra andando no rastro) ficou esquisito e foi removido. Divisão do boss em 2 corpos foi testada e o usuário preferiu **1 corpo só**.

## Arquivos de apoio que eu faço

- **Texturas PNG com alfa** (PIL), estilo low-poly facetado, **brancas** quando o Godot vai pintar.
- **Malhas de efeito GLB** (bpy):
  - emissivas;
  - animação em trilha NLA **mutada antes de exportar**, para a pose de repouso sair escondida (escala 0,001);
  - raiz com nome claro;
  - tamanho base de 1 m, para o Ziva escalar.
- **Sons** (numpy/scipy, WAV 44,1 kHz estéreo):
  - sincronizados com os eventos;
  - volume por RMS;
  - loops com chunk `smpl`;
  - um prompt de sons separado.
- **Preview** (render ou desenho de cima) mostrando como deve ficar no jogo.

## Braços / mãos nuas em primeira pessoa (estado)

**Arquivos no projeto:**
- `scripts/player/bracos_fps.gd` (`class_name BracosFps`): máquina de estados ESCONDIDO / GUARDA / SOCANDO / VOLTANDO / PEGANDO / GESTO, com mola do pulo;
- `scenes/player/hand_models.tscn`: o `HandsVisual/bracos` instancia `res://Blender/bracos_novo/bracos.glb`; o material `Mat_hand_cel` é toon;
- `scripts/player/player.gd`: chama `configurar`, `atualizar_pulo(no_chao, pulou, vel_y)`, `registrar_clique_soco`, `request_pegar`, `esconder` e `mostrar`. A mão nua é `_mao_nua_ativa()`.

**Hierarquia:** `Head/Camera3D/HandPivot` (o bobbing de andar mexe aqui) `> HandModels` (escala 3; o pulo mexe aqui) `> HandsVisual` + os visuais das ferramentas e armas (Axe, Pickaxe…, irmãos). Enxada, pá e os visuais das armas placeholder foram removidos.

**Regras decididas:**
- o golpe da mão nua (inimigo, árvore, pedra, construção) sai **só no impacto** da animação, pelo sinal `soco_impacto`, nunca no clique. Interações de clique (caça-níquel, mesa, monumento) continuam imediatas;
- `velocidade_soco` vai como `custom_speed` no `play()`. O impacto é checado em `current_animation_position` (tempo da animação), então continua alinhado em qualquer velocidade;
- com 4 s sem bater, as mãos se escondem. O primeiro clique faz `02_0_Surgir_Soco` (surge já socando). Trocar para o slot vazio não mostra as mãos;
- pegar do chão funciona com **qualquer item**: recolhe o item (tween para baixo ou `00_Escondido`) → `03_2_Pegar_Escondido` → devolve o item. O usuário prefere trocar de pose **passando pelo escondido**;
- poses próprias por item/arma virão depois. Hoje os itens sem visual mostram as mãos em guarda.

**Soco rápido com arma (V):** ação `Soco_Esquerdo_Arma` (0,40 s, impacto 0,167 s, chave **só nos ossos `_L`**) tocada num **segundo AnimationPlayer** (`AnimEsquerda`, biblioteca só com as trilhas `_L`, `deterministic = false`, `process_priority` e `process_physics_priority` +1, blend 0). A direita continua na pose da arma e dá para atirar durante o soco. Bloqueado no saque/recarga; cortado ao guardar ou pegar do chão. Mesmo ShapeCast do soco de mão nua (`_golpe_shapecast()`), +12 de essência. Pendente: punho aparece pouco (C16).

**Tempos dos .glb (corrigidos):** os .glb começavam com 1 quadro parado; agora soco 0,167 s, pegar 0,467 s, `Revolver_Atirar` 0,1 s, `Revolver_Pose` 2,0 s. `bracos.glb` e `revolver.glb` **sempre juntos**.

**Prompts entregues:** `PROMPT_ZIVA_MAOS.md` → `_V2` (glb novo, material, contorno, gestos, pulo por mola) → `_V3` (soco no ritmo, esconder sozinho, pegar com item) → `PROMPT_ZIVA_SOCO_ESQUERDO`.

## Armas animadas na mão (revólver R08, primeira)

**Montagem no Godot (funcionou):** `HandsVisual/bracos/BracosRig/Skeleton3D/EncaixeArma` (`BoneAttachment3D`, bone `Arma_R`) `> Revolver` (instância de `res://Blender/bracos_novo/revolver.glb`, **transform zerado**; a escala 3 vem do `HandModels`). Clarão e origem visual do tiro: `BoneAttachment3D` no osso `Cano` do revólver.

**Controlador `ArmaFps`** (`PROMPT_ZIVA_REVOLVER.md`): genérico por `prefixo`. Toca o mesmo nome nos dois `AnimationPlayer` (braços e arma), com a mesma velocidade. A arma usa **sempre blend 0**. As velocidades de tiro, recarga, saque e guardar são calculadas pela **duração lida da animação** (`get_animation(nome).length`) e pelos tempos do `WeaponData` — nada de duração fixa no código.

Com a arma na mão, o `BracosFps` fica pausado. Pegar do chão com arma: `_Guardar` → `03_2_Pegar_Escondido` → `_Sacar`.

**Lição:** quando algo aparece errado no jogo, **amplie o print antes de culpar o código do Ziva**. No revólver, o encaixe estava certo e o erro era meu (pose ajustada numa câmera diferente da do jogo e arma girada para o lado). Mandei um prompt de “correção” desnecessário.

## Estado atual dos bosses/objetos

- **Ordem dos bosses:** 1 Tomate (Planície) → 2 Uva-morcego (Floresta, libera fase 2) → 3 Dragão-Pitaya → 4 Batata-golem (Pedreira, refazer) → 5 Final (ideia: **deus no céu**; existe a cena `deus_colheita.tscn`; reserva: Espantalho Vulcânico) · ★ secreto: Totem de Melancia.
- **Santuários** (`SHRINE_DEFS`, pilares de boss): Tomate Gigante, Hidra Picante (placeholder), Golem de Raiz (**não** é o Batata-golem), Espantalho Vulcânico, Deus da Colheita Abissal. Hoje exigem 3 sementes de chefe (tier 1, `# TEMP`) e **ficam no mapa** para reinvocar (bloqueado com o boss vivo). **Rework total pendente (E08).** Todos os bosses registram derrota em `defeated_bosses` (Totem sem subir o tier).
- **Caça-níquel de pedra** (`caçaniqueis\`): roleta de armas, fogo por raridade, 4 explosões e sons. Pronto. Hoje sorteia só o revólver (Comum).
- **Bigorna:** abas Fabricação, **Fundir**, **Desmanchar**. **Barraca de Venda:** construída na bancada (20 madeira + 10 pedra).
- **Dragão-Pitaya** (`dragao_pitaya\`): verme segmentado com juntas em bola, escala 3, um corpo só.
  - Cava e persegue o jogador.
  - **Erupção** sob o jogador.
  - **Mergulho**: sempre prende a cabeça (janela, cabeça × 2,5).
  - **Tabuleiro de Raios**, o xadrez redondo: casas de 8 m, raio ~36 m, 5 ondas, aviso de 1,2 s, chance de 1/3 com garantia depois de 2. Depois dele o mergulho é garantido.
  - Bolas de choque no ar.
  - Escudo de campo elétrico: bater fora da janela é bloqueado e solta o campo.
  - Entrada com título "O Devorador do Pomar", barra rosa `#E0337E` e drops.
  - Prompts já entregues: `PROMPT_ZIVA`, `_SONS`, `_AJUSTES`, `_FASES`, `_SONS_FASES`, `_XADREZ`, `_XADREZ_AJUSTE`, `_XADREZ_REDONDO` e `_XADREZ_FINAL`.
- **Pendentes:** Tomate Boss, Uva-morcego, Milho e Batata-golem (refazer), cada um com sons + prompt Ziva. A **entrada de boss** deve ser aplicada a todos os bosses. Rework dos santuários. Como mostrar dano em inimigos comuns (I05). Revólver v2 no guia de estilo (em produção no chat de modelagem).

Atualize esta seção (e o repositório) quando algo mudar.
