# PROMPT ZIVA — Cortar a Batata-golem da cadeia de bosses

## Contexto
A Batata-golem foi **cortada do jogo**. Nova ordem: **1 Tomate → 2 Uva → 3 Dragão-Pitaya → 4 Pimenta Ardente → 5 Deus (final)** + Totem secreto.
Modo rápido, tudo de uma vez. **Não mude o que não está pedido.** Comente em português. Converta saves antigos sem quebrar.

## O que fazer
1. **Remova a Batata** do `ProgressionManager` (tabela, santuário da Pedreira, oferenda, drops). Mova o Golem de Raiz e o que for só dela para `res://_arquivo/bosses/`. Se um save antigo tiver a Batata como derrotada, ignore sem erro.
2. **A Pimenta (boss 4) passa a fazer o que a Batata fazia:** ao ser derrotada pela 1ª vez libera a raridade **Lendário** na máquina **e ergue o santuário final** (a subida do chão que já existe), além de registrar a **fase 3 do pesadelo** (sem inimigos ainda, só registrar). Mensagem/pulso no céu iguais aos outros.
3. **Santuário final (boss 5):** a oferenda passa a ser **Brasa Eterna + Escama de Pitaya + Semente de Uva Sombria** (a Raiz de Pedra sai). Continua não invocando nada por enquanto ("Ainda não…").
4. O **item Raiz de Pedra** e o **Minério de Ferro como oferenda** deixam de ser usados em santuários: **não apague o item Raiz de Pedra** (guarde para o futuro), só tire das oferendas.
5. Pedreira continua com minérios, **sem santuário de boss**.
6. Atualize `dev/validate_progressao` para a cadeia de 5 bosses (+ Totem) e me diga o placar.

## Checklist
- [ ] Batata removida (código e arquivos movidos para `_arquivo`) · [ ] Pimenta libera Lendário + ergue o santuário final + fase 3
- [ ] Oferenda final nova · [ ] Raiz de Pedra preservado · [ ] Save antigo ok · [ ] Validador · Nada além disso foi alterado
