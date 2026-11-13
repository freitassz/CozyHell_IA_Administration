# PROMPT ZIVA — Fundação: salvar/carregar, menu principal e criação de mundo

## Contexto
O CozyHell3D tem **mundo persistente** (estilo Terraria), mas hoje **nada é salvo**: o jogo abre direto no `main.tscn`, a seed é fixa (`556677869`) e não existe menu principal.
Vamos criar a base de salvamento, o menu e a criação de mundo.

- **Não mude o que não está pedido.** Não altere regras de combate, máquina, bigorna, santuários, inimigos.
- **Faça uma etapa por vez e teste.** A **Etapa 0 é só relatório**: pare e espere o ok.
- Comente o código em português.
- Valores que eu escolhi ficam em `@export` (ou constantes bem nomeadas) e estão marcados com ⚙️.

## Decisões de design (já tomadas)
| Tema | Decisão |
|---|---|
| Personagem | fica **dentro do mundo** (cada mundo tem seus jogadores) |
| Mundos salvos | **sem limite** |
| Modos | **Soneca** (leve) e **Pesadelo** (hardcore), escolhido ao criar o mundo |
| Morte no Soneca | renasce na cama (ou no spawn) perdendo parte do dinheiro e dos recursos |
| Morte no Pesadelo | **o mundo é apagado** e o jogo volta ao menu |
| Recursos coletados | **renascem** depois de alguns dias |
| Mapa | salvar só **seed + diferenças** (não o terreno inteiro) |
| Quando salva | ao usar a **cama**, a cada **amanhecer**, ao **sair** pelo menu e ao **fechar a janela**. Sem botão de salvar manual |

## Regras de multiplayer (o jogo terá multiplayer no futuro)
- O save pertence a quem hospeda (por enquanto, o jogador local).
- Dados de jogador ficam num dicionário por **ID de jogador** (hoje só existe `"local"`). Nunca "o player" como valor único no save.
- Não guarde estado de save em lugares que assumem um jogador só.

---

## ETAPA 0 — Relatório (não altere nada)
Me diga, com arquivo e linha:
1. Como o **inventário** guarda itens (ids, quantidade, hotbar) e onde ficam armadura/acessórios equipados, R$, sucata e o `nivel_arma`.
2. Como o `building_manager` guarda as construções e como o **Baú** guarda o conteúdo.
3. Como o `IslandGenerator` cria árvores, pedras, minérios, monumentos, santuários e vacas-melancia: **eles têm um ID estável** (mesmo ID para a mesma seed)? Se não, como dá para criar um?
4. Onde ficam: dia/hora (`DayNightCycle`), clima, `ProgressionManager`, santuários usados, bosses derrotados, monumentos limpos, contador de vacas-melancia (se existir).
5. O que acontece hoje quando o jogador **morre** e o que a **Cama** faz (dormir? ponto de renascer?).
6. Autoloads existentes.

**Pare aqui e entregue o relatório.**

## ETAPA 1 — SaveManager e dados do mundo
- Crie o autoload `SaveManager`.
- Pasta: `user://saves/<id_mundo>/` com:
  - `mundo.json`: metadados (lista de mundos lê só este arquivo).
  - `estado.json`: o resto.
- Formato do `mundo.json`:
  ```json
  {
    "versao_save": 1,
    "id": "mundo_20261113_153012",
    "nome": "Minha Fazenda",
    "seed": 556677869,
    "modo": "soneca",
    "dia": 4,
    "bosses_derrotados": 1,
    "criado_em": "2026-11-13T15:30:12",
    "salvo_em": "2026-11-13T16:02:40"
  }
  ```
- Padrão para os sistemas: cada sistema salvável entra no grupo `salvavel` e implementa
  ```gdscript
  func salvar() -> Dictionary
  func carregar(dados: Dictionary) -> void
  # e uma chave fixa:
  const CHAVE_SAVE := "dia_noite"  # exemplo
  ```
  O `SaveManager` junta tudo em `estado.json` por `CHAVE_SAVE`. Sistema novo = só implementar isso.
- Converta `Vector3`/`Basis` para arrays no JSON (crie funções utilitárias no `SaveManager`).
- Nesta etapa salve: **seed, modo, nome, dia, hora e clima**.
- `IslandGenerator` passa a receber a seed do `SaveManager` (não mais fixa no `main.tscn`).

**Teste:** criar um mundo por código, avançar a hora, salvar, recarregar → mesma seed, mesmo terreno, mesmo dia/hora.

## ETAPA 2 — Menu principal e criação de mundo
- Crie `ui/menu_principal.tscn` e defina como `run/main_scene`.
- Botões: **Novo Mundo**, **Carregar**, **Opções**, **Sair**.
- **Novo Mundo:** nome, seed (campo vazio = aleatória), modo **Soneca** / **Pesadelo** (com uma frase explicando cada um). Botão Criar → gera o mundo e entra.
- **Carregar:** lista lendo só os `mundo.json` (nome, modo, dia, bosses derrotados, data). Botões Jogar e **Apagar** (com confirmação).
- **Opções:** reaproveite o painel de volume/gráficos do menu de pausa.
- No menu de pausa: troque "Sair do jogo" por **"Salvar e voltar ao menu"** e mostre a seed do mundo (para compartilhar).
- Deixe espaço visual para um botão **Multiplayer** futuro (desativado ou oculto).

**Teste:** criar 2 mundos com seeds diferentes, voltar ao menu, ver os 2 na lista, carregar cada um, apagar um.

## ETAPA 3 — Jogador
Salve por ID de jogador (`"local"`): posição, rotação, vida, inventário completo (com hotbar), armaduras e acessórios equipados (com quantidade empilhada), R$, sucata, `nivel_arma`, ponto de renascer.
- Formato de item deve aceitar dados extras por cópia no futuro (ex.: `{"id": "revolver", "qtd": 1, "dados": {}}`).

**Teste:** juntar itens, equipar armadura, fundir o revólver, ganhar R$ → sair e carregar → tudo igual.

## ETAPA 4 — Construções e baús
- Salve cada construção: tipo, posição, rotação e dados próprios (conteúdo do Baú, etc.). Barraca de Venda, Bancada, Bigorna, Fornalha e Cama incluídas.

**Teste:** construir paredes, um baú com itens e uma bigorna → sair e carregar → tudo no lugar, baú com os itens.

## ETAPA 5 — Mapa por diferenças + renascimento
- Cada recurso do mapa (árvore, pedra, minério) precisa de **ID estável** pela seed (use o que a Etapa 0 indicar).
- Ao coletar, registre `coletados[id] = dia_atual`. Ao carregar, não crie (ou remova) os coletados.
- Renascimento: ⚙️ `@export var dias_para_renascer := 3`. Ao amanhecer, recursos com `dia_atual - dia_coletado >= dias_para_renascer` voltam (fora da visão do jogador, se possível).
- Também salvar: monumentos limpos, santuários e o estado deles, vacas-melancia mortas.

**Teste:** cortar 5 árvores → sair e carregar → continuam cortadas; passar 3 dias → voltam.

## ETAPA 6 — Progressão
Salve o `ProgressionManager` e tudo de progressão que a Etapa 0 encontrar (bosses derrotados, fase de inimigos, raridades liberadas, contador de vacas). Atualize `bosses_derrotados` no `mundo.json`.

**Teste:** matar um boss pelo ovo do F3 → sair e carregar → continua derrotado.

## ETAPA 7 — Salvamento automático
- Salve ao: usar a **Cama**, **amanhecer**, "Salvar e voltar ao menu", e fechar a janela (`NOTIFICATION_WM_CLOSE_REQUEST`).
- Mostre um aviso pequeno "Salvando..." no canto.
- Salve num arquivo temporário e só depois troque pelo definitivo (não corromper o save se o jogo fechar no meio).

**Teste:** jogar até amanhecer, matar o processo do jogo → ao carregar, está no estado do amanhecer.

## ETAPA 8 — Morte
- **Soneca:** renasce no ponto de renascer (cama, ou spawn se não houver), perdendo:
  - ⚙️ `@export var perda_dinheiro := 0.3` (30% do R$ e da sucata);
  - ⚙️ `@export var perda_recursos := 0.5` (50% dos itens do tipo recurso/drop).
  - Armas, armaduras, acessórios e ferramentas **não** são perdidos.
- **Pesadelo:** tela curta "Você acordou..." → **apaga a pasta do mundo** → volta ao menu principal.
- Se já existir lógica de morte, adapte-a para os dois modos sem mudar o resto.

**Teste:** morrer no Soneca → renasce com 70% do R$; morrer no Pesadelo → mundo some da lista.

---

## Checklist final
- [ ] Etapa 0: relatório entregue e aprovado
- [ ] `SaveManager` com `mundo.json` + `estado.json` e o padrão `salvar()/carregar()` no grupo `salvavel`
- [ ] Seed vem do mundo criado (não é mais fixa)
- [ ] Menu principal, Novo Mundo (nome, seed, modo), Carregar (com apagar), Opções
- [ ] Pausa: "Salvar e voltar ao menu" + seed visível
- [ ] Jogador salvo por ID (`"local"`), com inventário, equipados, R$, sucata, `nivel_arma`
- [ ] Construções e baús salvos
- [ ] Recursos coletados salvos e renascendo após `dias_para_renascer`
- [ ] Progressão salva
- [ ] Salvamento automático (cama, amanhecer, sair, fechar janela) com arquivo temporário
- [ ] Morte: Soneca (perdas) e Pesadelo (apaga mundo)
- [ ] Nada além disso foi alterado
