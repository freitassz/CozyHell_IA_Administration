# PROMPT ZIVA — Lote 4B: água com cara de água, nadar, fôlego e o Guardião das Águas

## Contexto
Hoje a água é "um terreno plano que sobe e desce". Queremos **água de verdade no estilo do jogo** (stylizada, leve), **nadar**, **barra de fôlego** e um **inimigo que mata quem tenta sair da ilha nadando**. **Desempenho é crítico** (notebook fraco): sem reflexo/refração de tela cheia; **opção de qualidade** e **FPS reportado**.
- Modo rápido, com validador. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.

## ETAPA 0 — Relatório curto
Como a água/oceano é feito hoje (malha, shader, nível), onde o jogador entra na água hoje (física, velocidade), e a posição da costa (função de distância à terra, se existir).

## 1. Água stylizada
- Malha de água **só ao redor do jogador** (grade ⚙️ 150 m, subdividida e centralizada no jogador, "clipmap" simples), nível fixo do mar.
- Visual (shader barato): cor **rasa clara** `#7FD6E6` → **funda** `#2F8FC4` pela **profundidade** (use `depth_texture`), **espuma branca** suave na beira (diferença de profundidade), **ondas suaves** por deslocamento de vértices (⚙️ amplitude 0,25 m) e brilho/sparkle por normais animadas; translucidez ⚙️ 0,75. Estilo facetado leve: normais em passos, nada realista demais.
- **Qualidade** (menu de pausa, padrão **Média**): Baixa = cor por profundidade + espuma, sem ondas; Média = + ondas; Alta = + sparkle e transparência melhor. Reporte FPS de cada uma.

## 2. Nadar
- Em água com profundidade > ⚙️ 1,1 m o jogador **nada**: flutua na superfície, velocidade ⚙️ 3,5 m/s, sem correr/pular normal; **pular** dá uma braçada; **agachar** (mantendo) **mergulha** a ⚙️ 2,5 m/s. Raso (< 1,1 m): anda mais devagar (⚙️ ×0,7) com respingos.
- Efeitos: respingo ao entrar, ondas circulares ao redor, **submerso**: névoa/tinta azul (⚙️ opacidade 0,35, bordas) e bolhas. Sem texto.
- Armas na água: só **soco** e golpes funcionam; tiro **não** (⚙️), e a arma some da mão ao mergulhar.

## 3. Barra de fôlego
- Só aparece com a **cabeça submersa**: ícone de **bolhas** + barra azul **fina** (sob a stamina), ⚙️ 15 s. Vazia: **8 de dano/s** até emergir. Recupera ⚙️ 3× mais rápido na superfície.

## 4. Guardião das Águas (mata quem sai da ilha)
- Se o jogador estiver a mais de ⚙️ 60 m da costa **em água funda**, o **Guardião das Águas** surge: uma **barbatana grande** (placeholder azul-escuro facetado, nada perto do preto) que **circula** o jogador deixando **marolas** e uma **sombra** na água. Depois de ⚙️ 6 s de aviso, **ataca**: 35 de dano a cada ⚙️ 1,5 s (morte em ~4 s) até o jogador voltar a ⚙️ 40 m da costa, quando ele **some** (afunda sem texto). Mesmo comportamento no Soneca e Pesadelo (a morte segue as regras do modo).
- Sinais: `guardiao_surgiu`, `guardiao_atacou`, `guardiao_sumiu`, `entrou_agua`, `mergulhou`, `emergiu`.
- Não aparece se o jogador estiver em barco/(futuro) ou perto da costa.

## Teste
`dev/validate_lote4b`: profundidade → nada/raso, fôlego só submerso e dano ao zerar, qualidade Baixa/Média/Alta, Guardião surge > 60 m, aviso 6 s, dano a cada 1,5 s, some a < 40 m, armas bloqueadas, FPS por qualidade. E `dev/agua_preview.tscn`. Placar.

## Checklist
- [ ] Água stylizada local ao jogador com 3 qualidades · [ ] Nadar/mergulhar com efeitos · [ ] Fôlego (só submerso)
- [ ] Guardião das Águas com aviso e dano · [ ] FPS reportado · [ ] Validador + prévia · Nada além disso foi alterado
