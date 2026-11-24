# Pedido para o chat de modelagem — Sons do Tomate Gigante

> Use a skill `lowpoly-game-3d-blender` (seção **Sons**: sintetizados com numpy/scipy, WAV 44,1 kHz 16-bit estéreo, volume por RMS, loops com chunk `smpl`). Pasta: `Blender\<pasta do tomate boss>\sons\`.
> A luta já está pronta no jogo. Os sons serão ligados a sinais que já existem.

## Tom
Boss fofo-infernal: um tomate gigante e mal-humorado. Sons **cartunescos e "molhados"** (squish, splat, boing), nunca sangrentos. Rugidos graves mas engraçados.

## Lista
| Arquivo | Quando toca (sinal) | O que é | Duração aprox. |
|---|---|---|---|
| `tomate_entrada.wav` | entrada do boss | rugido grave e engraçado + "splash" | 2,0 s |
| `tomate_pulo.wav` | `pulo_inicio` | impulso: pernas comprimindo + "fwump" | 0,5 s |
| `tomate_aterrissagem.wav` | `pulo_aterrissou` | baque pesado molhado + **onda** de terra se espalhando | 1,2 s |
| `tomate_investida.wav` | `investida_inicio` | arrancada + passos rápidos + rosnado | 1,3 s |
| `tomate_bate_obstaculo.wav` | `investida_bateu(true)` | "tonk" de batida + tontura | 0,8 s |
| `tomate_mordida.wav` | `investida_bateu(false)` | mordida (boca Pac-Man fechando) | 0,4 s |
| `tomate_linguada.wav` | `linguada_inicio` | língua esticando, molhada ("slurp" rápido) | 0,6 s |
| `tomate_lingua_presa.wav` | `linguada_prendeu` | "boing" da língua presa no cenário + esforço | 0,8 s |
| `tomate_tonto_loop.wav` | `atordoado` (loop até sair do atordoado) | tontura (assobio/estrelinhas) | 2,0 s, **loop com `smpl`** |
| `tomate_fase2.wav` | `fase2` | rugido mais forte e irritado | 1,5 s |
| `tomate_morte.wav` | `morreu` | "squish" longo + estouro em pedaços (sincronizar com os impactos da `tomato_boss_explosion.glb`) | ~2,5 s |
| `tomate_dano.wav` | ao levar dano (opcional) | squish curto | 0,15 s |

## Níveis (dB RMS, aproximado)
Entrada −17 · fase 2 −16 · aterrissagem −15 · morte −14 · investida −19 · batida −18 · mordida −19 · pulo −21 · linguada −20 · língua presa −20 · tonto −24 · dano −26.

## Devolver
Lista dos arquivos com duração, nível e quais são loop (com `smpl`). O chat não escuta: valide por forma de onda/espectrograma e diga isso.
