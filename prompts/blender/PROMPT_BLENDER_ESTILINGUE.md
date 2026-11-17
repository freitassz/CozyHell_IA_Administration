# Pedido para o chat de modelagem — Estilingue de Forquilha

> Use a skill `lowpoly-game-3d-blender`. Pasta sugerida: `Blender\armas\estilingue\`.
> **Aparência (do Gustavo):** forquilha de **madeira** com uma **fita branca enrolada** no cabo. O resto da aparência o Gustavo descreve aqui no chat (ex.: cor do elástico).

## Contexto
O Estilingue já funciona no jogo como arma de teste (usando o visual do revólver). Agora ganha modelo e animações próprios.
É uma arma **carregável**: segurar o botão **puxa** o elástico (até ~1,0 s para a carga cheia), soltar **atira** uma pedra que faz **arco** (vai mais longe quanto mais puxou).
Comum, pente de 8 pedras, recarga ~1,0 s, cadência 1,5/s.

## Estilo geral (guia aprovado)
- Roça + magia do sono: coisa de fazendeiro, velha, remendada. Não é de brinquedo, mas é leve.
- Cores fortes e claras; nada perto do preto (só o contorno). Fosco e sem reflexo. Sem magia (não precisa de `EssenciaMagica`).

## Mãos: estilingue usa as DUAS mãos
- **Mão esquerda segura a forquilha** à frente; **mão direita segura a bolsa** (com a pedra) e **puxa** o elástico para trás.
- No jogo isso vira `usa_duas_maos = true`: o golpe rápido (V) é uma **coronhada** — aqui, um **golpe curto com a forquilha**.
- Mantenha o padrão de encaixe que o código usa (arma presa no `Arma_R`, transform zerado). Se para o estilingue fizer mais sentido a forquilha seguir a **mão esquerda**, pode — **avise** como ficou, porque o código precisa saber.
- O elástico precisa **esticar de verdade**: tiras deformadas por ossos entre as pontas da forquilha e a bolsa (ex.: osso `Bolsa`). A pedra na bolsa pode ser um osso/objeto (`Pedra`) que some ao soltar.

## Ações (30 fps), prefixo `Estilingue_`
| Ação | O que mostra | Duração base |
|---|---|---|
| `_Sacar` | tira o estilingue e já com uma pedra na bolsa | ~0,5 s |
| `_Pose` | parado, elástico solto, pedra na bolsa (**loop**) | ~2,0 s |
| `_Puxar` | do elástico solto até **totalmente puxado** | ~1,0 s (= carga cheia) |
| `_Atirar` | **solta**: a bolsa volta, a pedra sai | ~0,15 s |
| `_Cooldown` | pega a próxima pedra e põe na bolsa | ~0,5 s |
| `_Recarregar` | pega um punhado de pedras do bolso e coloca na bolsa | ~1,0 s |
| `_Guardar` | guarda | ~0,4 s |
| `_Coronhada` | golpe curto com a forquilha para a frente, **sem tapar a mira** | ~0,6 s |

**Importante sobre `_Puxar`:** o código **não** vai tocar essa ação normalmente; ele vai posicionar o tempo dela pela carga (carga 50% = meio da ação). Então ela deve ser **contínua e linear o bastante** para qualquer quadro servir de pose parada. O último quadro de `_Puxar` deve emendar com o primeiro de `_Atirar`, e qualquer quadro de `_Puxar` deve poder ir para `_Atirar` sem pulo feio (se não der, avise).

## Regras técnicas (iguais às outras armas)
- `.glb` separado com rig próprio; ações com **mesmo nome e duração** nos braços e na arma; **sem quadro parado no início**; emendas = 0; `bracos.glb` e o glb da arma **sempre juntos**; `export_force_sampling=False`.
- Osso **`Cano`** = de onde a pedra sai (entre as pontas da forquilha), apontando para a frente, **paralelo à câmera** (mira no centro). Correção de eixo da exportação como nas outras armas.
- Prévias com a **câmera calibrada do jogo** e a cruz no centro.
- O recuo é procedural no jogo: `_Atirar` pode ser curta.

## Entregar
1. `estilingue.glb` + `bracos.glb` + `.py`.
2. Prancha: lateral, 3/4 e **primeira pessoa** com o elástico solto, meio puxado e todo puxado.
3. **Dados para o Ziva** (trazer ao chat de administração):
   - arquivo, nó raiz, e em que osso a arma está presa (`Arma_R` ou outro);
   - ações com **duração (s)** e nº de quadros;
   - em que momento do `_Atirar` a pedra sai;
   - **impacto da coronhada**;
   - em que momento do `_Cooldown` e do `_Recarregar` a pedra/pente entra;
   - ossos especiais (`Bolsa`, `Pedra`, …).
