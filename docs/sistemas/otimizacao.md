# Otimização (desempenho)

> Status: 🔴 pendente — olhar no futuro. Registrado em nov/2026.

## Problema
No notebook Lenovo antigo do Gustavo (menos potente) o jogo **trava bastante, com FPS bem baixo**.
Público de jogos tipo Muck/Terraria joga muito em PC fraco: desempenho é requisito, não luxo.

## A preencher quando formos olhar
- Especificações do notebook (processador, placa de vídeo, RAM) e FPS medido em cada situação (parado, andando, noite com horda, boss).
- Perfil do Godot (Debugger → Monitores / Profiler) para achar o que pesa de verdade, **antes** de mudar qualquer coisa.

## Suspeitos comuns (a confirmar com medição)
- Grama e vegetação espalhada (quantidade de instâncias, sombras).
- Terreno procedural (tamanho, colisão, LOD).
- Sombras em tempo real, luz dinâmica, shader de céu customizado.
- Partículas e decals (efeitos de boss, impacto novo da F2.1).
- Quantidade de inimigos ativos e scripts rodando todo frame (`_process`/`_physics_process`).
- Raycasts por frame (projéteis, decals).

## Ideias de solução (depois de medir)
- Menu de **qualidade gráfica** real (a aba de gráficos hoje é placeholder): sombras, distância de visão, densidade de grama, escala de resolução (FSR), limite de FPS.
- MultiMesh para grama/pedras, LOD e distância de desaparecimento.
- Desligar processamento de coisas longe do jogador.
- Pools para efeitos (já é padrão do jogo).
