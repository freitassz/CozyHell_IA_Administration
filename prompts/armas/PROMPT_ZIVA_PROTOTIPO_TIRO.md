# PROMPT ZIVA — F2: Protótipo do tiro (Essência do Sonho)

## Contexto
O jogo já tem salvamento, menu e criação de mundo. A única arma real é o **Revólver do Coveiro** (modelo, animações e controlador `ArmaFps`).
Agora vamos montar o **núcleo do tiro** para testar se é divertido, **sem arte nova**:
- ficha de dados de arma (`WeaponData`);
- armas como **cópias** (nível por cópia, fusão por soma);
- barra de **Essência do Sonho** (recarga e especial gastam dela);
- **soco rápido** com a arma na mão (enche a essência);
- **mirar** com o botão direito;
- **especial próprio por arma** na tecla **Q** (algumas armas não têm);
- 3 armas de teste usando o modelo do revólver;
- feedback de acerto.

Regras:
- **Não mude o que não está pedido.** Não mexa em máquina, santuários, inimigos, geração, save (além do que a Etapa 2 pede).
- **Faça uma etapa por vez e teste.** A **Etapa 0 é só relatório**: pare e espere o ok.
- Comente o código em português.
- **Nada de número fixo no código de tiro:** tudo vem do `WeaponData` ou de `@export`. Valores que eu escolhi estão marcados com ⚙️.
- Regras de multiplayer (futuro): a essência, o pente e o cooldown são **de cada jogador**; nada de singleton que assume um jogador só.

---

## ETAPA 0 — Relatório (não altere nada)
Me diga, com arquivo e linha:
1. Como o revólver **atira** hoje (`_on_tiro_revolver`, hitscan ou projétil, dano, alcance) e como **recarrega** (munição, pente, existe munição de reserva?).
2. O `ArmaFps`: como lê cadência/recarga/saque e o que precisa para receber os valores de um `WeaponData`.
3. **Teclas** (Input Map): o botão direito já faz algo? Q, V já estão em uso?
4. Existe **mirar** (zoom/ADS) hoje?
5. O **soco** da mão nua: dano, como acerta (sinal `soco_impacto`), e se dá para tocar `02_1_2_Soco_Esquerdo` (mão esquerda) **enquanto o revólver está na mão direita** — o `BracosFps` fica pausado com arma na mão.
6. Como o inventário guarda armas hoje (empilham?) e como a bigorna faz Fundir/Desmanchar com o `nivel_arma`.
7. Vida dos inimigos comuns (Tomate, Cenoura, Pimentão, Cebola, Milho, Abóbora) e dos bosses.
8. Como o HUD mostra vida e munição; se há mira (crosshair) e som de acerto.

**Pare e entregue o relatório.**

## ETAPA 1 — `WeaponData`
Crie `resources/weapons/weapon_data.gd` (`class_name WeaponData extends Resource`) com:
```gdscript
@export var nome: String
@export var raridade: int                     # use o enum de raridade existente
@export_enum("Instantaneo", "Projetil") var tipo_tiro := 0
@export var dano := 10.0                      # por projétil
@export var projeteis_por_tiro := 1
@export var dispersao_graus := 0.0
@export var cadencia_tps := 2.0               # tiros por segundo
@export var pente := 6
@export var recarga_s := 1.5
@export var custo_essencia_recarga := 10.0
@export var essencia_por_acerto := 2.0        # quanto CADA projétil que acerta devolve de essência
@export var alcance_m := 50.0
@export var queda_dano_50_m := 30.0           # distância em que o dano cai pela metade
@export var tempo_saque_s := 0.4
@export var knockback_m := 0.5
@export var fov_mira := 60.0                  # FOV ao mirar
@export var mult_dispersao_mira := 0.4        # dispersão multiplicada ao mirar
@export var especial: EspecialArma            # null = arma SEM especial
@export var cena_visual: PackedScene          # no protótipo todas usam o revólver
```
- Ligue o `ItemData` do revólver a um `WeaponData` (`revolver_data.tres`) com os **valores atuais** dele (os do relatório) e `pente = 6`, `custo_essencia_recarga = 10` ⚙️, `essencia_por_acerto = 2` ⚙️.
- O código de tiro e o `ArmaFps` passam a ler **só** o `WeaponData`.

**Teste:** o revólver atira, recarrega e dá o mesmo dano de antes.

## ETAPA 2 — Armas como cópias + fusão por soma
- Armas **não empilham** mais. Cada slot de arma guarda `{"item": ItemData, "amount": 1, "dados": {"nivel": 1, "balas": N}}`.
- Toda arma nasce **nível 1** com o pente cheio.
- Multiplicador de dano por nível ⚙️:
  ```gdscript
  @export var bonus_por_nivel: Array[float] = [0.0, 0.08, 0.14, 0.19, 0.23]  # nv1..nv5
  ```
- **Bigorna → Fundir:** o jogador escolhe a arma principal e uma cópia do **mesmo tipo** para consumir. Resultado: `nivel = min(5, nivel_a + nivel_b)`. Se a soma passar de 5, mostre o aviso "O excesso será perdido" antes de confirmar.
- **Desmanchar:** por cópia (escolhe qual). Mantém a confirmação.
- Nome mostra o nível ("Revólver do Coveiro nv3").
- Remova o `nivel_arma` por tipo.
- **Save:** passe para `versao_save: 2`. Ao carregar um save v1, converta: cada cópia recebe `nivel = clamp(nivel_arma_antigo + 1, 1, 5)` e pente cheio. Salve `nivel` e `balas` de cada cópia.

**Teste:** 2 revólveres com níveis diferentes em slots separados; nv3 + nv2 = nv5; nv4 + nv3 = nv5 com aviso; salvar/carregar mantém níveis e balas; um save antigo carrega sem erro.

## ETAPA 3 — Essência do Sonho
Componente no jogador (`essencia_component.gd`):
```gdscript
@export var maximo := 100.0
@export var regen_por_segundo := 0.75     # ⚙️ lenta de propósito (0 → 100 em ~2 min)
@export var ganho_por_soco := 12.0        # ⚙️ por soco que acerta (valor fixo, alto)
@export var perda_ao_levar_dano := 0.0    # ⚙️ desligado
signal essencia_mudou(atual: float, maximo: float)
```
- Começa **cheia**. Ganho de tiro = `essencia_por_acerto` **da arma** por projétil que acerta (cada arma tem o seu).
- Soco (mão nua ou soco rápido) que acerta: `+ganho_por_soco`.
- HUD: barra **lilás** (`#B98CFF`) abaixo da vida, com uma marquinha no valor do `custo_essencia_recarga` da arma na mão.
- Salve a essência no save do jogador.

**Teste:** atirar e acertar enche um pouco; socar enche bem mais; parado regenera devagar.

## ETAPA 4 — Recarga gastando essência
- Munição infinita. **Recarregar gasta `custo_essencia_recarga`** no início da recarga.
- Sem essência suficiente: **não recarrega** → clique seco (som existente), barra pisca vermelho 0,4 s, aviso "Sem essência" perto da mira. Sinal `recarga_negada`.
- Trocar de arma **não** enche o pente (cada cópia guarda suas `balas`).
- Pente vazio + tentar atirar → tenta recarregar automaticamente (com a mesma regra).

**Teste:** com 5 de essência não recarrega; com 10+ recarrega e a barra cai; trocar de arma e voltar mantém as balas.

## ETAPA 5 — Soco rápido com arma na mão (tecla V)
Para "socar para recarregar" valer a pena, o jogador não pode precisar guardar a arma.
- Ação `soco_rapido` na tecla **V** ⚙️.
- Com arma na mão: soco da **mão esquerda** (`02_1_2_Soco_Esquerdo`) sem guardar a arma. Dano = dano do soco atual. Cooldown ⚙️ 0,6 s.
- O golpe sai no **impacto** da animação (mesma regra do `soco_impacto`).
- Se o relatório mostrar que não dá para tocar a mão esquerda com a arma na direita, faça: guardar rápido → soco → sacar rápido (velocidade 2x) e me avise.

**Teste:** com o revólver na mão, apertar V soca com a esquerda, acerta o inimigo e enche +12 de essência.

## ETAPA 6 — Mirar (botão direito)
- Segurar o **botão direito** mira (se já existir mira, adapte; se não, crie):
  - FOV vai para `fov_mira` da arma em 0,12 s ⚙️;
  - dispersão × `mult_dispersao_mira`;
  - velocidade de andar × 0,6 ⚙️;
  - ao soltar, volta em 0,12 s.
- Pose de mira da arma (centralizar) **não** é necessária agora (vem com a arte).

**Teste:** mirar com a escopeta fecha o leque; com a sniper o zoom é forte.

## ETAPA 7 — Especiais (tecla Q)
- Crie `EspecialArma` (`extends Resource`) com:
  ```gdscript
  @export var nome := ""
  @export var custo_essencia := 30.0
  @export var cooldown_s := 1.5
  func executar(atirador, arma: WeaponData) -> void: pass   # cada especial sobrescreve
  ```
- Q com arma **sem especial** (`especial == null`): não faz nada (só um clique leve).
- Especial **não gasta bala** do pente. Sem essência: mesma resposta da recarga negada. Sinal `especial_usado(nome)`.
- Crie **3 especiais diferentes** (são para teste; o design final vem depois):

| Especial | Arma | Custo ⚙️ | Cooldown ⚙️ | Efeito |
|---|---|---|---|---|
| **Tiro do Coveiro** | Revólver | 35 | 1,5 s | 1 tiro com dano ×3, atravessa até 3 inimigos, empurra 4 m. Clarão maior, lilás |
| **Coice** | Escopeta de teste | 40 | 3 s | 12 projéteis, empurra inimigos 6 m e **joga o jogador 4 m para trás** (dá para usar como mobilidade) |
| **Tiro Carregado** | Sniper de teste | 30 (cobrado ao soltar) | 2 s | **segurar Q** carrega até 1,5 s; dano de ×1 a ×4; atravessa todos; andar × 0,5 enquanto carrega; trocar de arma cancela sem gastar |

**Teste:** cada especial funciona e gasta o certo; a Pistola de teste não tem especial.

## ETAPA 8 — Armas de teste (só pelo F3)
Três `ItemData` + `WeaponData`, todas com o visual do revólver e as animações em velocidade calculada pelos dados:

| Arma | Dano | Proj. | Disp. | Cadência | Pente | Recarga | Custo recarga | Essência/acerto | Alcance | Queda 50% | FOV mira | Especial |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Teste — Pistola rápida | 20 | 1 | 2° | 4/s | 10 | 1,2 s | 10 | 1 | 50 m | 30 m | 62 | — |
| Teste — Escopeta | 8 | 6 | 8° | 1,2/s | 2 | 1,8 s | 20 | 0,8 | 20 m | 10 m | 68 | Coice |
| Teste — Sniper | 90 | 1 | 0° | 0,7/s | 4 | 2,2 s | 15 | 5 | 120 m | 90 m | 30 | Tiro Carregado |

⚙️ Ajuste os danos se a vida dos inimigos (Etapa 0) pedir; me avise o que mudou.
Não coloque essas armas na máquina caça-níquel.

**Teste:** cada uma tem sensação diferente (rápida / perto e forte / longe e lenta).

## ETAPA 9 — Feedback de acerto
- **Marcador de acerto** na mira: um "X" pequeno, branco no acerto, **vermelho no abate**, some em 0,15 s.
- Inimigo **pisca branco** 0,08 s ao levar dano (todos os inimigos e bosses).
- Som de acerto (reaproveite um existente); som diferente no abate se houver.
- **Sem números de dano flutuando.**
- Sinal `acertou(alvo, dano, matou: bool)` no atirador (para sons e efeitos futuros).

**Teste:** acertar mostra o X branco e o inimigo pisca; matar mostra o X vermelho.

---

## Sinais (para sons e efeitos futuros)
`essencia_mudou(atual, maximo)` · `recarga_negada` · `especial_usado(nome)` · `acertou(alvo, dano, matou)` · `tiro_disparado(arma: WeaponData)`

## Checklist final
- [ ] Etapa 0: relatório entregue e aprovado
- [ ] `WeaponData` criado; revólver migrado sem mudar comportamento
- [ ] Armas como cópias; nível por cópia; fusão por soma (máx. 5, aviso de excesso); save v2 com conversão do v1
- [ ] Barra de Essência no HUD (tiro por arma, soco +12, regen 0,75/s), salva no save
- [ ] Recarga gasta essência; negada sem essência; pente por cópia
- [ ] Soco rápido (V) com arma na mão
- [ ] Mirar no botão direito (FOV, dispersão, velocidade)
- [ ] Especial na Q por arma (Tiro do Coveiro, Coice, Tiro Carregado); arma sem especial não faz nada
- [ ] 3 armas de teste no F3, fora da máquina
- [ ] Marcador de acerto + piscar branco + som; sem números flutuando
- [ ] Nada além disso foi alterado
