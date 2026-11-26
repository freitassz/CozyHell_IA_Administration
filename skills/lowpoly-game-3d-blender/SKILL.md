---
name: "lowpoly-game-3d-blender"
description: "Criar inimigos, bosses, braços de primeira pessoa, armas e objetos 3D low-poly para o jogo CozyHell3D (Godot 4) no Blender via bpy: modelo, rig, animações em etapas, explosões, sons sintetizados e prompts para o Ziva AI."
---

# Criação 3D low-poly para jogo (Blender via Python) + sons + prompts Ziva

O usuário (Gustavo) faz o jogo **CozyHell3D** no **Godot 4**. Ele cria personagens a partir de imagens ou folhas de referência: inimigos, bosses, frutas e vegetais com personalidade, e objetos de jogo. Ele escreve em português.

O que ele quer:
- resultado fiel à referência;
- testado visualmente;
- com rig e animações prontas para a engine;
- e, cada vez mais, **sons** e **prompts para o Ziva AI**, uma IA que escreve o código Godot no projeto dele.

Ele gosta de trabalhar **por etapas**, organizado e sem pular de assunto. Use lista de tarefas e entregue por etapa.

## Como esta skill é usada agora (ler primeiro)

- Esta skill roda no **chat de modelagem** (com acesso à pasta do jogo). O **chat de administração** organiza o projeto no repositório **`freitassz/CozyHell_IA_Administration`** e escreve os pedidos em `prompts/blender/PROMPT_BLENDER_<ASSUNTO>.md`.
- **Em conflito, o repositório vence esta skill** (`docs/jogo/decisoes.md`, `docs/armas/guia-estilo.md`).
- O **prompt do Ziva** agora é escrito no chat de administração. Aqui, ao terminar, **devolva os dados** para ele: nomes exatos das ações, duração (s) e nº de quadros, tempos de impacto/eventos, ossos com chave, ossos `FX_*` com posição Godot, nomes de materiais especiais e qualquer cuidado no Godot.
- **A aparência de cada arma/modelo quem descreve é o Gustavo** (referências e explicação no próprio chat). O pedido do chat de administração traz só as **regras técnicas** e o **estilo geral**.

## Ambiente

- Não há Blender instalado. Instale com `pip install bpy --break-system-packages` (bpy 5.x, Python 3.13) e rode os scripts com `python3 script.py`.
- **Nunca** dê a um script o nome de um módulo da stdlib. Um `inspect.py` derrubou o Blender. Deixe os scripts numa pasta própria.
- Render: `addon_utils.enable('cycles')`, engine CYCLES, device CPU.
  - Use 12 a 16 samples para iterar e 24 a 40 no final.
  - Deixe o denoise ligado e `view_transform = 'Standard'`.
  - Um render 700x900 leva uns 10 s. Divida lotes grandes para caber em uns 590 s por comando.
- Avisos inofensivos:
  - Draco/MeshOptimizer no export GLB;
  - "active Vertex Color will not be exported" (vem dos materiais que não usam a cor);
  - DeprecationWarning de `use_nodes` no Blender 5.
- Cada asset é um script `.py` autocontido que gera `.blend`, `.glb` e renders. Variáveis de ambiente: `OUT_DIR`, `SAMPLES`, `VIEWS`, `RENDER=0` (só exporta) e `ZOOM="nome,az,el,ortho,tx,ty,tz;..."` para closes.
- O container é temporário. Os `.py` de cada asset ficam **na pasta do usuário**. Para mexer num asset antigo numa conversa nova, busque o `.py` pela ponte do computador (`device_stage_files`) ou peça o anexo.

## Pasta do projeto e entrega

- Pasta de assets (dentro do projeto Godot): `C:\Users\Gustavo\Documents\jogo 3d\CozyHell3D\3dddddd\Blender`.
  - O Godot importa sozinho qualquer `.glb` ou `.blend` que estiver lá.
  - Não deixe versões duplicadas ou velhas de GLB nessa pasta, porque viram imports duplicados.
- Entregue numa **subpasta por asset**, com o nome que ele pedir (ex.: `caçaniqueis\`). Sons ficam em `subpasta\sons\`.
  - Prepare os arquivos em `/mnt/user-data/outputs/<pasta>/`.
  - Grave no PC com `device_commit_files`.
  - Mande também no chat com `SendUserFile`.
- Há outros modelos na pasta que **não** foram feitos com esta skill: PepperBoss (+ Fireball/FireBarrier), CowMellon, CowMellonBossTikiTiki, Carrot, Onion, pepper, Tomato, House, tree, Bush, Stone, GoldStone, hole, Little_Rocks e Stick. Eles podem ganhar sons e prompts depois.

## Fluxo obrigatório de modelagem

1. **Analise a referência antes de modelar.**
   - Liste formas, cores, proporções, partes separadas e poses.
   - Meça em pixels e converta para metros.
2. **Modele 100% procedural** (bmesh / from_pydata), low-poly facetado, com `use_smooth = False`.
3. **Renderize as MESMAS vistas da referência** e monte uma prancha rotulada com PIL. Para personagens alongados, faça a prancha referência x render lado a lado.
4. **Compare e itere sempre.**
   - Use máscara de silhueta e zoom em detalhes.
   - Diga ao usuário o que encontrou em cada rodada.
5. **Entregue**:
   - prancha de vistas, `.blend`, `.glb`, `.py`;
   - quando houver, prancha de animações e mapa de âncoras FX;
   - resposta final curta, em português, dizendo o que mudou.

## Preferências do usuário

- **Estilo:**
  - low-poly facetado, com cores vivas e chapadas;
  - materiais Principled simples, com emissão para brilhos;
  - escala real em metros: boss ~5 m, inimigo comum ~1,7 m, objeto ~2,4 m.
- **Fidelidade à referência** é prioridade. Se a referência for inconsistente, escolha a leitura mais coerente e avise.
- **Partes que flutuam** (ex.: olho) são objetos separados, presos a um osso por bone-parent.
- **Projéteis** são objeto e GLB separados. Inclua um osso `Muzzle` como ponto de spawn.
- **Variações** (menos faces etc.) vão em **arquivos separados** (`*_v2.*`), sem mexer no original. Informe os triângulos antes x depois.
- **Retrabalho de um asset** pedido pelo usuário (ex.: caça-níquel v2) substitui o anterior na pasta do jogo. O antigo fica só no zip ou no chat.
- **Técnicas que ele cita:** bmesh, Bevel, Subdivision, Simple Deform, Skin, Decimate, inset. Use quando fizer sentido e **seja honesto**: nunca liste no cabeçalho do script uma técnica que não foi usada.
- **Detalhes decorativos** devem ser variados. Ele achou "sem graça" um padrão repetitivo. Use motivos diferentes por face, sem sair do low-poly.
- Ele **não gostou** da folha de referência da batata-golem ("paia"). Folhas para outra IA precisam de mais cuidado: confirme o estilo antes.
- **Ele se preocupa com tokens.** Para algo novo, primeiro alinhe a referência e mande **uma imagem de teste** (render pequeno, 1 pose) antes de construir rig e animações. Itere em passos curtos, com uma mudança por rodada. Não faça buscas, renders ou variações grandes sem necessidade.
- **Quando ele reclamar de algo visual, pergunte ou teste o que de fato incomoda** antes de refazer tudo. Nos braços, a queixa "juntas estranhas" era na verdade o polegar e o pulso dobrado na pose; a malha unificada por remesh foi rejeitada e revertida.

## Rig (lições aprendidas)

- Use hierarquia simples: `Root > Main/Hover/Spin > Body > partes`. Ossos de controle e de FX levam `use_deform=False`.
- **Evite IK em pernas curtas.** Prefira 1 osso por perna (FK).
- **Pivô do corpo no chão** (head do Body em z=0). Para girar no ar, use um osso `Spin` com pivô no centro.
- As pernas acompanham a parte onde estão presas (ex.: filhas do Jaw).
- **Boca Pac-Man:**
  - casca dupla (externa colorida + interna escura), cortada na boca, com lábio ligando as duas;
  - dobradiça traseira (Upper/Jaw);
  - topo das pernas **entre as cascas**.
- **Expressões, brilhos e rachaduras:** use shape key dirigida por um osso CTRL (driver AVERAGE, `LOC_Y` 0..1). O GLB exporta isso como morph animado.
  - Para **brilho que acende**, faça um disco emissivo escondido atrás da superfície que avança e cresce no shape key.
  - Para **rachaduras**, use faixas emissivas enterradas que sobem no shape key. Deixe a base funda e longe dos chanfros.
- **Não use constraints** em ossos animados, porque fazem bake no GLB.
- Mundo para local: `R_local = M^-1 @ R_world @ M`, com `M = bone.matrix_local.to_3x3()`. Faça o mesmo para deslocamentos. Escala: mapeie os eixos do osso.
- Chave **todos** os ossos em todo key. Use quaternion com correção de hemisfério (`LASTQ`) e zere a pose antes de trocar de action.
- **Ossos-âncora `FX_*`** (não-deform) marcam onde o jogo coloca fogo, fumaça, explosão, spawn de item e tela. Eles viram joints no GLB e o Godot usa com `BoneAttachment3D`.

## Animações

- **Divida em etapas** que o código encadeia, por exemplo:
  - `Jump_Start` / `Jump_Air` / `Jump_Land`
  - `Attack_Open` / `Attack_Hold` (loop) / `Attack_Close`
  - `Stun_Start` / `Stun_Loop` / `Stun_End`
  - `Death_Start` + explosão
  - `Lever_Pull` > `Spin_Loop` > `Spin_Stop` > `Fail` ou `Explode_Start_*`
- **Não desloque o personagem** em pulo, queda ou voo. A altura vem do código; a animação só inclina e achata (squash).
- O último quadro de uma etapa é igual ao primeiro da seguinte, e os loops fecham sem salto. **Verifique por código** (diferença de `matrix_basis` = 0) e informe.
- Guarde as actions com `use_fake_user` e em trilhas NLA mutadas. Exporte com `export_animation_mode='ACTIONS'` e 24 fps. Confira no JSON do GLB: nomes, joints, morph targets e COLOR_0/TEXCOORD_0.
- **Mudança de cor de material** (ex.: tomate ficando verde) **não exporta** por nó Mix. Isso é feito no código do jogo; avise o usuário.

## Explosão em pedaços (GLB separado)

1. Gere os pedaços da pose final do `*_Start`, com a malha avaliada: k-means sobre os centros das faces, separando por parte.
2. Crie uma **cunha** para o centro, com interior escuro.
3. Simule a física em Python: gravidade, quique 0,25, giro e encolher no fim.
4. Crie **uma trilha NLA por nível**, com o mesmo nome em todos os objetos. Exporte com `export_animation_mode='NLA_TRACKS'`.
5. Chave os objetos de efeito (clarões, onda de choque) em **todos** os níveis, com escala 0,001 quando o nível não usa.
6. **Mute todas as trilhas antes de exportar.** O exportador continua gerando 1 animação por trilha, e a pose de repouso no GLB fica limpa (efeitos escondidos).
7. A troca no jogo é invisível: o GLB de explosão é instanciado no mesmo transform da máquina.
8. Para ler curvas no Blender 5:
   - use `action.layers[0].strips[0].channelbag(strip.action_slot).fcurves`;
   - alternar o mute depois de reabrir o .blend **não** reavalia o NLA.

## Relevos e detalhes (lições)

- Use uma classe `Plane(O, U, V, N)` para relevos em qualquer face, inclusive inclinada. Ela tem:
  - `line`: polilinha em faixa;
  - `poly`: polígono convexo;
  - `rect`, `disc`, `frame`;
  - `ringr`: anel.
- **Polilinha em relevo com cantos em meia-esquadria.** Caixas sobrepostas por segmento criam faces coplanares: cantos pretos no Cycles e z-fighting no Godot. Também gastam mais triângulos.
- Motivos já prontos:
  - greguinha (meander);
  - degrau-gancho (xicalcoliuhqui);
  - gancho duplo;
  - friso em degraus (onda quadrada);
  - quadrados concêntricos;
  - disco solar com raios;
  - pirâmide escalonada com escadaria e templo;
  - friso de discos;
  - cravos.
- Blocos encostados devem **sobrepor** um pouco, para não abrir fresta.
- Elementos na frente de uma face precisam sair o suficiente para não ficarem enterrados.

## Godot (para prompts e conferência)

- Coordenadas: Blender (x, y, z) → Godot (x, z, −y). Modele com a **frente em −Y no Blender**, que vira **+Z no Godot**.
- A cor por vértice vai como COLOR_0. Se a pedra aparecer branca, ligue `vertex_color_use_as_albedo`.
- Tela ou superfície para textura dinâmica:
  - use um material próprio, com UV 0–1 e cor de vértice branca;
  - o glTF inverte o V, então o canto superior-esquerdo vira UV (0,0) no Godot;
  - confira no GLB.
- Despeje um `*_dados.json` com: posições FX em coords Godot, durações (`(quadros-1)/24`), materiais e dados da tela. Use ele para escrever o prompt.
- **Mapa de âncoras FX:**
  1. Renderize 2 vistas (frente-esquerda e costas-direita).
  2. Projete as cabeças dos ossos com `world_to_camera_view`.
  3. Teste a visibilidade com `scene.ray_cast`.
  4. Desenhe os rótulos com PIL: círculo cheio = visível, tracejado = escondido.

## Prompts para o Ziva AI

> Hoje os prompts do Ziva são escritos no **chat de administração**. Use esta seção só se o Gustavo pedir um prompt aqui; o normal é devolver os dados.

- O texto é em português e organizado em **ETAPAS numeradas**, cada uma com o que fazer e um teste. Termine com um checklist.
- Comece com contexto e fluxo do jogo, depois uma tabela de arquivos e orientação.
- Inclua os **dados exatos**:
  - animações com duração e loop;
  - ossos FX com posição Godot e uso;
  - materiais por `resource_name`.
- Regras que funcionaram:
  - **Não alterar o .glb.** Usar uma cena wrapper e achar nós por tipo (`find_children`).
  - Usar `BoneAttachment3D` nos `FX_*`.
  - Os emissores de partículas ficam **fora do modelo**, num nó `FX`, e copiam **só a posição**. Assim o fogo sobe no mundo e sobrevive quando o modelo some.
  - Morphs já vêm animados; não animar por código.
  - Trocar cor por `set_surface_override_material`.
  - Loop por código: `loop_mode = LOOP_LINEAR`. Encadear pelo `animation_finished`. Sair de loop com blend de 0,1 s.
  - Parâmetros em `@export`: chances, pesos, tempos e listas de cenas.
- **Prompt só de uma parte** (ex.: só sons), quando o resto já foi implementado:
  - diga "não mude nada além disso";
  - mapeie cada `anim.play(...)` existente para a chamada nova.
- **Cores de raridade do jogo:** comum `#3DDC4A` (verde), raro `#2F8BFF` (azul), épico `#A23DFF` (roxo), lendário `#FFD21F` (amarelo).

## Sons (sintetizados com numpy/scipy, sem gravação nem IA de áudio)

- Formato: WAV 44,1 kHz, 16-bit, estéreo.
- Peças prontas:
  - `clack` (estalo de pedra: ruído + ressonâncias);
  - `thump` (baque com queda de pitch + tanh);
  - `gravel`;
  - `creak` (stick-slip em bandpass);
  - `rumble` (ruído browniano em lowpass);
  - `whine` (energia subindo, com harmônicos);
  - `rattle`;
  - `crackle`;
  - `suck` (sucção antes do estouro);
  - `boom(size)`;
  - `gong` (parciais inarmônicos);
  - `cough`.
- Espaço: reverb leve por `fftconvolve` com IR de ruído decaindo. Use pan equal-power.
- **Sincronia com animação:** o tempo do evento é `(quadro-1)/24`. Explosões leem os momentos em que cada pedaço toca o chão direto das fcurves da trilha NLA (`impactos.json`) e tocam as pedras nesses instantes.
- **Volume coerente por RMS**, com limitador tanh. Alvos já usados (dB RMS):
  - alavanca −19, roleta −22, trava −19, erro −22;
  - início comum −27, raro −23, épico −21, lendário −19;
  - explosão comum −23, rara −19, épica −15,5, lendária −12,5.
- **Loop sem emenda:**
  - para ruído periódico, repita o ruído 3x, filtre e pegue o pedaço do meio;
  - grave um chunk `smpl` com o ponto de loop, para o Godot ("Detect From WAV") repetir sozinho.
- **Eu não escuto o áudio.** Valide por forma de onda, espectrograma, `ffprobe` e níveis, e diga isso ao usuário.

## Trechos úteis

- **Builder de malha:**
  - listas V/F/M/W/FC e UV por face;
  - shape keys por vértice;
  - normal de Newell com `expect(fc)` para orientar a face (inverta junto com a UV).
- `bmesh.ops.inset_individual` retorna as faces da BORDA.
- `subdivide_edges(use_sphere=True)` colapsa vértices.
- `bmesh.ops.bevel` para chanfros; `polyfill` para contornos.
- Para enquadrar, não use `camera_fit_coords` em proporções largas. Projete com `world_to_camera_view`.
- Câmera: `(-d).to_track_quat('-Z','Y')`. O sun acompanha a câmera. Chão com grade por nós (FRACT/LESS_THAN).
- Para ver o albedo puro num diagnóstico, troque o material por Emission da cor de vértice.

## Assets já feitos (referência de estilo e estado)

- **Dragão-pitaya:**
  - corpo magenta segmentado (loft de 10 lados);
  - espinhos dente-de-serra com degradê rosa→verde;
  - olhos brancos com sementes pretas e anel no pescoço.
  - **Segmentado** para boss em corrente (`pitaya_dragon_segments`): Head / Body / Tail, com a frente em +Y e origens nos centros das seções de encaixe. As seções batem, com uma luva interna de 0,18 m e 4% mais fina. O corte da cabeça fica em 2,32: em 2,30 cai num anel e duplica vértices. Sem animação; o movimento é por código.
- **Tomate Boss** (~5 m):
  - modelo:
    - 6 gomos, cálice de 6 folhas e olhos brancos;
    - boca Pac-Man de casca dupla;
    - 4 pernas largas em cima e finas e arredondadas embaixo;
    - pálpebras bravas.
  - animações: Idle, `Jump_Start/Air/Land`, `Attack_Open/Hold/Close`, `Stun_Start/Loop/End` (cai de pernas abertas, olhos fechados; o verde-claro é feito no jogo) e `Death_Start`;
  - explosão: `tomato_boss_explosion.glb`.
- **Milho inimigo** (~1,7 m, flutua):
  - modelo:
    - espiga em barril com grãos por inset;
    - palha lateral;
    - 4 braços e 4 pernas-tentáculo;
    - olho de amêndoa separado e emissivo, com pupila em fenda.
  - animações: Idle, Walk, `Attack_Start/Shoot/Attack_End`, Hit e Death;
  - projétil: `corn_kernel_projectile.glb`.
  - **v2**: menos faces e ataque mais inclinado.
- **Uva-morcego** (boss, envergadura ~6 m):
  - modelo:
    - corpo em icosfera e olho com shape key `EyeRed` (via `CTRL_Rage`);
    - asas-folha com 2 ossos cada;
    - caule e 5 uvas.
  - origem no centro, com o voo feito por código.
  - animações:
    - Idle e Wander;
    - `Attack_Start/Attack_Loop`;
    - `Dash_Start/Dash_Loop`, `Dash_Hit` (→ Wander) e `Dash_Miss` (→ `Fallen_Loop`);
    - `Fallen_Recover`.
  - projétil: `grape_projectile.glb`.
- **Caça-níquel de pedra** (`caçaniqueis\`, ~2,4 m, alavanca em +X):
  - modelo:
    - ídolo no topo, tela inclinada com material `TelaRoleta` e glifo retrátil (osso `Glifo`);
    - laterais com motivos variados.
  - rig: `Root > Spin > Body > Lever / Idol / Glifo / FX_*`, com `CTRL_Glow`/`CTRL_Crack` dirigindo os morphs `EyeGlow`/`Cracks`.
  - fogo: **sem fogo no modelo**. O fogo é feito no Godot em 7 âncoras `FX_Fogo_*`. Outras âncoras: `FX_Tela`, `FX_Fumaca`, `FX_Explosao`, `FX_Item`.
  - animações:
    - `Lever_Pull`, `Spin_Loop`, `Spin_Stop` e `Fail`;
    - `Explode_Start_Comum/Raro/Epico/Lendario`;
    - `Fall_Start/Loop/Impact`.
  - explosões: `cacaniquel_explosao.glb`, com `Explode_Comum` (só desmonta), `Explode_Raro`, `Explode_Epico` e `Explode_Lendario` (com onda de choque).
  - 12 sons em `sons\`, mais `PROMPT_ZIVA.md` (completo) e `PROMPT_ZIVA_SONS.md` (só sons). Já implementado pelo Ziva.
- **Batata-golem**: só uma folha de referência, que foi reprovada. Está pendente refazer.

## Braços de primeira pessoa (`Blender\bracos_novo\`, script atual `bracos_v5.py`; o v4 é a base sem arma)

**Estilo aprovado** (depois de várias tentativas rejeitadas: braço realista com dedos separados e juntas em bola, braço "geométrico" de cubos com luva, e malha única por remesh):
- peças arredondadas facetadas: seção de 8 lados quase regular e pontas abauladas;
- mão grande, com palma em 1 peça e as costas da mão um pouco mais altas que o antebraço;
- **indicador e polegar separados; médio, anelar e mínimo num bloco só**;
- cada dedo é **1 peça que dobra no meio** por pesos (base → ponta), e a **raiz nasce de dentro da palma** (pesos Mão → dedo);
- polegar com raiz um pouco mais gorda (monte, `monte=1.2`);
- braço e antebraço em gomos grossos (cartunesco), com o antebraço afinando e se misturando com a Mão no pulso;
- pele `#F2A48C` e palma/lado de dentro dos dedos `#E88A78` por **cor de vértice** (COLOR_0);
- material fosco (roughness 1, specular 0), `use_smooth=True` + `mesh.set_sharp_from_angle(55°)`. No Godot: toon + contorno por casco invertido (`next_pass`, `grow`).

**Rig e poses:**
- ossos por lado (`_R`/`_L`): `Raiz > Braco > Antebraco > Mao > Indicador1/2, Dedos1/2, Polegar1/2`;
- poses por **IK analítico de 2 ossos**: o alvo da mão é pulso + `fwd` (pulso→nós dos dedos) + `back` (costas da mão) + polo do cotovelo;
- `reto=True` alinha a mão ao antebraço (pulso reto). Foi o que deixou a pose de bater boa: costas da mão para cima e polegar cruzado embaixo `(50, -40, 70, 40)`;
- presets de mão: aberta, espalmada, relaxada, punho, garra, apontar, joinha;
- **lado esquerdo = espelho:** as rotações locais dos dedos viram `Quaternion((w, x, -y, -z))`. Sem isso, o polegar e a abdução do lado esquerdo saem errados;
- amasso no impacto = escala do osso `Mao`; chave `location`/`rotation`/`scale` em todo key.

**Câmera e escala:**
- câmera **calibrada pelo print do jogo**: FOV vertical ~68°, posição `(0, 0.05, 0.02)` olhando +Y (no `revolver_anim.py`, `cam_fps`; env `CAMPOS`/`CAMFOV`). A câmera antiga (origem, FOV 60) **não batia com o jogo**: a arma parecia certa na prévia e no jogo ficava grande e torta;
- para calibrar de novo: render Workbench com cores chapadas, máscara de cor da arma e da mão no print, e busca em grade de FOV/rotação/posição pelo maior IoU (~20 s);
- no projeto, o `HandModels` tem **escala 3** e as ferramentas são irmãs dele, por isso **o glb sai em escala 1** (`ESC=1`).

**Exportação:** use `export_force_sampling=False`, para cada animação gravar **só os ossos que tem chave**. Com amostragem forçada, todas as animações gravam todos os ossos e uma camada apaga a outra.

**Animações (30 fps, emendas verificadas = 0):**
- `00_Escondido`, `01_0_Surgir`, `01_Pose_Bater` (loop);
- `02_0_Surgir_Soco` (impacto 0,233 s), `02_1_Soco_Direito`, `02_1_2_Soco_Esquerdo`, `02_1_3_Soco_Direito_Combo` (impacto 0,167 s);
- `02_2_Volta_Direito/Esquerdo` (0,433 s, com exagero no final);
- `03_Pegar_Chao` e `03_2_Pegar_Escondido` (pega aos 0,467 s);
- `05_Apontar`, `06_Joinha`, `07_Acenar` (loop), `08_Empurrar` (impacto 0,2 s).

- `Soco_Esquerdo_Arma` (nov/2026): 0,40 s, 13 quadros, impacto 0,167 s (quadro 5) com amasso em `Mao_L`; chave **só** em `Braco_L`, `Antebraco_L`, `Mao_L` e dedos `_L` (a `Raiz` é única e fica sem chave). Início e fim = mão esquerda escondida da `Revolver_Pose`. No Godot roda num **segundo AnimationPlayer** (`AnimEsquerda`) por cima da pose da arma. Pendente (C16): o punho aparece pouco — avançar mais para frente/centro sem tapar a mira.
- **Correção de tempo (nov/2026):** as ações dos .glb começavam com 1 quadro parado (impacto saía em 0,2 s em vez de 0,167 s; loops travavam). Corrigido nos dois .glb.

O **pulo não é animação**: é uma mola no código, aplicada no `HandModels`.

## Guia de estilo das armas (aprovado nov/2026 — detalhes em `docs/armas/guia-estilo.md`)

- **Tema:** roça + magia do sono. Armas de fazendeiro velhas, sucateadas, remendadas ("gambiarra da roça"), com toque mágico. **Não são de brinquedo**, mas são **mais leves**; silhueta reconhecível em primeira pessoa.
- **Paleta "sonho feliz":** cores **fortes e claras**; nada perto do preto (só o contorno). Linha geral aprovada: metal pintado claro com tinta descascando, ferrugem como **manchas chapadas**, madeira cor de mel, fitas coloridas nos remendos. As cores exatas de cada arma o Gustavo define.
- **Materiais:** formas puramente de cor (cor por vértice), **sem textura**, poucos detalhes modelados. **Fosco e sem reflexo** (roughness 1, specular 0, metallic 0) — regra que vale para **tudo** no jogo (armas, inimigos, bosses). Brilhos, fumaça e faíscas são **efeitos no Godot**, não no modelo.
- **Raridade** não aparece no modelo (só na cor do nome no jogo).
- **Peça mágica — opcional, criatividade livre** (nenhuma arma é obrigada a ter magia visível; a pistola enferrujada do fazendeiro, por ex., não tem). Quando tiver: objeto/material **separado** (ex.: `EssenciaMagica`) para o Godot acender na recarga e no especial. Variações: frasco/pote/cristal lilás; ideia guardada: cristal que escurece a cada tiro e volta a brilhar na recarga.

## Armas na mão (revólver R08 pronto: `revolver.glb`, `revolver_modelo.py`, `revolver_anim.py`; v2 no guia de estilo em produção)

**Arquitetura (vale para as próximas armas):**
- osso **`Arma_R`** nos braços (filho de `Mao_R`, sem deformar); no Godot vira `BoneAttachment3D` e a arma entra com **transform zerado**;
- a arma é um **glb separado** com rig próprio. As ações têm o **mesmo nome e a mesma duração** nos dois glb (`Revolver_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar`) e o código toca as duas juntas, na mesma velocidade;
- no Blender, as ações da arma se chamam `G_<nome>`. Na exportação: (1) apaga a arma e as `G_` e exporta os braços; (2) reabre o .blend, apaga os braços e as ações deles, renomeia `G_` → nome. Renomeie com `list(bpy.data.actions)`: renomear muda a ordem da coleção e corta o nome duas vezes;
- a geração é **quadro a quadro**: keys com pose da arma no mundo, spec da mão esquerda e mecânica (cão, gatilho, tambor, giro, extrator, cápsulas). A mão direita é derivada da arma (`spec_R = Gw @ A^-1`) e os dois rigs recebem chave em todos os quadros, então nada escorrega.

**Erros que custaram rodadas:**
- **eixo no Godot:** no glTF o osso `Arma_R` fica com Y = frente e Z = cima, mas o modelo exportado fica com frente -Z e cima +Y. Com o transform zerado, a arma apontava para baixo. Correção: na exportação, o objeto `RevolverRig` vai com `rotation_euler = (90°, 0, 0)`. Confira lendo o glb (osso `Cano` em +Y);
- **mirar:** o cano tem que ser **paralelo à câmera** (yaw/pitch ~1,5°) para apontar para o centro da tela. Girar a arma para dentro “para ficar bonito” fez ela mirar para o lado e o usuário reclamou. Nas prévias, desenhe uma cruz no centro da tela;
- **tamanho:** a escala vai no nó raiz exportado (`ESC_ARMA = 1.35`) e o cabo é afinado (`CABO_FINO = 1.2`) para continuar cabendo na mão;
- **símbolo de 6 câmaras:** o tambor pode começar a ação 60° atrás. A arma toca sempre com blend 0, então o pulo é invisível.

**Regras para armas novas (o jogo depende disso):**
- arma de **uma mão**: a mão esquerda fica **escondida na mesma pose do revólver** em todas as ações (o soco rápido `Soco_Esquerdo_Arma` só mexe nos ossos `_L` e serve para qualquer arma assim);
- arma de **duas mãos**: o soco rápido vira **coronhada** (ação própria da arma);
- **sem quadro parado no início** das ações (o 1º quadro já é o começo do movimento); confira que os tempos no .glb batem com o documentado;
- o **recuo do tiro é procedural** no Godot (`forca_recuo`): a ação `_Atirar` pode ser curta/sutil — o código só a usa se `usa_animacao_tiro = true`;
- o código lê a **duração real** das ações para ajustar a velocidade, então pode variar a duração base, mas avise;
- `bracos.glb` e o glb da arma **sempre juntos** quando um mudar.

**Preferências do usuário:**
- arma de mão segurada com **uma mão só**: a esquerda nunca aparece;
- recarga cartunesca com uma mão: tranco abre o tambor, cano para cima derruba as cápsulas, a arma passa por fora da tela e volta cheia, tranco fecha girando;
- o ritmo das animações vem da planilha: `Atirar + Cooldown = 1 / cadencia_tps`, `Recarregar = recarga_s`, `Sacar/Guardar` pelo `tempo_saque_s`. As animações saem com duração base e o código ajusta a velocidade (`PROMPT_ZIVA_REVOLVER.md`).

**Modelo (v1, será substituído pelo v2 no guia de estilo):** perfis laterais extrudados com chanfro (`lateral`/`frontal`/`revolve`/`loft`), facetado (`use_smooth=False`), cor por vértice (aço `#525A5F`, madeira `#8E3B2B`, latão `#D8A73C` — escuro demais para o estilo novo). Ossos: `Raiz > Cao, Gatilho, Tambor > Giro > Carga, Tambor > Extrator, Balas, Cano` (ponta do cano).

**Prévia do contorno:** Freestyle só com `external_contour`. Silhueta e contorno interno desenham vincos que no Godot não aparecem.

## Pacote padrão de cada inimigo/boss (meta do projeto)

1. Modelo + rig + animações em etapas, verificadas.
2. Âncoras FX, `*_dados.json` e mapa FX.
3. Explosão ou morte em GLB separado, se fizer sentido.
4. Sons sincronizados, em `sons\`.
5. `PROMPT_ZIVA.md`: lógica/IA, em etapas, com dados exatos.
6. `PROMPT_ZIVA_SONS.md`: só os sons, ligados aos `anim.play` existentes.
7. Checklist de teste.

## Roteiro combinado (atualizar quando mudar)

O roteiro oficial está no `ROADMAP.md` do repositório. Resumo (nov/2026):
- Fase do **tiro** (F2) fechada. Fase atual: **F3 — guia de estilo**, com o **revólver v2** como primeira arma.
- **Ordem dos bosses (nov/2026):** 1 Tomate → 2 Uva-morcego → 3 Dragão-Pitaya → 4 **Pimenta Ardente** (PepperBoss2; só leva dano atordoado; bola de fogo rebatível) → 5 Final (deus no céu, a criar) · ★ secreto: Totem de Melancia. **Batata-golem foi cortada.** Detalhes: repositório `docs/jogo/progressao.md`.
- **Inimigos por fase:** 1 = Tomate, Cenoura, Pimentão · 2 = Cebola, Milho, **Abóbora (ainda não existe)** · 3 em aberto. Variantes Mutante/Ancestral foram removidas.
- Pendentes de modelagem: revólver v2; ajuste do `Soco_Esquerdo_Arma` (C16); coronhada quando houver arma de duas mãos; armas da lista oficial (depois da revisão da planilha); Batata-golem; Abóbora.

No início de uma conversa nova, confirme com o usuário qual pedido do `prompts/blender/` estamos fazendo.
