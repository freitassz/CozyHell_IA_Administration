# PROMPT ZIVA — Limpeza do projeto (remover o que foi cortado)

## Contexto
O CozyHell3D passou por uma revisão de design. Algumas coisas foram **cortadas** e precisam sair do jogo **sem quebrar o resto**.
Este prompt **só remove**. Não crie sistemas novos.

- **Não mude o que não está pedido.**
- **Faça uma etapa por vez e teste** antes de seguir para a próxima.
- **Não apague o `revolver`** nem nada ligado a ele.
- Comente o código em português.

## O que NÃO mexer (fica no jogo)
Revólver do Coveiro · Vara de Pesca · comidas/drops de inimigos · Fogueira · acessórios e a máquina de acessórios · sementes de chefe · ovos de invocação · armaduras · picaretas e machados · Bancada, Bigorna, Fornalha, Baú, Cama · construções · sementes **Normais** (e as "base") · Monumento · pilar de boss · ciclo dia/noite · hordas noturnas · visual da chuva.

## O que sai
| # | Item | Onde procurar |
|---|---|---|
| 1 | **Loja** (`unlock_pistol`) | procure `unlock_pistol` e qualquer "shop"/"loja" |
| 2 | **Armas placeholder:** `pistol`, `sword`, `iron_sword`, `scythe`, `shotgun`, `warhammer`, `rifle`, `potato_cannon` | `resources/items/weapons/`, pools das máquinas de sorteio, receitas, drops, inventário inicial, visuais em `HandModels` |
| 3 | **Mesa de Contrato / Armeiro** (`WeaponTrader`) | item de construção, receita, cena, UI do painel de contratos |
| 4 | **Enxada, Enxada de Ferro, Pá, Pá de Ferro** | `resources/items`, receitas, visuais em `HandModels` (Hoe, Shovel), lógica de arar/cavar |
| 5 | **Sementes e inimigos Mutante e Ancestral** (Abóbora, Batata, Cenoura, Milho, Pimenta, Tomate) | `resources/items`, tabelas de spawn (natural, noturno), `resources/encounters` (monumento), drops |
| 6 | **Chuva acelerando o crescimento das plantações** | `WeatherSystem` (só o multiplicador de crescimento) |

---

## ETAPA 0 — Segurança e relatório (não apague nada)
1. Confirme que o projeto está com tudo commitado no git (peça ao Gustavo para fazer um commit "antes da limpeza", se não estiver).
2. Para **cada item da tabela**, procure **todas** as referências no projeto (`.gd`, `.tscn`, `.tres`, `.json`, `project.godot`, autoloads).
3. Responda também:
   - O plantio de sementes (que gera os inimigos) **depende da enxada ou da pá**?
   - Qual é a diferença entre "Semente de X" (base) e "X Normal"? Qual delas o spawn usa?
   - A máquina de sorteio de armas aguenta ficar **só com o revólver** no pool (sem erro de pool vazio por raridade)?
4. **Entregue o relatório ao Gustavo e pare.** Só siga para a Etapa 1 com o ok dele.

**Teste:** nada mudou no jogo; só existe o relatório.

## ETAPA 1 — Remover a loja
- Remova a loja e o desbloqueio `unlock_pistol` (scripts, UI, chamadas, flags salvas em memória).
- Se algo chamava a loja (botão, NPC, tecla), remova a chamada.

**Teste:** o jogo abre, nenhum erro no console, nenhum botão/tecla leva à loja.

## ETAPA 2 — Remover as armas placeholder
- Apague os 8 resources de arma listados (mantenha `revolver`).
- Tire essas armas de: pools das máquinas de sorteio, receitas (bancada/bigorna), drops, inventário inicial, catálogo do criativo.
- Remova os visuais delas dentro de `HandModels` (ex.: `Pistol`), sem mexer em `HandsVisual` nem no encaixe do revólver.
- Se a máquina de armas quebrar com pool pequeno, faça ela **ignorar raridades sem arma** (não sortear raridade vazia). Não mude mais nada na máquina.

**Teste:** girar a máquina de armas várias vezes → só sai o revólver (ou sucata se repetido), sem erro. F3 não lista as armas removidas. Revólver saca, atira e recarrega normalmente.

## ETAPA 3 — Tirar a Mesa de Contrato (guardar o código)
- Tire a Mesa de Contrato do jogo: receita, item de construção, catálogo, qualquer instância no mundo.
- **Não apague o código:** mova script, cena e UI do `WeaponTrader` para `res://_arquivo/weapon_trader/`. Ela vai virar um NPC no futuro.
- Garanta que o `ItemDatabase` **não** varre `res://_arquivo/` (se o item da mesa for um `.tres` em `resources/items`, mova-o também).

**Teste:** F3 não lista a Mesa; não dá para construir; o jogo abre sem erro.

## ETAPA 4 — Remover enxada e pá
- Apague os 4 itens (Enxada, Enxada de Ferro, Pá, Pá de Ferro), as receitas e os visuais (`Hoe`, `Shovel`) em `HandModels`.
- Remova a lógica de arar/cavar que só servia a elas.
- **Se o plantio de sementes dependia da enxada** (Etapa 0): faça a semente ser plantada **direto no chão** ao usar o item (mesma ação/tecla de hoje para plantar), sem precisar de ferramenta. Não mude o tempo nem o que nasce.

**Teste:** F3 não lista enxada/pá; plantar uma semente Normal ainda faz o inimigo nascer.

## ETAPA 5 — Remover Mutante e Ancestral
- Apague as sementes **Mutante** e **Ancestral** de todas as plantas e as variantes de inimigo correspondentes (cenas, resources, multiplicadores de status).
- Tire-as das tabelas de spawn natural, noturno, dos encontros de monumento (`resources/encounters`) e dos drops. Onde uma tabela ficar vazia, use a versão **Normal** da mesma planta.
- **Não mexa** em "Semente de X" base × "X Normal" ainda: só reporte (Etapa 0). O Gustavo decide depois.

**Teste:** passar uma noite inteira e ativar 2 monumentos → só aparecem inimigos Normais, sem erro. F3 não lista Mutante/Ancestral.

## ETAPA 6 — Chuva sem crescimento
- No `WeatherSystem`, remova **só** o efeito de dobrar a velocidade de crescimento das plantações. A chuva continua aparecendo igual.
- (O efeito novo da chuva — inimigos mais fortes/rápidos — virá em outro prompt. Não faça agora.)

**Teste:** com chuva, uma semente plantada leva o mesmo tempo que sem chuva.

---

## Checklist final
- [ ] Etapa 0: relatório entregue e aprovado
- [ ] Loja e `unlock_pistol` removidos
- [ ] 8 armas placeholder removidas; máquina sorteia só o revólver sem erro
- [ ] Mesa de Contrato fora do jogo; código em `res://_arquivo/weapon_trader/`
- [ ] Enxada e pá removidas; plantio funciona sem ferramenta
- [ ] Mutante e Ancestral removidos de itens, spawns, encontros e drops
- [ ] Chuva não acelera mais o crescimento
- [ ] Revólver funciona igual a antes
- [ ] Jogo abre e roda uma noite inteira sem erro no console
- [ ] Nada além disso foi alterado
