# Guia de estilo das armas (F3)

> Status: ✅ base aprovada pelo Gustavo (nov/2026) · 🟡 itens marcados como proposta
> Vale para **toda arma nova** e para o redesign do revólver. As referências visuais virão aos poucos, arma por arma.

## 1. Tema
**Roça + magia do sono.** São armas de fazendeiro — velhas, remendadas, "gambiarra da roça" — que, por estarem num **sonho**, ganharam um toque mágico.
- Ex.: pistola **enferrujada e cabreira** de fazendeiro; sniper = **rifle sucateado** de fazendeiro.
- A magia permite ser criativo: peças que não fariam sentido no mundo real podem existir (um cano de cano de regador, um tambor que é um pote de vidro…).

## 2. Proporções
- **Não são de brinquedo.** São armas com cara de arma, mas **mais leves** (menos massa, menos peças pesadas) e de **fazendeiro**: velhas, consertadas, simples.
- Variam por arma. O que vale para todas: **silhueta clara** vista em primeira pessoa (dá para reconhecer a arma só pela forma).
- Low-poly facetado (igual a tudo no jogo).

## 3. Paleta — "sonho feliz"
Cores **fortes e claras**. Nada de aço escuro realista; o tom mais escuro de uma arma não deve ficar perto do preto (só o contorno é escuro).

| Papel | Cor sugerida 🟡 | Uso |
|---|---|---|
| Metal pintado | `#8FB3C9` (azul-acinzentado claro) / `#9ED8B5` (verde-menta desbotado) | corpo, cano |
| Metal cru | `#B8C2CC` | partes sem pintura |
| Ferrugem | `#E07B39` / `#C9622B` | **manchas chapadas** (não textura) |
| Madeira | `#D9A15B` (mel) / `#A8693A` (mais escura) | cabo, coronha |
| Remendos | `#E5484D` (fita vermelha) / `#F2C94C` (fita amarela) / arame `#C8CDD2` | gambiarra |
| **Magia do sono** | `#B98CFF` (lilás, mesma da barra de Essência) + brilho `#E3D1FF` | peça mágica (ver item 6) |
| Contorno | marrom escuro (o mesmo dos braços) | casco invertido |

Cores de raridade **não** aparecem na arma (ver item 5).

## 4. Materiais
- **Formas puramente de cor**: cores chapadas por face/peça (cor por vértice), **sem textura** e com poucos detalhes modelados.
- **Fosco e sem reflexo:** roughness 1, specular 0, metallic 0. Nada com aparência de metal brilhante.
- Mesmo acabamento dos braços: **toon + contorno**.
- Qualquer detalhe além da forma/cor (brilho, fumaça, faísca, partículas) é **efeito visual adicionado depois**, no Godot — não vai no modelo.

## 5. Raridade
- Aparece **só na cor do nome** da arma (como no Terraria). O modelo não muda de cor por raridade.
- Quem diz se uma arma "merece" ser rara são o **dano e a mecânica**, não o visual.

## 6. Peça mágica (🟡 proposta do Claude — confirmar)
Toda arma tem **uma peça onde a Essência do Sonho entra**: um frasco, um cristal, um pote de vidro, uma câmara — em **lilás**.
- Explica a mecânica sem texto: a arma é "recarregada com essência" → a peça lilás **acende** na recarga e no especial (efeito no Godot).
- Cria uma assinatura visual comum a todas as armas, mesmo sendo muito diferentes.

## 7. Regras de animação e rig (já decididas)
- **Uma mão:** a mão esquerda fica **escondida na mesma pose do revólver** (o soco rápido `Soco_Esquerdo_Arma` funciona com qualquer arma).
- **Duas mãos:** `usa_duas_maos = true`; o V vira **coronhada** (animação própria).
- Arma é um **.glb separado** com rig próprio, presa no osso `Arma_R` (transform zerado); ações com o **mesmo nome e duração** nos dois .glb (`<Arma>_Sacar/Pose/Atirar/Cooldown/Recarregar/Guardar`); osso **`Cano`** na ponta do cano (origem do rastro/projétil).
- Cano **paralelo à câmera** (mira no centro da tela); prévias com a **câmera calibrada do jogo** e cruz no centro.
- Recuo do tiro é **por código** (`forca_recuo` e companhia): a animação de tiro pode ser curta/sutil.

## 8. Inimigos e bosses (I03)
Não há material padrão obrigatório. A única regra para tudo no jogo: **fosco e sem reflexo de luz** (nada com cara de metal).
