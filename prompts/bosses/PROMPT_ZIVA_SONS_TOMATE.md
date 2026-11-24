# PROMPT ZIVA — Sons do Tomate Gigante

## Contexto
Os sons do Tomate foram gerados em `res://Blender/<pasta do tomate boss>/sons/`. A luta já emite os sinais. **Só ligar os sons — não mude nada da luta.** Comente em português.
Todos os sons com `volume_db = 0` (os níveis já vêm equilibrados). Importe os loops com "Detect From WAV".

## Ligações
| Arquivo | Sinal / momento | Onde toca | `unit_size` / `max_distance` |
|---|---|---|---|
| `tomate_entrada.wav` | início da entrada do boss | **preso** no boss | 12 / 100 |
| `tomate_pulo.wav` | `pulo_inicio` | preso | 10 / 80 |
| `tomate_aterrissagem.wav` | `pulo_aterrissou` | **no lugar** (player criado no ponto, liberado no `finished`) | 12 / 100 |
| `tomate_investida.wav` | `investida_inicio` | preso | 10 / 80 |
| `tomate_bate_obstaculo.wav` | `investida_bateu(true)` | no lugar | 10 / 80 |
| `tomate_mordida.wav` | `investida_bateu(false)` | preso | 8 / 60 |
| `tomate_linguada.wav` | `linguada_inicio` | preso | 8 / 60 |
| `tomate_lingua_presa.wav` | `linguada_prendeu` | no lugar (ponta da língua) | 8 / 60 |
| `tomate_tonto_loop.wav` | `atordoado` → para no fim do atordoado | preso, **loop** | 8 / 60 |
| `tomate_fase2.wav` | `fase2` | preso | 12 / 100 |
| `tomate_morte.wav` | `morreu` | no lugar (posição da morte) | 12 / 100 |
| `tomate_dano.wav` | ao levar dano | preso; no máx. 1 a cada ⚙️ 0,1 s | 6 / 40 |

- "No lugar" = `AudioStreamPlayer3D` criado **fora** do boss, na posição, e liberado no `finished` (sobrevive à morte/explosão).
- Um som por evento (não um por partícula/onda).

## Checklist
- [ ] 12 sons ligados aos sinais · [ ] loops do tonto param no fim do atordoado · [ ] "no lugar" sobrevive à morte · Nada além disso foi alterado
