# PROMPT ZIVA — Sons da Uva-morcego

Sons em `res://Blender/<pasta da uva>/sons/`. **Só ligar os sons, não mudar a luta.** `volume_db = 0` em todos; loops com "Detect From WAV". Comente em português.
"No lugar" = `AudioStreamPlayer3D` criado fora do boss e liberado no `finished`.

| Arquivo | Sinal / momento | Onde | `unit_size` / `max_distance` |
|---|---|---|---|
| `uva_entrada.wav` | entrada | preso | 12 / 100 |
| `uva_asas_loop.wav` | enquanto voa (para quando cai ou morre) | preso, loop | 8 / 60 |
| `uva_chuva.wav` | `chuva_inicio` | preso | 10 / 80 |
| `uva_estouro.wav` | `uva_estourou` (1 por uva, no máx. 1 a cada 0,08 s) | no lugar | 8 / 60 |
| `uva_mergulho_aviso.wav` | `mergulho_aviso` | preso | 12 / 100 |
| `uva_mergulho.wav` | `mergulho_inicio` | preso | 10 / 80 |
| `uva_acertou.wav` | `mergulho_acertou` | preso | 8 / 60 |
| `uva_caiu.wav` | `mergulho_errou` | no lugar | 12 / 100 |
| `uva_tonta_loop.wav` | enquanto caída (para no `levantou`) | preso, loop | 8 / 60 |
| `uva_levantou.wav` | `levantou` | preso | 8 / 60 |
| `uva_laser_aviso.wav` | `laser_aviso` | preso | 10 / 80 |
| `uva_laser_loop.wav` | `laser_inicio` → para no `laser_fim` | preso, loop | 12 / 100 |
| `uva_fase2.wav` | `fase2` | preso | 12 / 100 |
| `uva_morte.wav` | `morreu` | no lugar | 12 / 100 |

Checklist: [ ] 14 sons ligados · [ ] loops param na hora certa · Nada além disso foi alterado
