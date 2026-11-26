# F4 — Progressão: bosses, santuários, oferendas e máquina (proposta v1)

> ⚠️ **Ordem atual: Tomate → Uva → Dragão → Pimenta → Batata → Final (6 bosses).** A Pimenta entrou na cadeia (nov/2026); ver ajuste no [prompt](../../prompts/bosses/PROMPT_ZIVA_PIMENTA_AJUSTE_2.md).
> Status: ✅ aprovado com ajustes (nov/2026) · Prompt: [PROMPT_ZIVA_PROGRESSAO](../../prompts/progressao/PROMPT_ZIVA_PROGRESSAO.md). Base: `loop.md` e `decisoes.md`.
> Objetivo: a "espinha dorsal" do jogo — o que cada boss pede, o que dá e o que libera. Depois vira prompts do Ziva (sistema) e, boss por boss, o conteúdo.

## A espinha dorsal
A coluna **Santuário** diz **em que bioma do mapa** fica o santuário daquele boss (o jogo tem 3: Planície, Floresta, Pedreira).

| # | Boss | Santuário | 1ª oferenda (3 itens) | Reinvocar (3 itens) | Dropa | Libera |
|---|---|---|---|---|---|---|
| 1 | **Tomate Gigante** | Planície | drop do Tomate + drop da Cenoura + drop do Pimentão | 3× drop do Tomate | **Ficha Rara** + **Casca do Tomate** | **Raro** na máquina |
| 2 | **Uva-morcego** | Floresta | **Casca do Tomate** + drop da Cenoura + drop do Pimentão | 3× drop da Cenoura | **Ficha Rara** + **Semente de Uva Sombria** | **Fase 2 do pesadelo** (Cebola, Milho, Abóbora) |
| 3 | **Dragão-Pitaya** | Planície (área aberta para o tabuleiro de raios) | **Semente de Uva Sombria** + drop da Cebola + drop do Milho | 3× drop do Milho | **Ficha Épica** + **Escama de Pitaya** | **Épico** na máquina |
| 4 | **Pimenta Ardente** (PepperBoss2) | Floresta (clareira aberta) | **Escama de Pitaya** + Molho de Pimenta + Lágrima de Cebola | 3× Molho de Pimenta | **Ficha Épica** + **Brasa Eterna** | **fase 3 do pesadelo** (a definir) |
| 5 | **Batata-golem** | Pedreira | **Brasa Eterna** + Minério de Ferro + Lágrima de Cebola | 3× Lágrima de Cebola | **Ficha Épica** + **Raiz de Pedra** | **Lendário** na máquina + o santuário final se ergue |
| 6 | **Final** (deus no céu — a criar) | **existe desde o início, meio enterrado** (local a definir; sugestão: centro do mapa) | **Raiz de Pedra** + **Brasa Eterna** + **Escama de Pitaya** | a decidir | **Ficha Lendária** + material final | fim da "campanha"; mundo continua |
| ★ | **Totem de Melancia** (secreto) | — (10 vacas-melancia) | — | matar 10 vacas de novo | **Ficha Épica** (no futuro: drop especial, ver armas futuras) | nada |

Os nomes dos materiais são provisórios. Os "drops" de inimigos hoje são placeholders (comidas) e serão renomeados depois.

## Ritual do santuário ✅ (ideia do Gustavo)
- O jogador aperta **E** no santuário: o jogo **coloca 1 item por vez**, pegando **direto do inventário** (não precisa estar na mão).
- Cada item colocado começa a **girar em volta do altar**, com um **rastro**.
- Com os **3 itens**, eles **voam para o santuário e explodem** — e o **boss é invocado**.
- **Santuário final:** existe desde o início, **parcialmente enterrado**. Quando o boss 4 morre, ele **sai do chão** e revela algo (o que revela: pensar depois).

## Regras
- **Oferenda = 3 itens** específicos por boss (tabela acima), colocados no ritual. Substitui as "3 sementes" de hoje.
- **Santuário fica no mapa** (já é assim). Depois da 1ª vitória, ele aceita a **oferenda fácil** (3 drops comuns), para farmar material.
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

## Decidido
- Tabela aprovada; fichas = giro garantido; reinvocar barato; Totem dropa algo especial no futuro; santuário final meio enterrado desde o início.
