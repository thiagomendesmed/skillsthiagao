---
name: carrossel-editorial-estatico
description: Cria CARROSSEL ESTÁTICO de Instagram (8 slides 1080×1350, PNG) no estilo EDITORIAL CIENTÍFICO — grade de linhas finas de 1px, numeração grande vazada (outline), tag em pílula, título curto em Inter 800, parágrafo didático, caixa de ANALOGIA, citação da fonte no rodapé, capa com foto do expert recortada e CTA claro com o produto. Lê a marca e o design system do projeto (design-systems/*/dna.json, marca.md, product.md, publico.md) e escreve um único preview.html em tira horizontal, exportado pelo app Carousel do BRIX. Use quando o usuário pedir "carrossel estático", "carrossel educativo", "carrossel editorial", "carrossel científico/médico", "faz um carrossel igual aos dos genes", "carrossel de X passos / X itens", "carrossel em PNG", mesmo sem citar a skill. Versão com movimento é `carrossel-editorial-animado`.
---

# Carrossel editorial estático (8 slides, PNG)

Padrão aprovado no projeto *O Despertar do Código* (ebook de genética para médicos, out/2026).
**Antes de começar, olhe as folhas em `reference/`** — são o resultado que se espera:

- `folha-os-genes-do-laudo-…png` → versão **escura** (fundo #1C1C1A), lista de itens
- `folha-como-ler-um-laudo-…png` → versão **clara**, passo a passo
- `folha-farmacogenetica-…png` → versão **clara**, lista de itens com sub-rótulo (gene)

Os HTMLs que geraram cada folha estão em `template/` (`exemplo-escuro.html`, `exemplo-claro-passos.html`,
`exemplo-claro-lista.html`). **Parta sempre de um deles** — copie, troque paleta/conteúdo. Não reescreva do zero.

## 1. Ler antes de escrever (na pasta do projeto)

1. `design-systems/*/dna.json` → paleta (`fundo`, `texto`, `acento`, `acento_suave`), tipografia, vibe.
   Sem dna.json: use `marca.md` e pergunte só a cor de acento.
2. `marca.md` (tom e proibições), `product.md` (promessa, preço, nome), `publico.md` (pra quem fala),
   `angles/angles.json` e `copy/` se existirem (ângulos e frases já aprovadas).
3. `assets/` → logo (PNG com fundo transparente), foto do expert **recortada** (PNG sem fundo), foto limpa
   (pro avatar redondo do CTA), capa/mockup do produto. Nunca invente foto, nome ou arroba.
4. `memory/MEMORY.md` se existir (o que o dono já aprovou/recusou).

## 2. Criar a peça (BRIX)

```bash
brix content new "Título curto do assunto"      # devolve a pasta content/AAAA-MM-DD-slug/
```
Use **exatamente** a pasta devolvida. Copie para ela:
- `template/fonts/*` → `<peça>/fonts/` (Inter 400/500/700/800, OFL; nunca fonte online — o export roda offline)
- logo, foto recortada, foto limpa e capa do produto → `<peça>/images/` (`logo.png`, `expert-recorte.png`,
  `expert-limpa.jpg`, `livro.jpg` — mantenha esses nomes que o template já usa)
- o template escolhido → `<peça>/preview.html`

Fora do BRIX: mesma estrutura numa pasta qualquer; para PNG use o Chrome headless abrindo
`preview.html#export=N` em janela 1080×1350.

## 3. Estrutura fixa do HTML

- **Uma tira**: `body` e `.strip` com 8640×1350 (8 × 1080), cada `<section class="slide">` 1080×1350,
  `padding: 0 96px`. Manter o `<script>` do fim (modo `#export=N` mostra só o slide N — é o que o export usa).
- **Grade de linhas finas (1px)** em todo slide: `.grid-v` (vertical em x=96), `.grid-h` (horizontal em y=176),
  `.grid-f` (horizontal a 150px do fundo). Cor: branco 14% no escuro, preto 13–14% no claro.
- **Topo (176px)**: logo 46px + nome da marca em caixa alta, 19px, peso 500, `letter-spacing:.32em`;
  à direita a paginação `01 / 08` (20px, tracking .2em, opacidade .7).
- **Rodapé (150px)**: à esquerda uma palavra-chave da marca em acento (`EXCLUSIVO PARA MÉDICOS`,
  `MEDICINA DE PRECISÃO`), 18px, tracking .3em; à direita `ARRASTE →`.
- **Corpo** (padding-left 32px a partir da linha vertical), nesta ordem:
  1. `.num` — número grande vazado: 150–170px, peso 400, `color:transparent; -webkit-text-stroke:1.5px` (55% no escuro, ~20% no claro). `00` = contexto, `01…06` = itens, faixas tipo `05–07` quando agrupar.
  2. `.tag` — pílula com borda 1px no acento, 19px, caixa alta, tracking .28em (categoria do item).
  3. `.gene` (opcional) — sub-rótulo técnico em acento suave, 24–26px, peso 700, tracking .3em (gene, fármaco, sigla).
  4. `h2` — **a tese do slide**, 70px, peso 800, `line-height:1.04`, `letter-spacing:-.02em`, máx. ~880px.
  5. `p` — 31–33px, `line-height:1.45`, opacidade .86, `<b>` nos 1–2 termos-chave.
  6. `.analogia` — borda esquerda 2px no acento suave, rótulo `ANALOGIA` (18px, tracking .3em) + frase 34px peso 500.
  7. `.fonte` (quando houver dado/estudo) — 16–17px, opacidade .45, logo acima da linha do rodapé. Formato Vancouver curto: `Autor X et al. Revista. Ano;vol(n):pág.`
- **Curva orgânica** (SVG, traço 2px, 18–28% de opacidade, saindo pela borda direita) em slides alternados — lembra molécula, quebra a rigidez da grade.

## 4. Arco dos 8 slides

| # | Papel | Como fica |
|---|---|---|
| 1 | **Capa** (é a miniatura do perfil) | pílula sólida no acento (`EXCLUSIVO PARA …`), `h1` 80px com a promessa numérica ("7 genes que…", "6 fármacos…", "Como ler … em 6 passos"), subtítulo de 1–2 linhas com a dor ("E o que a faculdade não te ensinou…"). Foto do expert recortada à direita, P&B (`grayscale(1) contrast(1.05)`), halo radial no acento atrás, e ao fundo texto técnico repetido a 5–7% de opacidade (siglas do tema). Rodapé com a palavra-chave da marca. |
| 2 | **Contexto `00`** | por que isso importa: o erro comum / a crença a quebrar. |
| 3–7 | **Itens / passos `01…`** | um item por slide. Dá pra agrupar os dois últimos num slide de **2 colunas** (contraste: "muda a conduta" × "superinterpretado") separadas por linha de 1px. |
| 8 | **CTA** — sempre **claro** (no escuro, inverte o fundo) | tag "O próximo passo", h2 "Isso é só o começo…", parágrafo do que o produto cobre, mockup do produto à direita, avatar redondo P&B + nome + prova ("+10 mil pacientes atendidos"), botão sólido retangular `GARANTA O SEU · LINK NA BIO` (tracking .24em), rodapé com aviso "CONTEÚDO EDUCATIVO PARA PROFISSIONAIS DE SAÚDE". |

**Ritmo de fundos**: na versão escura todos #1C1C1A e só o CTA branco. Na versão clara, alterne
`branco` / `off` (#F4F5F3) / `verde-claro` (#EEF3EF) — nunca dois iguais seguidos no meio.

## 5. Regras de copy

- **Uma ideia por slide.** O `h2` é uma afirmação curta (3–8 palavras) que funciona sozinha:
  "O paciente médio não existe.", "Risco não é sentença.", "VUS não é resultado positivo."
- Parágrafo: no máximo ~45 palavras, mecanismo + consequência prática.
- **Analogia em todo slide de item** — é a assinatura do estilo ("A enzima é uma fábrica…",
  "É previsão do tempo, não destino."). Curta, concreta, cotidiana.
- Dado, estudo ou diretriz → **sempre** com `.fonte`. Nada de número sem referência.
- Inclua pelo menos um "o que NÃO fazer" (ex.: MTHFR) — dá autoridade e foge do hype.
- Tom do `marca.md`. Em saúde: **sem promessa de cura, sem "milagre", sem garantia de resultado**,
  sem antes/depois (regras do CFM/publicidade médica). Fala de profissional para profissional.

## 6. Contraste e acabamento

- Acento suave sobre branco não passa contraste em texto pequeno: escureça (ex.: `#8AACB1` → `#4C767C`
  para texto, `#C6D3C8` → `#5F7D66`). No escuro use os tons originais.
- Logo: `filter: invert(1)` no fundo escuro se o arquivo for preto.
- Avatar do CTA: `background` da foto limpa com `background-size`/`position` ajustados pra enquadrar o rosto.
- Ajuste fino de posição (quando o usuário arrasta algo no app) pode ficar como `transform: translate()` inline.
- Nada pode encostar nas linhas da grade nem passar da linha do rodapé — confira o slide mais denso.

## 7. Mostrar, conferir, exportar

```bash
brix content preview "<caminho absoluto>/preview.html"   # mostra/atualiza no app (rode de novo após editar)
brix content export "<pasta da peça>"                    # gera exports/<slug>-01..08.png
brix content list                                         # confirme título e 8 slides antes de dizer que está pronto
```
Abra 2–3 PNGs exportados (o 1, o mais denso e o 8) e confira estouro de texto, contraste e fontes carregadas.
Vários carrosséis de uma vez = um subagente nativo por carrossel, cada um com seu `brix content new`.
