# Skills do Thiagão

Skills para o Claude (Claude Code, Claude.ai e Claude Desktop).

| Skill | O que faz |
|---|---|
| [`carrossel-editorial-estatico`](skills/carrossel-editorial-estatico/SKILL.md) | Carrossel de Instagram de 8 slides (1080×1350, PNG) em estilo editorial científico: grade de linhas finas, número vazado, analogia por slide, fonte citada, CTA com o produto. |
| [`carrossel-editorial-animado`](skills/carrossel-editorial-animado/SKILL.md) | A versão com movimento (HTML/CSS/SVG): uma cena ilustrada por slide que demonstra a analogia, entradas de título variadas, exporta PNG no estado final. |

As skills puxam cores e tom de voz do seu projeto (`design-systems/*/dna.json`, `marca.md`, `product.md`, `publico.md`) — o estilo é o mesmo, a marca é a sua.

## Instalar

### Claude Code
```bash
git clone https://github.com/thiagomendesmed/skillsthiagao.git
mkdir -p ~/.claude/skills
cp -R skillsthiagao/skills/* ~/.claude/skills/
```
Abra uma sessão nova e peça: *"faz um carrossel estático sobre …"* ou *"carrossel animado sobre …"*.
Para atualizar depois: `cd skillsthiagao && git pull` e copie de novo.

### Claude.ai / Claude Desktop
Compacte a pasta da skill (ex.: `skills/carrossel-editorial-estatico` → `.zip`) e envie em
**Configurações → Capacidades → Skills → Enviar skill**.

## Antes de usar
- Tenha na pasta do projeto: `marca.md`, `product.md` e em `assets/` o logo, sua foto recortada (PNG sem fundo), uma foto limpa (avatar) e a capa do produto.
- Os comandos `brix content …` são do app **BRIX**. Sem ele, gere o `preview.html` e exporte cada slide pelo Chrome abrindo `preview.html#export=N` em 1080×1350.
- Os exemplos em `template/` e `reference/` são do ebook *O Despertar do Código* — servem de referência visual; troque pelo seu conteúdo.
