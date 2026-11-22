# PROMPT ZIVA — Trocar o visual provisório pelo modelo (modelo de uso geral)

> Use este prompt **sempre** que o chat de modelagem entregar uma ou mais armas. Cole abaixo o bloco **"Dados para o Ziva"** que o chat de modelagem devolveu.

## DADOS DO CHAT DE MODELAGEM
```
(COLE AQUI)
```

## O que fazer (para cada arma dos dados)
- **Não mude o que não está pedido.** Comente em português.
1. Troque o visual provisório (bloco ou revólver) pelo `.glb` indicado, no encaixe indicado (`Arma_R` com transform zerado, salvo se os dados disserem outro).
2. `prefixo_anim` da arma = prefixo das ações dos dados; toque o **mesmo nome** nos braços e na arma. Use o `bracos.glb` novo se veio junto e confira que **as outras armas e o soco esquerdo continuam iguais**.
3. Ligue os **eventos** dos dados: momento do tiro/arremesso, impacto do golpe/coronhada, munição/cristal entrando na recarga. Tempos ÷ velocidade da animação. Golpes corpo a corpo: o visual agora é a animação (remova o golpe por código), mantendo os tempos de ativo/recuperação/preparo do `WeaponData` (se a animação tiver outra duração, me avise).
4. Material: toon fosco com contorno (textura assada → `albedo_texture`). Se houver `EssenciaMagica`, ligue a cor ao cristal/recarga/especial como já existe.
5. Rastro/projétil saem do osso `Cano` (armas de tiro). Ajuste `offset_posicao`/`offset_rotacao_graus` para a arma ficar **embaixo à direita**; confira com captura que a mão esquerda escondida (armas de 1 mão) não aparece.
6. Coloque a arma na **máquina caça-níquel** na raridade dela (se ainda não estiver).
7. Rode os validadores dessa arma e me diga o placar.

## Checklist
- [ ] Modelo no lugar do provisório · [ ] Ações e eventos ligados · [ ] Material e `EssenciaMagica`
- [ ] Posição à direita · [ ] Outras armas intactas · [ ] Na máquina · [ ] Placar · Nada além disso foi alterado
