---
name: carrossel-editorial-animado
description: Cria CARROSSEL ANIMADO de Instagram (8 slides 1080×1350) no estilo EDITORIAL CIENTÍFICO CLARO com movimento em HTML/CSS/SVG puro — cada slide tem uma CENA ILUSTRADA que demonstra a analogia (fábrica de engrenagens, chave de ignição, xícaras de café, nuvem + medidor, balança, fileira de pessoas), uma ENTRADA DE TÍTULO diferente por slide (blur, wipe, rise, track, skew, pop), palavra-chave em serifa itálica no acento, hélice de DNA 3D na capa e livro 3D com brilho no CTA. O mesmo arquivo exporta PNG no estado final (modo .static). Lê marca e design system do projeto (design-systems/*/dna.json, marca.md, product.md). Use quando o usuário pedir "carrossel animado", "carrossel com movimento", "versão animada do carrossel", "anima esse carrossel", "carrossel com ilustrações que se mexem", mesmo sem citar a skill. Versão parada é `carrossel-editorial-estatico`.
---

# Carrossel editorial animado (8 slides, CSS/SVG)

Padrão aprovado no projeto *O Despertar do Código* (out/2026): "7 genes do laudo — versão animada".
**Olhe `reference/folha-estado-final.png` antes de começar** (os 8 slides no estado final, que é o PNG exportado).
O HTML completo está em `template/exemplo-animado.html` — **parta dele**: ele já tem todas as peças
(hélice, entradas de título, cenas, modo export). Troque conteúdo e cenas; não reescreva a base.

É a versão "viva" do `carrossel-editorial-estatico`: mesma grade, topo, rodapé, tags e arco de 8 slides
(leia aquela skill para estrutura, arco e regras de copy). O que muda está abaixo.

## 1. Preparar

1. Leia `design-systems/*/dna.json`, `marca.md`, `product.md`, `publico.md`, `memory/MEMORY.md` (igual ao estático).
2. `brix content new "Título — versão animada" --estilo animado` → use a pasta devolvida.
3. Copie `template/fonts/*` (Inter + **Playfair itálico**) para `<peça>/fonts/` e as imagens do projeto
   para `<peça>/images/` (`logo.png`, `expert-recorte.png`, `expert-limpa.jpg`, `livro.jpg`).
4. Copie `template/exemplo-animado.html` → `<peça>/preview.html`.

## 2. Diferenças visuais em relação ao estático

- **Tema claro**: fundos alternando `--bg #FFFFFF`, `--bg2 #F4F5F3`, `--bg3 #EEF3EF`; tinta `#1C1C1A`,
  texto secundário `--mute #5A605D`. Acentos escurecidos pra texto (`--blueD`, `--greenD`) e um
  **`--warn` terroso (#C65A36)** só para o lado "ruim" da comparação (toxicidade, ativação reduzida, metabolizador lento).
- **Vinheta suave** em todo slide (`.slide::after`, radial 6%).
- **Palavra-chave do título em serifa itálica** (`<span class="i">` → Playfair Italic 600 no acento escuro):
  "O paciente médio *não existe.*", "Risco *não é sentença.*". Uma por título, sempre a virada da frase.
- **Texto mais curto** que no estático (o desenho explica): parágrafo ≤ 25 palavras, sem caixa de analogia —
  **a analogia vira a cena**.
- O `.num` vazado fica menor (140px, 20% de opacidade), posicionado ao lado da cena e flutuando devagar.
- Layout do slide: topo → tag → sub-rótulo → título → parágrafo curto → **`.scene`** (área de 440px de altura
  em `top:736px`), com chão em perspectiva opcional (`.floor`, grade 60px que some com máscara).

## 3. Cada slide = uma cena que demonstra a analogia

Escolha a cena pela analogia do item. Modelos prontos no template:

| Analogia | Cena (classes no template) | Movimento |
|---|---|---|
| Média × indivíduo | `.pop-row` de `.person` com alturas diferentes + linha tracejada "A MÉDIA"; um destacado "SEU PACIENTE" | pessoas balançam fora de fase, linha da média oscila |
| Velocidade de metabolismo (3 níveis) | `.lane` lento/normal/ultra: cápsula → engrenagem (`--sp` = velocidade) → fluxo de moléculas (`data-dots`, `data-dur`) → selo de resultado | engrenagens em velocidades diferentes; ultra com selo pulsando em alerta |
| Ativação / pró-fármaco | dois `.ign` com motor 3D e chave (`#key`) | chave entra e gira; faísca forte num lado, fraca e falhando no outro |
| Rápido × lento (substância fica/sai) | duas `.cupbox` com xícara SVG (`#cup`), vapor e `.meter` | barra esvazia rápido num lado, quase nada no outro |
| Probabilidade, não destino | nuvem + sol + chuva (`.rain data-drops`) + `.gauge` com agulha | nuvem deriva, chuva cai, agulha oscila numa faixa |
| Peso diferente / hype | `.scale` com `.beam` e dois `.pan` (bloco sólido × caixa tracejada com `.ripple`) | balança pende pro lado pesado e balança de leve |

Criando cena nova: só HTML + CSS + SVG inline (`<symbol>` no fim do arquivo, reutilizado com `<use>`),
gradientes suaves e sombras projetadas pra dar volume "3D de produto", nas cores da paleta. Sem imagem gerada, sem lib.

## 4. Coreografia

- **Capa: tudo visível no 1º quadro** (é a miniatura da grade). Só laços decorativos: hélice de DNA 3D girando
  atrás do expert (`.helix data-n data-w data-gap`, montada pelo JS), halo pulsando, brilho passando na pílula,
  `ARRASTE →` cutucando.
- **Slides 2–8**: tag entra com mola (`.ent-tag`), título com **uma entrada diferente por slide** — não repita
  em slides vizinhos:
  `blur split` (palavras saem do desfoque) · `wipe` (barra no acento revela) · `rise` (linhas sobem por trás
  da base; marque `.ln`) · `track` (letras se aproximam) · `skew` (entra de lado) · `pop split` (palavras estouram).
  Depois parágrafo (`.ent-fade`, 0,55 s) e cena (`.ent-scene`, 0,35 s com leve overshoot).
- Tudo de entrada termina em **≤ 1,5 s**; depois só **loops lentos e contínuos** (2–9 s) na cena. Nada pisca rápido.
- **CTA**: raios girando bem devagar atrás do livro 3D (rotação suave + reflexo passando), avatar com anel no
  acento, botão com brilho e pulso de sombra.
- Easings: `cubic-bezier(.2,.8,.2,1)` para entradas, `(.3,1.4,.4,1)`/`(.3,1.6,.45,1)` para mola.

## 5. Estado final / export (obrigatório)

- `#export=N` adiciona `.static` no `<html>`: **todas as animações desligam** e o slide fica no estado final.
  Toda animação nova precisa de uma regra `.static …` que deixe o elemento numa pose bonita e legível
  (moléculas espalhadas na pista, chave virada, agulha no meio da faixa, balança inclinada, gotas visíveis).
  Elementos com `opacity:0` no início do keyframe **têm** que ficar visíveis no `.static`.
- Entradas usam `animation-fill-mode: both` → o estado final é o legível.
- Mantenha `@media (prefers-reduced-motion: reduce)`.

## 6. Mostrar, conferir, exportar

```bash
brix content preview "<caminho absoluto>/preview.html"   # o app mostra animado; rode de novo após editar
brix content export "<pasta da peça>"                    # PNG de cada slide no estado .static
brix content list
```
Confira os PNGs exportados (nenhuma cena vazia ou elemento invisível) e o preview animado (entradas terminam
rápido, loops não distraem da leitura). Para publicar como vídeo, grave cada slide do preview (5–8 s, 1080×1350)
ou leve as cenas para Remotion — mas a peça aprovada aqui é o HTML animado + os PNGs.
