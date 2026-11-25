# Pedido para o chat de modelagem — Pimenta Ardente (PepperBoss2): mãos complexas + animações + sons

> Skill `lowpoly-game-3d-blender`. Pasta: a do `PepperBoss2`. **Aparência: mantenha o modelo atual** (corpo vermelho, chifres, cabo verde, olhos e boca de fogo); o Gustavo descreve o que mudar nas mãos. Faça **tudo de uma vez** (modelo → rig → animações → sons) e devolva um bloco só. Mande **uma imagem de teste das mãos** antes de animar.

## 1. Mãos mais complexas
- Hoje são blocos com dedos chatos. Quero **mãos articuladas**: palma + **polegar (2 segmentos) + 4 dedos (3 segmentos)**, com os dedos curvando de verdade (rig com ossos de dedo), estilo facetado.
- Cor mais clara que o corpo (vermelho-fogo / laranja), nada perto do preto. **Pontas dos dedos** num material separado emissivo `PontasDedos` (o Godot pode acender).
- Aparecem **duas vezes**: (a) presas ao corpo (ossos `MaoE`/`MaoD`, flutuando como hoje) e (b) em **`pimenta_mao.glb`** separado, com rig próprio, para o jogo mandá-las voando no ataque.

## 2. Corpo (`pimenta_boss.glb`) — ações (30 fps, emendas = 0, sem quadro parado no início)
Mantenha/renomeie as 4 existentes e crie as novas (se preferir manter os nomes antigos, informe o mapa).
| Ação | O que mostra | Duração |
|---|---|---|
| `Idle` (= IDLE) | flutua, mãos balançando, dedos mexendo de leve — **loop** | 2,0 s |
| `Brasas` | sobe as mãos, dedos tremendo; **solta** as brasas em ~1,2 s | 1,8 s |
| `Anel_Fogo` (= DEFENSE_FIRE) | se encolhe cercado de fogo e **libera o anel** em ~1,2 s | 1,8 s |
| `Maos_Enviar` | as mãos **soltam** e somem (escala 0,001 no fim, para não duplicar com `pimenta_mao.glb`) | 1,2 s |
| `Maos_Voltar` | as mãos reaparecem no lugar | 0,6 s |
| `Lancar_Bola` (= ATTACK_FIREBALL) | boca abre e **acende** (carrega 1,2 s), **solta** a bola em ~1,4 s, recupera | 2,0 s |
| `Hurt` (= HURT) | tranco curto | 0,3 s |
| `Atordoado_Start` | desmonta no ar, olhos viram espiral/fecham, fogo diminui | 0,6 s |
| `Atordoado_Loop` | tonto, balançando — **loop** | 1,5 s |
| `Atordoado_End` | se recompõe, olhos acendem | 0,6 s |
| `Fase2` | olhos e boca flamejam mais, treme | 1,5 s |
| `Morte_Start` | se desfaz, mãos caem | 2,0 s |

**Mãos soltas** (`pimenta_mao.glb`): `Mao_Aberta` (loop, 1,0 s), `Mao_Esmagar` (dedos abrem em garra e a mão desce com força, 0,5 s; impacto em 0,35 s), `Mao_Sumir` (0,3 s).

## 3. Âncoras e materiais
- Ossos `FX_Boca` (de onde sai a bola), `FX_OlhoE`, `FX_OlhoD`, `FX_MaoE`, `FX_MaoD`, `FX_Topo`.
- Materiais separados: **`OlhosFogo`**, **`BocaFogo`** (o Godot escurece quando atordoado), `PontasDedos`.
- Bola de fogo: reaproveite o `Fireball` que já existe no projeto; só refaça se destoar (`bola_fogo_pimenta.glb`, base ~1 m).
- Estilo: cores fortes e claras, fosco, sem textura; fogo/faíscas/fumaça = efeitos no Godot.

## 4. Sons (sintetizados; WAV 44,1 kHz 16-bit estéreo; RMS; loops com `smpl`) — pasta `sons\`
Tom: fogo e crepitar cartunesco, nada sangrento.
| Arquivo | Quando | Duração | dB RMS |
|---|---|---|---|
| `pimenta_entrada.wav` | entrada | 2,0 s | −17 |
| `pimenta_fogo_loop.wav` | enquanto voa (fogo suave) | 1,5 s **loop** | −27 |
| `pimenta_brasas.wav` | `brasas_inicio` | 1,0 s | −20 |
| `pimenta_brasa_impacto.wav` | cada brasa que cai | 0,3 s | −23 |
| `pimenta_anel_aviso.wav` | `anel_aviso` (carregando) | 1,2 s | −19 |
| `pimenta_anel.wav` | `anel_inicio` (onda de fogo) | 1,0 s | −16 |
| `pimenta_maos_aviso.wav` | `maos_aviso` | 1,2 s | −20 |
| `pimenta_maos_esmagar.wav` | `maos_esmagaram` | 0,7 s | −15 |
| `pimenta_bola_aviso.wav` | `bola_aviso` (boca acendendo) | 1,2 s | −19 |
| `pimenta_bola_loop.wav` | bola voando | 1,0 s **loop** | −22 |
| `pimenta_bola_rebatida.wav` | `bola_rebatida` ("TONK" de rebater) | 0,5 s | −15 |
| `pimenta_bola_explode.wav` | `bola_errou` | 0,8 s | −16 |
| `pimenta_atordoado_loop.wav` | `atordoado` | 2,0 s **loop** | −24 |
| `pimenta_acordou.wav` | `acordou` | 0,6 s | −21 |
| `pimenta_fase2.wav` | `fase2` | 1,4 s | −16 |
| `pimenta_morte.wav` | `morreu` | 2,5 s | −14 |
| `pimenta_dano.wav` | ao levar dano | 0,15 s | −26 |
O chat não escuta: valide por forma de onda/espectrograma.

## Devolver (um bloco só)
Arquivos e nós raiz · mapa de nomes das ações com **duração e nº de quadros** · **momentos dos eventos** (brasas, anel, bola sai, impacto da mão) · ossos e materiais · lista de sons com duração/nível/loops.
