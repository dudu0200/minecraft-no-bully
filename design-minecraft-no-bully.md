# Mashup: Minecraft dentro do Bully

Cole este arquivo no final do prompt do Melty (abaixo da linha "If anything is written below this line"). O agente deve pular as perguntas e começar a construir.

## Decisões do design (já respondidas pelo usuário)

- **Ideia:** Minecraft dentro do Bully: Scholarship Edition.
- **Jogo principal (host, role "primary"):** Bully: Scholarship Edition. Mantenha esta escolha; a ausência do Bully no catálogo do Melty não justifica trocar os jogos.
- **Companheiro (role "companion"):** Minecraft: Java Edition. Texturas e sons dos blocos são lidos da cópia instalada do jogador via `{game:minecraft-java}`. Nada do Minecraft é copiado para o upload.
- **O que o Minecraft traz:** blocos. O jogador quebra e coloca blocos pelo campus de Bullworth.
- **Primeiro minuto:** o jogador segue a história normal do Bully, mas com todas as funções do Minecraft ativas o tempo todo. Os blocos colocados são sólidos e afetam o próprio Jimmy (colisão, ele pode subir neles, ficar preso etc.).
- **Modo:** solo. Sem multiplayer (não configurar recipe.multiplayer).
- **Primeira versão jogável deve ter:**
  1. Quebrar e colocar blocos com colisão real.
  2. Texturas e sons do Minecraft lidos da cópia do jogador.
  3. Inventário com hotbar.
  4. Vários tipos de bloco: terra, pedra, madeira.

## Pontos de atenção para o agente

1. O Bully não tem loader no Melty. Escolher a rota de modding (plugin ASI/DLL, script hook ou similar) a partir dos arquivos do jogo e de `game_info`, e empacotar o que precisar no release se a licença permitir. Rodar `one_click_check` cedo.
2. Colisão real com blocos novos é a parte mais difícil no motor do Bully. Se for inviável, explicar ao usuário e pedir concordância antes de mudar o design.
3. Não copiar texturas ou sons do Minecraft. Ler da pasta do jogador em tempo de execução.
4. Chamar `search_mashups` antes de construir, caso algo parecido já exista.

## Planilhas (fonte da verdade)

Altere a planilha antes do código. Toda linha e coluna precisa estar preenchida e verificada antes do build (preflight).

```json
{
  "blocks": [
    {"id": "dirt", "texture": "block/dirt.png", "breakSound": "dig/gravel", "placeSound": "dig/gravel", "hardness": 0.5, "solid": true},
    {"id": "stone", "texture": "block/stone.png", "breakSound": "dig/stone", "placeSound": "dig/stone", "hardness": 1.5, "solid": true},
    {"id": "oak_planks", "texture": "block/oak_planks.png", "breakSound": "dig/wood", "placeSound": "dig/wood", "hardness": 2.0, "solid": true}
  ],
  "inventory": [
    {"slot": 1, "block": "dirt", "startCount": 64},
    {"slot": 2, "block": "stone", "startCount": 64},
    {"slot": 3, "block": "oak_planks", "startCount": 64}
  ],
  "systems": [
    {"id": "place_block", "input": "botão direito", "range": 5, "effect": "cria bloco no grid; colisão com o Jimmy"},
    {"id": "break_block", "input": "botão esquerdo", "range": 5, "effect": "remove o bloco e devolve ao inventário"},
    {"id": "hotbar_select", "input": "teclas 1-9 / scroll", "effect": "troca o bloco ativo"}
  ],
  "hooks": [
    {"id": "player_position", "target": "Bully: posição e hitbox do Jimmy", "status": "a descobrir"},
    {"id": "camera_raycast", "target": "Bully: câmera para apontar o bloco", "status": "a descobrir"},
    {"id": "world_collision", "target": "Bully: colisão do mundo", "status": "a descobrir"},
    {"id": "minecraft_assets", "target": "{game:minecraft-java} jar de assets e sons", "status": "a descobrir"}
  ]
}
```

## Listagem (rascunho; o agente pode ajustar com base no build real)

- **Título:** Minecraft em Bullworth
- **Tagline:** Siga a história do Bully, mas com blocos de Minecraft.
- **Descrição:** Jogue Bully: Scholarship Edition normalmente, mas agora você pode quebrar e colocar blocos de Minecraft por todo o campus. Os blocos são sólidos e afetam o Jimmy. Requer Bully: Scholarship Edition e Minecraft: Java Edition instalados.
- **Créditos, licença e remix:** perguntar ao usuário. Não adivinhar.
