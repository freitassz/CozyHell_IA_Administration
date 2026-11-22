# Pedido para o chat de modelagem — Armas de tiro (2ª leva): Rifle de Pregos, Lança-Rojão Junino, Lança-Chamas de Fogão, Mangueira de Água Amaldiçoada, Lampião

> Siga também `PROMPT_BLENDER_REGRAS_ARMAS.md`. Aparência: o Gustavo descreve. **Uma arma por vez**, nesta ordem. Silhuetas bem diferentes entre si e das armas que já existem.

| Arma | Mãos | O que o jogo faz | Ações (além de `_Sacar/_Pose/_Guardar`) | Extras |
|---|---|---|---|---|
| **Rifle de Pregos** (Épico) | 2 | tiro instantâneo de pregos que atravessam inimigos | `_Atirar`, `_Cooldown`, `_Recarregar` (informe quando o pente enche), `_Coronhada` | osso `Cano` |
| **Lança-Rojão Junino** (Épico) | 2 | dispara um rojão de festa junina (projétil) que explode em confete | `_Atirar`, `_Recarregar` (põe um rojão novo; informe o momento), `_Coronhada` | `rojao.glb` separado (o projétil, ~1 m de base); bandeirinhas são bem-vindas |
| **Lança-Chamas de Fogão** (Épico) | 2 | jato contínuo de fogo; **cristal do sono** escurece com o uso (superaquecimento) | `_Atirar` (**loop** enquanto segura), `_Recarregar` (gesto de "recarregar o cristal", informe o momento) e `_Coronhada` | **obrigatório:** cristal como objeto/material `EssenciaMagica`; osso `Cano` na boca do jato |
| **Mangueira de Água Amaldiçoada** (Lendário) | 2 | jato contínuo de água amaldiçoada | `_Atirar` (**loop**), `_Recarregar` (cristal), `_Coronhada` | se tiver cristal, `EssenciaMagica`; osso `Cano` no bico |
| **Lampião** (raridade a definir) | **1** (esquerda escondida) | tiro lento de **bola de fogo** que queima | `_Atirar`, `_Cooldown`, `_Recarregar` (informe o momento) | a chama do lampião = objeto/material separado `ChamaLampiao` (o Godot faz brilhar); osso `Cano` de onde a bola sai |

## Devolver
Bloco "Dados para o Ziva" das regras comuns, por arma.
