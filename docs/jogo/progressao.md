# F4 — Progressão: bosses, santuários, oferendas e máquina (proposta v1)

> Status: 🟡 proposta do Claude para aprovar. Base: `loop.md` e `decisoes.md`.
> Objetivo: a "espinha dorsal" do jogo — o que cada boss pede, o que dá e o que libera. Depois vira prompts do Ziva (sistema) e, boss por boss, o conteúdo.

## A espinha dorsal
| # | Boss | Santuário (bioma) | 1ª oferenda (difícil) | Reinvocar (fácil) | Dropa | Libera |
|---|---|---|---|---|---|---|
| 1 | **Tomate Gigante** | Planície | drops comuns dos inimigos da fase 1 + recursos | drops comuns | **Ficha Rara** + **Casca do Tomate** | **Raro** na máquina |
| 2 | **Uva-morcego** | Floresta | **Casca do Tomate** + drops | drops comuns | **Ficha Rara** + **Semente de Uva Sombria** | **Fase 2 do pesadelo** (Cebola, Milho, Abóbora) — animação no mundo + mensagem |
| 3 | **Dragão-Pitaya** | Pedreira (ele cava) | **Semente de Uva Sombria** + drops da fase 2 | drops comuns | **Ficha Épica** + **Escama de Pitaya** | **Épico** na máquina |
| 4 | **Batata-golem** | Pedreira funda | **Escama de Pitaya** + minério | drops comuns | **Ficha Épica** + **Raiz de Pedra** | **Lendário** na máquina |
| 5 | **Final** (deus no céu — a criar) | o céu (santuário aparece depois do boss 4) | **Raiz de Pedra** + materiais dos 4 | drops comuns | **Ficha Lendária** + material final | fim da "campanha"; mundo continua |
| ★ | **Totem de Melancia** (secreto) | — (aparece ao matar 10 vacas-melancia) | — | matar 10 vacas de novo | **Ficha Épica** + material secreto | nada (é secreto) |

Os nomes dos materiais são provisórios.

## Regras
- **Oferenda = item fabricado na Bancada** (receita), colocado no santuário do boss com **E**. Substitui as "3 sementes" de hoje.
- **Santuário fica no mapa** (já é assim). Depois da 1ª vitória, ele aceita a **oferenda fácil** (receita barata com drops comuns), para farmar material.
- **Ordem garantida:** a 1ª oferenda de cada boss pede o material do boss anterior. Não dá para pular boss.
- **Ficha de raridade:** item que, usado na máquina caça-níquel, dá **um giro garantido** daquela raridade. (Depois: NPC que troca itens por fichas.)
- **Máquina por nível:** só sorteia raridades **liberadas**; a chance das raridades liberadas segue a tabela da planilha (Comum 60 / Raro 28 / Épico 10 / Lendário 2), redistribuída entre as liberadas.
- **Material único:** serve para a próxima oferenda **ou** para uma **arma de boss** na bigorna (armas de boss: depois).
- **Fase do pesadelo:** fase 1 no início (Tomate, Cenoura, Pimentão); fase 2 depois da Uva (soma Cebola, Milho, Abóbora). A fase muda o que o spawn natural, as hordas noturnas e os monumentos geram.
- **Tudo salvo** (bosses derrotados, raridades liberadas, fase, vacas) — o save já guarda a progressão.

## Ordem de trabalho sugerida
1. **Ziva — sistema de progressão** (dá para testar com os ovos do F3, mesmo sem a luta dos bosses):
   - santuários novos (posição por bioma, oferenda por receita, 1ª × reinvocar);
   - receitas das oferendas e itens de material/ficha;
   - máquina por nível + uso das fichas;
   - fase do pesadelo nos spawns + animação/mensagem;
   - drops dos bosses.
2. **Boss 1 — Tomate Gigante** (modelo e animações já existem): luta + sons + entrada de boss.
3. **Boss 2 — Uva-morcego** (modelo e animações já existem) + **Abóbora** (inimigo novo da fase 2).
4. Dragão (já pronto: só ligar drops/santuário) → Batata-golem (refazer) → Final (criar).

## Perguntas
1. Aprova a tabela (oferendas, drops, o que libera)? Algum boss em outro bioma?
2. **Fichas:** giro garantido da raridade na máquina — ok?
3. **Reinvocar** com receita barata de drops comuns — ok?
4. O **Totem secreto** dropa ficha Épica — ok, ou algo especial (ex.: uma arma única)?
5. **Santuário do boss final** só aparece depois do boss 4 (ou já existe desde o início, mas trancado)?
