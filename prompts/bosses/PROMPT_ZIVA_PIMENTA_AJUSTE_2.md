# PROMPT ZIVA — Pimenta Ardente: Ajuste 2 (escudo discreto + entra na cadeia de bosses)

## Contexto
O Gustavo gostou da Pimenta Ardente. Duas mudanças: (1) o escudo fica **discreto**; (2) ela **entra na cadeia de bosses** (deixa de ser boss extra). Nova ordem: **1 Tomate → 2 Uva → 3 Dragão-Pitaya → 4 Pimenta → 5 Batata-golem → 6 Deus (final)**.
Modo rápido: tudo de uma vez. **Não mude o que não está pedido.** Comente em português. ⚙️ = valor escolhido por mim.

## 1. Escudo discreto
- **Sem escudo visível por padrão.** Remova a barreira grande/permanente (e a que aparecia no anel de fogo).
- Fora do atordoado, o boss continua **negando todo dano** (tiro, golpe, soco, coronhada, explosão, Queimar), mas agora o escudo **só aparece quando alguém tenta feri-lo**:
  - uma casca fina facetada translúcida laranja **colada ao corpo** (⚙️ 1,15× o raio do corpo, nunca maior), com **onda de brilho** saindo do ponto do impacto;
  - **aparece em ⚙️ 0,05 s e some em ⚙️ 0,2 s**; vários acertos seguidos só renovam (sem acumular).
- Mantenha: "plink" no bloqueio, marcador de acerto **cinza**, sem dano/Essência/hitstop no boss.
- Ao ser atordoado (bola rebatida): pequeno estilhaçar rápido do mesmo brilho (⚙️ 0,3 s). **Não há mais "refazer a barreira"**: ao acordar, ele só volta a negar dano (sem efeito até alguém atirar).
- Sinais iguais (`barreira_bloqueou`, `barreira_quebrou`); `barreira_refeita` pode ser removido.

## 2. Pimenta na cadeia de progressão
Atualize a tabela do `ProgressionManager` (e converta saves antigos sem quebrar):
| id | Santuário | 1ª oferenda (3 itens) | Reinvocar | Dropa | Libera |
|---|---|---|---|---|---|
| `pimenta` (**novo, boss 4**) | **Floresta** (clareira aberta ⚙️ raio 25 m para a órbita) | Escama de Pitaya + Molho de Pimenta (drop do Pimentão) + Lágrima de Cebola | 3× Molho de Pimenta | **Ficha Épica + Brasa Eterna** (item novo, material de boss: laranja-fogo `#FF6A1F`, fosco) + dinheiro | **fase 3 do pesadelo** (só registrar; inimigos da fase 3 ainda não existem) |
| `batata` (agora **boss 5**) | Pedreira | **Brasa Eterna** + Minério de Ferro + Lágrima de Cebola | 3× Lágrima de Cebola | Ficha Épica + Raiz de Pedra | **Lendário** + ergue o santuário final (igual hoje) |
| `final` (boss 6) | centro, meio enterrado | Raiz de Pedra + Brasa Eterna + Escama de Pitaya | (depois) | Ficha Lendária + Material Final | fim da campanha |
- O santuário final continua subindo quando a **Batata** (o boss logo antes dele) morre.
- A Pimenta passa a **sair do ritual do santuário** (E → 3 itens → explodem → invoca) como os outros. Mantenha o **ovo do F3**. Troque os drops provisórios dela (Molho de Pimenta + dinheiro) por **Ficha Épica + Brasa Eterna + dinheiro**, na primeira derrota registra o boss e mostra a mensagem de liberação ("O pesadelo se aprofunda…") + pulso no céu (como nos outros).
- Ajuste mensagens/validador: `dev/validate_progressao` com a nova cadeia (6 bosses) e `dev/validate_pimenta` com o escudo discreto. Placar.

## Checklist
- [ ] Escudo invisível por padrão; casca fina colada que pisca ao ser atacada (0,05 s / 0,2 s)
- [ ] Pimenta no `ProgressionManager` (boss 4), santuário na Floresta, oferenda e drops novos; Batata e final atualizados
- [ ] Item Brasa Eterna · [ ] Save antigo convertido · [ ] Validadores com placar · Nada além disso foi alterado
