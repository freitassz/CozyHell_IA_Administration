# Revisão geral do jogo

> Lista viva de tudo que precisa ser decidido ou ajustado. Cada item tem um ID para a gente tratar **um por vez**.
> Status: 🔴 decidir · 🟡 em discussão · ✅ decidido (ir para `decisoes.md`) · ❌ descartado
> As propostas são opinião do Claude pensando no jogo e no público — não são decisão.

## Ordem sugerida
1. **Loop e progressão** (P01–P05): define o que o jogador faz e por que volta. Tudo o resto depende disso.
2. **Estilo** (I01–I04): resolve o choque fofo × armas.
3. **Multiplayer** (M01): decidir agora sai muito mais barato que depois.
4. **Escopo de conteúdo** (C01, C02, N01, N02).
5. Documentar sistemas existentes (S01–S04).

---

## I — Identidade e estilo

### I01 🔴 Mundo fofo × armas de fogo
- **Problema:** o mundo é claro e fofo; uma arma com cara de arma real (o R08 é aço, madeira e latão realistas) parece de outro jogo.
- **Observação:** a planilha **já aponta a solução** — quase todas as armas são objetos de fazenda/cozinha improvisados (rolha, sementes, pregos, panela de pressão, mangueira). O problema maior é o visual, não o conceito.
- **Proposta:** uma linguagem visual única para todas as armas:
  - "gambiarra da roça": feitas de objetos do dia a dia, com fita, arame, tábua;
  - proporções de brinquedo (grossas, exageradas, cano curto e largo);
  - cores da paleta do jogo (metal pintado, madeira clara, detalhes coloridos), nada de aço escuro realista;
  - mesmo shader toon + contorno das mãos;
  - efeitos coloridos e cartunescos: rolha, sementes, suco, estrelinhas — em vez de faísca e fumaça realista.
  - Referências de tom: Ratchet & Clank, Splatoon, Fortnite, Plants vs. Zombies: Garden Warfare.
- **Consequência:** o R08 provavelmente precisa de um redesign visual (as animações e o controlador `ArmaFps` continuam valendo).

### I02 🔴 O que é o "Hell" de CozyHell?
- **Problema:** hoje o "cozy" está claro (grama, cores), o "hell" não. Sem isso, armas e bosses parecem fora de lugar.
- **Opções:**
  - A) **Horta amaldiçoada:** a comida ganhou vida e virou monstro (já é o que os inimigos são). O inferno está nos inimigos, não no mundo.
  - B) **Dia cozy / noite hell:** a noite muda a luz, a névoa e a música, e os inimigos ficam mais fortes (combina com o loop do Muck).
  - C) **Corrupção progressiva:** a cada dia ou boss derrotado, o mundo vai ficando mais vermelho e escuro.
- **Proposta:** A + B (A é a história, B é o ritmo). C é mais caro e pode vir depois.

### I03 🔴 Shading e acabamento iguais em tudo
- **Problema:** as mãos usam toon + contorno; inimigos e bosses usam material Principled; os modelos antigos (PepperBoss, CowMellon, Carrot, Onion, pepper, Tomato, House, tree…) foram feitos por outro processo. Mistura de acabamentos é uma das maiores causas de "não parece o mesmo jogo".
- **Proposta:** definir **um** material padrão (ex.: toon + contorno) e testar todos os modelos com ele numa cena só. Listar quem destoa e decidir: ajustar, refazer ou tirar.

### I04 🔴 Violência e feedback de acerto
- **Proposta:** inimigos são comida, então a morte vira **suco, sementes e pedaços** — nada de sangue. Mantém o jogo para todas as idades e combina com o cozy.
- Para tiro: marcador de acerto na mira, som de acerto, inimigo reagindo (achatar, piscar branco) e, talvez, números de dano. Em FPS de tiro, o feedback de acerto vale mais que o modelo da arma.

---

## P — Loop e progressão

### P01 🔴 Para que serve a máquina depois de ter boas armas?
- **Problema:** no Muck, os itens **empilham** e o jogador fica sempre mais forte. Aqui a máquina dá **armas**, sem durabilidade e sem limite. Depois de 2 ou 3 armas boas, rodar a máquina perde o sentido e o loop principal morre.
- **Opções:**
  - A) **Repetidas sobem de nível** (estrelas): tirar a mesma arma de novo deixa ela mais forte.
  - B) **Roleta mista:** armas + itens passivos que empilham (como no Muck).
  - C) **Vender ou desmontar repetidas** por sucata ou dinheiro.
  - D) **Mods de arma** na roleta (ex.: "+1 projétil", "aplica Queimar").
- **Proposta:** A (simples, todo jogador entende, mantém o foco em armas) e talvez D depois. Atenção: A não conflita com "raridade é só etiqueta" (a raridade continua sem multiplicador; o nível é outra coisa).

### P02 🔴 Como é um dia de jogo?
- Definir o ciclo: explorar/coletar → ganhar R$/sucata → máquina → construir → noite/ataque → boss?
- **Hoje** os bosses só aparecem por ovo no modo criativo. Como aparecem no jogo normal? (dia fixo? altar? ovo achado no mapa?)

### P03 🔴 Duas moedas (R$ e sucata)
- Definir para que serve cada uma. Proposta: R$ = máquina; sucata = construção. Se uma não tiver uso claro, juntar numa só.

### P04 🔴 Como termina uma partida?
- Opções: derrotar os 5 bosses (com um final); sobreviver X dias; infinito com dificuldade crescente (Muck).
- Proposta: os 5 bosses formam a "campanha" e existe um modo infinito depois.

### P05 🔴 O que acontece quando morre?
- Roguelike (recomeça tudo, como no Muck)? Perde as armas? Em co-op, reviver amigo?

---

## C — Combate e armas

### C01 🔴 Foco é tiro, mas 15 das 35 armas são corpo a corpo
- **Problema:** 43% das armas são corpo a corpo, e ainda tem o soco. Isso contradiz o pilar "focado em tiro" e consome arte e animação.
- **Proposta:** reduzir o corpo a corpo para ~5 (uma por nicho) como "plano B" e investir o esforço nas armas de fogo.

### C02 🔴 Escopo das armas
- Cada arma = modelo + rig + ~6 animações + sons + efeitos + prompt. O R08 sozinho levou várias rodadas.
- **Proposta:** primeira versão jogável com **~12** armas (ex.: 1 por nicho de distância + algumas corpo a corpo + 2 lendárias); o resto vem em atualizações.

### C03 🔴 Recursos demais?
- Vida + stamina + energia de recarga + calor. Para um jogo "simples na essência", é bastante.
- A energia de recarga é a ideia mais original, mas pode frustrar: barra vazia = arma inútil.
- **Proposta:** prototipar cedo e ter uma rede de segurança (ex.: com a barra vazia, a recarga é lenta mas grátis). Avaliar se a stamina é necessária só para o especial — o cooldown já limita.

### C04 🟡 Raridade sem multiplicador
- Ok, mas a planilha precisa garantir que uma lendária **pareça** melhor ao usar. Verificar quando houver protótipo.

---

## N — Conteúdo (bosses e inimigos)

### N01 🔴 Quais são os 5 bosses?
- Candidatos (6): Dragão-Pitaya ✅, Tomate Boss, Uva-morcego, Batata-golem (refazer), PepperBoss (antigo), CowMellonBossTikiTiki (antigo).
- Definir os 5, a ordem de dificuldade e o bioma de cada um.

### N02 🔴 Elenco de ~8 inimigos com papéis diferentes
- Temos: Milho (atirador voador) + antigos (CowMellon, Carrot, Onion, pepper, Tomato).
- **Proposta:** uma tabela de papéis (corpo a corpo rápido, atirador, voador, tanque, enxame, kamikaze, suporte/cura, emboscada) e um inimigo por papel. Num jogo de tiro, a variedade de **como** o inimigo se move importa mais que a aparência.

### N03 🔴 Inimigos por bioma
- Ligar cada inimigo e boss a um bioma.

---

## S — Sistemas existentes (documentar)

### S01 🔴 Construção
- Para que serve? Defesa da base (o HUD tem "defesa")? Os inimigos atacam a base? Isso muda muito o jogo (vira meio tower defense).

### S02 🔴 Biomas e geração procedural
- Quais biomas, o que tem em cada um, o que falta.

### S03 🔴 Ferramentas e plantio
- Existem pá, enxada e machado, e plantar sementes. Tem agricultura? Se tem, como se liga ao resto (dinheiro? comida? vida?).

### S04 🔴 Mesa, monumento e outros interativos
- Documentar o que são e para que servem.

---

## M — Multiplayer

### M01 🔴 Decidir agora se vai ter
- **Problema:** colocar multiplayer num jogo pronto é das coisas mais caras e arriscadas que existem. E o público de jogos tipo Muck joga **muito em grupo** — para esse público, o co-op é quase parte do núcleo.
- **Proposta:** decidir já. Se a resposta for "sim, no futuro", adotar regras desde agora:
  - nada de `Engine.time_scale` (a câmera lenta da entrada de boss trava o jogo de todos) → câmera lenta só visual/local;
  - estado do jogo num lugar só (quem manda é o servidor/host);
  - geração procedural por **seed**;
  - código que não assume "um jogador só" (ex.: inimigo persegue o jogador mais próximo, não "o player");
  - decidir: roleta e drops por jogador ou compartilhados; vida de boss escalando com nº de jogadores.

### M02 🔴 Prompts do Ziva "prontos para multiplayer"
- Se M01 for sim, todo prompt novo ganha uma seção com essas regras.

---

## T — Técnico e processo

### T01 🔴 O projeto Godot está versionado (git)?
- Se não estiver, um arquivo corrompido ou uma mudança errada do Ziva pode perder trabalho. Proposta: repositório próprio para o projeto, com Git LFS para os `.glb`, `.wav` e `.png`.

### T02 🔴 Prompts antigos fora deste repo
- Subir as cópias para `prompts/`.
