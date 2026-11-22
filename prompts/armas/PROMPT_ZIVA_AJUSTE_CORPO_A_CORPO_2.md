# PROMPT ZIVA — Ajuste 2 do corpo a corpo (combo sem cortar a animação + preparo opcional)

## Contexto
Testando: clicar **durante** o golpe corta a animação e já pula para o próximo golpe do combo. Fica incoerente.
E algumas armas (começando pelo **Martelo**) precisam de um **preparo** (levantar a arma) antes do golpe.
- **Não mude o que não está pedido.** Tempos de ativo/recuperação, dano, alcance e o resto continuam.
- Comente o código em português. Valores que eu escolhi: ⚙️.

## 1. O combo só continua quando o golpe anterior termina
- A animação de um golpe = **ativo + recuperação** (a varrida e a volta). Ela **nunca é cortada** por um clique.
- Clique **durante** o golpe = fica **guardado** (um só). Quando o golpe termina, o próximo golpe do combo começa **na hora** (sem pausa extra).
- Sem clique guardado: depois que o golpe termina, há uma **janela de combo** ⚙️ (campo novo `janela_combo_s := 0.3`). Clicou dentro dela → próximo golpe do combo. Passou → o combo volta ao 1º golpe.
- Vale para as três armas.

## 2. Preparo opcional por arma
- Campo novo: `@export var tempo_preparo_s := 0.0` (0 = sem preparo, golpe começa no clique como hoje).
- Com preparo > 0: clique → **preparo** (a arma sobe/vai para trás, **não acerta**) → ativo → recuperação.
- **Martelo da Vovó:** `tempo_preparo_s = 0.4` ⚙️ (levanta o martelo). Cutelo e Facão: `0.0`.
- **Martelo + carga:** o preparo é o "levantar". Se o jogador **continua segurando** depois do preparo, o martelo **fica levantado carregando** (carga de `carga_minima` até cheia em `carga_max_s`). Ao **soltar** (ou num toque rápido, assim que o preparo termina), vem o ativo. Carga cheia continua: dano ×2 + onda de choque + empurra.
- O visual provisório mostra o preparo (o bloco sobe devagar no Martelo) antes da varrida.
- V, F, troca de arma durante o preparo/carga cancelam sem golpear (regras atuais).

## 3. Teste
- Atualize o `dev/validate_corpo_a_corpo`: clique no meio do golpe não corta a animação e o próximo golpe sai quando ela termina; janela de combo de 0,3 s; preparo do Martelo de 0,4 s antes do ativo; carga depois do preparo. Me diga o placar.

## Checklist
- [ ] Golpe nunca é cortado; clique guardado dispara o próximo golpe ao terminar
- [ ] `janela_combo_s` (0,3) depois do golpe
- [ ] `tempo_preparo_s` por arma; Martelo 0,4 s; Cutelo e Facão 0
- [ ] Martelo: preparo → segurar carrega levantado → soltar golpeia
- [ ] Validador atualizado e placar
- [ ] Nada além disso foi alterado
