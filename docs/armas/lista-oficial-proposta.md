# Lista oficial de armas — proposta v1 (12 armas)

> Status: 🟡 proposta do Claude para o Gustavo aprovar/cortar/mudar. Depois vira a planilha (A03).
> Critério: **12 armas, cada uma com uma sensação diferente**; variações (versões de cada uma) vêm depois.
> Nomes vêm da planilha de rascunho, com exceção do Estilingue (que agradou no teste).

## Distribuição por raridade (= quando aparece na máquina)
| Raridade | Libera quando | Qtde | Por quê |
|---|---|---|---|
| Comum | início | 4 | o começo já tem variedade: pistola, escopeta, automática e carregável |
| Raro | Tomate morto | 3 | sniper, arremesso e o único corpo a corpo |
| Épico | Dragão morto | 3 | perfuração, explosão e fogo contínuo |
| Lendário | Batata morta | 2 | mecânicas únicas (vórtice, torreta) |

Armas **exclusivas de boss** (bigorna) ficam **fora** destas 12.

## As 12
| # | Arma | Raridade | Nicho | Tiro | Auto | Carreg. | Mãos | Especial (ideia) | Papel / sensação |
|---|---|---|---|---|---|---|---|---|---|
| 1 | **Revólver do Coveiro** ✅ | Comum | Pistola | Instantâneo | não | não | 1 | **Tiro do Coveiro** (×3, atravessa, empurra) | arma de confiança, precisa |
| 2 | **Espingarda de Rolha** | Comum | Shotgun | Projétil (rolhas) | não | não | 2 | **Coice** (rajada que te joga para trás) | perto e forte, pulo de fuga |
| 3 | **Metralhadora de Sementes** | Comum | Rifle automático | Projétil rápido | **sim** | não | 2 | — | segurar e espalhar sementes |
| 4 | **Estilingue de Forquilha** | Comum | Arremesso / arco | Projétil com arco | não | **sim** | 1 | — | puxar e acertar longe; habilidade pura |
| 5 | **Rifle de Pressão** | Raro | Sniper | Instantâneo | não | não | 2 | **Tiro Carregado** (segura F, atravessa todos) | sniper sucateado de fazendeiro |
| 6 | **Machadinha de Lenha** | Raro | Arremesso | Projétil girando | não | não | 1 | **Bumerangue**: volta acertando no caminho | crava no inimigo e "recarrega" pegando de volta |
| 7 | **Frigideira de Ferro** | Raro | Corpo a corpo | Golpe | — | — | 1 | **Panelada**: rebate projéteis por ~1 s | enche **muita** essência (mais que o soco); para quem gosta de perto |
| 8 | **Rifle de Pregos** | Épico | Rifle | Instantâneo | não (semi rápido) | não | 2 | **Pregar**: prende o inimigo no chão por ~2 s | pregos **atravessam** 2 inimigos |
| 9 | **Bazuca de Panela de Pressão** | Épico | Explosivo | Projétil com arco | não | não | 2 | — | explosão em área; o apito da panela antes de estourar |
| 10 | **Lança-Chamas de Fogão** | Épico | Contínuo | Jato curto | contínuo | não | 2 | — | **Queimar**; superaquece |
| 11 | **Liquidificador Demoníaco** | Lendário | Contínuo | Jato/vórtice | contínuo | não | 2 | **Batida**: solta todos os sugados de uma vez | **puxa** inimigos para um ponto |
| 12 | **Relógio de Cuco Maldito** | Lendário | Armadilha | Arremesso | não | não | 1 | **Hora Cheia**: onda que atordoa | joga um cuco-torreta que bica sozinho (~7 s) |

## O que cada arma exige de sistema novo (honestidade de escopo)
| Arma | Já funciona hoje? | Sistema novo necessário |
|---|---|---|
| Revólver, Espingarda, Metralhadora, Estilingue, Rifle de Pressão | ✅ tudo existe (instantâneo, projétil, automática, carregável, especiais) | só modelo/animação e números |
| Machadinha | 🟡 | arremesso que **crava e volta** (recarga = pegar de volta) |
| Frigideira | 🟡 | **arma corpo a corpo** (golpe com hitbox, sem pente) + rebater projéteis |
| Rifle de Pregos | 🟡 | **perfuração** no tiro normal; status "preso" |
| Bazuca | 🟡 | **explosão em área** (`raio_explosao_m`) |
| Lança-Chamas | 🔴 | **tiro contínuo** + **superaquecimento (C06)** + status **Queimar** |
| Liquidificador | 🔴 | tiro contínuo + **puxar** inimigos |
| Relógio de Cuco | 🔴 | **torreta** temporária + atordoar em área |

Ordem natural de produção: as 5 que já funcionam → Machadinha/Frigideira/Pregos/Bazuca → Lança-Chamas/Liquidificador/Relógio.

## Perguntas para o Gustavo
1. Aprova as 12? Troca alguma? (candidatas fora: Faca do Chef Eterno, Tridente do Churrasco, Foice da Colheita Final, Caldeirão-Canhão da Vovó, Fuzil do Espantalho, Canhão de Sal Grosso, Mangueira de Jardim, Besta de Estaca…)
2. **1 corpo a corpo (Frigideira)** está bom, ou quer 0 / 2?
3. O **Revólver** fica Comum (é a arma inicial de teste) — ok?
4. Os especiais propostos fazem sentido? Quais armas ficam **sem** especial?
5. Superaquecimento (C06): o Lança-Chamas é o lugar para decidir. Entra?
