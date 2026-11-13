# Pipeline de produção

Resumo de como cada coisa é feita. Detalhes técnicos completos estão nas skills
`lowpoly-game-3d-blender` e `cozyhell-prompts-ziva`.

## Modelo 3D (Blender via Python)
1. Analisar a referência (formas, cores, proporções, medidas).
2. Modelar 100% procedural, low-poly facetado.
3. **Imagem de teste** (1 pose) → aprovação do Gustavo.
4. Renderizar as mesmas vistas da referência e comparar; iterar uma mudança por vez.
5. Rig + animações em etapas (emendas verificadas por código).
6. Exportar `.glb` + `.blend` + `.py` + pranchas + `*_dados.json` + mapa FX.

## Sons
- Sintetizados com numpy/scipy (WAV 44,1 kHz, 16-bit, estéreo).
- Sincronizados com quadros da animação; volume por RMS; loops com chunk `smpl`.
- O Claude não escuta: valida por forma de onda/espectrograma.

## Prompt para o Ziva
Arquivo `PROMPT_ZIVA_<ASSUNTO>.md`: contexto → "Não mude o que não está pedido" → tabela de arquivos → dados exatos → ETAPAS com teste → sinais → checklist → "Comente o código em português". Sons em prompt separado.

## Entrega
Subpasta por asset em `3dddddd\Blender\<asset>\`, sons em `sons\`. Cópia do prompt também em `prompts/` deste repo.
