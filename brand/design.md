# Bongarbit · design.md — Mapa do Agbê

Guia da identidade visual do **Mapa do Agbê** (https://bongarbit-org.github.io/mapa-do-agbe/), editor de carta de miçangas com visualizador 3D, dentro da identidade Bongarbit (Escola de Luteria da Xambá).

**Tese visual:** a tecnologia não vem de fora, já existe na comunidade. Tudo é impresso popular — xilogravura, papel, tinta. Nada de estética de software (sem gradiente, sem sombra suave, sem blur, sem cantos arredondados).

## Estrutura do pacote (`brand/`)
```
brand/
  design.md
  tokens/   fonts · colors · typography · spacing · effects · base (.css)
  assets/
    fonts/        woff2 (Amatic SC, Cabin, Oswald)
    logo/         wordmark, ornamento, lockups, símbolo, tagline
    ilustracoes/  cabaca.png
```
Páginas na raiz carregam os tokens nesta ordem:
```html
<link rel="stylesheet" href="brand/tokens/fonts.css">
<link rel="stylesheet" href="brand/tokens/colors.css">
<link rel="stylesheet" href="brand/tokens/typography.css">
<link rel="stylesheet" href="brand/tokens/spacing.css">
<link rel="stylesheet" href="brand/tokens/effects.css">
<link rel="stylesheet" href="brand/tokens/base.css">
```
- `fonts.css` aponta para `../assets/fonts/` — manter a estrutura de pastas.
- Estilizar sempre com `var(--*)`; não inventar cores ou tamanhos fora dos tokens.
- Mudanças de identidade mexem só na apresentação (CSS e marcação). Não alterar a lógica de cálculo, a carta nem o 3D.
- A pasta `_ds/` é o design system anterior (TheMixMono); as páginas não dependem mais dela.

## Logos (`brand/assets/logo/`)
| Arquivo | Tinta | Uso |
|---|---|---|
| `wordmark.png` | grafite + ponto ocre | Nome "bongarbit" **com** ornamento e tagline "Escola de Luteria da Xambá" já incluídos. É o cabeçalho da página. |
| `ornamento.png` | grafite | Pontos + onda sonora. Divisor entre seções e acima do rodapé. |
| `lockup-horizontal.png` | grafite | Marca completa horizontal, para telas largas fora do app. |
| `simbolo.png` | grafite | Símbolo isolado. Favicon / ícone (≥32px). |
| `tagline.png` | grafite | "Escola de Luteria…" manuscrito, quando usado sem o wordmark. |
| `*-papel.png` (`wordmark-papel`, `ornamento-papel`, `lockup-papel`) | cor de papel | Versões **claras**, para fundos escuros (grafite). Sobre o fundo de papel desta página elas somem — não usar. |

Ilustração de apoio: `assets/ilustracoes/cabaca.png` (topo ou estado vazio).

`wordmark.png`, `ornamento.png` e `cabaca.png` foram reduzidos (1600px / 1600px / 1000px de lado maior) para carregar rápido; os demais PNGs estão em tamanho original (4–6 mil px) — reduzir antes de usar na página.

Regras: não redesenhar, recolorir, distorcer ou aplicar efeitos. O lettering é desenho à mão dos autores **Adelson Boris** e **Philipe Camarão** — nunca substituir por fonte. Respiro mínimo em volta = altura do "o" do wordmark. Sempre com `alt` descritivo (`alt="Bongarbit — Escola de Luteria da Xambá"`); ornamentos decorativos usam `alt=""` ou `background-image`.

## Cores
Base: papel `--papel-cartaz #f0d6b8` (fundo da página, do painel e do palco 3D), tinta `--preto-grafite #161512` (texto, linhas, botão primário).

| Token | Hex | Uso no Mapa do Agbê |
|---|---|---|
| `--papel-cartaz` | #f0d6b8 | Fundo da página, do painel e do palco 3D |
| `--papel` | #ead6bf | Cabeçalho e rodapé da tabela |
| `--papel-claro` | #f6e9d8 | Área do mapa (quadro) e corpo da tabela |
| `--papel-escuro` | #dcc3a3 | Linhas entre linhas da tabela, barra de abas e de cores no celular, trilho de rolagem |
| `--preto-grafite` | #161512 | Texto, bordas, botão primário, aba ativa |
| `--terracota-tinta` | #963720 | Lede, valores (`output`), dados do projeto, sliders e checkboxes |
| `--terracota-queimada` | #b14826 | Estado "pressionado" da barra de rolagem; erro |
| `--ocre-cabaca` | #d4752d | Foco (outline) e seleção de cor na paleta |
| `--areia-tinta` | #be7f5e | Traço do amostra "vazio" (só decorativo) |
| `--verde-baoba` | #31671f | Sucesso |
| `--azul-caixas-dagua` | #376182 | Informação / dica |
| `--amarelo-ocre` | #d0962d | Aviso |

Paleta sempre quente; se a tela parecer fria, está errada. Verde-limão e laranja EPI só existem no equipamento da mascote — nunca como cor de interface.

**Cores de dados não são interface:** as cores das miçangas (paleta do projeto, incluindo cores acrescentadas pelo usuário), o desenho da carta no canvas e os materiais do modelo 3D (cabaça, linhas, trança) representam o objeto real e ficam fora destas regras.

## Tipografia (fontes substitutas)
- `--font-hand` Amatic SC 700 — título da página em CAIXA ALTA (`REDE DO AGBÊ`, 56px). Só ≥32px.
- `--font-sans` Cabin — corpo, labels, botões. Labels/kickers em caixa alta, 700.
- `--font-condensed` Oswald 500–700 — **números**: valores dos sliders, dados do projeto, zoom, tabela.
- Papéis prontos: `--type-display`, `--type-headline`, `--type-lede`, `--type-kicker`, `--type-body`, `--type-small`, `--type-numeral`.

## Forma
- Cantos: `0` em tudo, inclusive inputs de cor, amostras e botões nativos (`border-radius:0` explícito). Exceções: selo de data `6px`, tags `pill`, radio/pontos círculo.
- Bordas: `2px solid var(--preto-grafite)` em botões, quadro, tabela, amostras; `3px` na divisória entre painel e palco e na barra de abas; `3px` em avisos/diálogos.
- Profundidade: `--shadow-carimbo` (3px 3px 0 grafite) — bloco de tinta deslocado, nunca sombra difusa.
- Espaçamento: escala `--sp-1`…`--sp-9` (4–96px).

## Layout
- **Desktop (>900px):** duas colunas. Painel à esquerda (600px, papel-cartaz, rolável) e palco 3D à direita (flexível). Divisória de 3px grafite.
- **Painel, de cima para baixo:** wordmark centralizado → título → lede terracota → Trançado (sliders e dados) → ornamento → Mapa de miçangas (texto, ações) → ornamento → Cores → ornamento → Miçangas por fiada → mapa editável (zoom, quadro, paleta) → ornamento → rodapé com créditos.
- **Celular (≤900px):** barra de abas fixa no topo (Ajustes · Mapa · Modelo 3D); aba ativa em grafite com texto papel. Na aba Mapa a paleta vira coluna fixa à direita (66px, `--papel-escuro`) e o botão "Ver tudo" fica grafite na base dela. O rodapé aparece só na aba Ajustes.
- Fundo chapado de papel. Sem foto de fundo, sem padrão, sem gradiente.

## Componentes
- **Título:** Amatic SC caixa alta, centralizado, sob o wordmark. **Lede:** Cabin 700 18px em `--terracota-tinta`, centralizado, máx. ~46ch. Textos de apoio (`.ajuda`): Cabin 500 14px em `--fg-2`.
- **Kicker / eyebrow:** Cabin 700 14px caixa alta, `--tracking-kicker`.
- **Slider:** `accent-color: var(--terracota-tinta)`. Rótulo em kicker; valor à direita em Oswald 600 18px terracota-tinta.
- **Checkbox:** `accent-color: var(--terracota-tinta)`, 18px, rótulo em kicker.
- **Dados do projeto:** uma linha em Oswald 500 16px, terracota-tinta.
- **Botão secundário (`.acao`):** fundo transparente, borda 2px grafite, Cabin 700 caixa alta, `--shadow-carimbo`. Hover: `translate(-2px,-2px)` + `--shadow-carimbo-lg`. Press: `translate(3px,3px)` + sombra 0. Transição `--dur-fast` `--ease-print`, sem bounce.
- **Botão primário:** mesmo botão com fundo grafite e texto papel-cartaz. Um por grupo; hoje é "Baixar mapa".
- **Foco:** `outline: 3px solid var(--focus); outline-offset: 2px` em botões, inputs, amostras e `summary`.
- **Zoom:** botões quadrados 40px com carimbo; valor em Oswald 600 18px entre eles.
- **Quadro do mapa:** fundo `--papel-claro`, borda 2px e carimbo; barras de rolagem grafite sobre trilho `--papel-escuro` (14px); `:active` do polegar em `--terracota-queimada`.
- **Amostras de cor:** 52×44px, borda 2px grafite, nome em Cabin 700 9px caixa alta (papel-cartaz sobre cores escuras, grafite sobre claras). Selecionada: outline ocre. "Vazio": fundo `--papel-escuro` com traços diagonais em `--areia-tinta` (SVG embutido, nunca gradiente).
- **Tabela por fiada:** cabeçalho em Cabin 700 12px caixa alta sobre `--papel`, linha de 2px grafite embaixo; linhas de 1px `--papel-escuro`; números em Oswald, alinhados à direita (primeira coluna à esquerda); rodapé com linha de 2px em cima. Dentro de caixa rolável com borda 2px e carimbo.
- **Stepper (− n +):** botões 28px, borda 2px grafite, canto 0, sem sombra.
- **Divisor (`.filete`):** `ornamento.png` centralizado, 24px de altura, como `background` contido — substitui qualquer régua simples.
- **Aviso de segurança (EPI):** borda 3px, tom afetuoso e sereno — "A Xambarina já tá de óculos. E você?" — nunca alarmista.
- **Rodapé:** kickers centralizados — "MINISTÉRIO DA CULTURA E PROGRAMA ROUANET NORDESTE APRESENTAM", "BONGARBIT.ORG · @BONGARBIT" — e linha de créditos "Identidade visual: Adelson Boris e Philipe Camarão".

## Texto
- Português brasileiro, tratamento por *você*, imperativo convidativo: "Toque ou arraste para pintar", "Ajuste quantas miçangas entram em cada vão".
- Títulos e kickers em CAIXA ALTA; corpo em caixa de frase.
- Nomes reais dos instrumentos e lugares: Agbê, Engome, Tambor Falante, Berimbau; Portão do Gelo, Olinda, Recife Antigo.
- Termos do ofício como estão na página: argola, trança, fiada, nó, miçanga, cabaça, carta/mapa de miçangas.
- Sem emoji. Contatos por extenso: `BONGARBIT.ORG`, `@BONGARBIT`.

## Ícones
Não há sistema de ícones da marca. Se precisar (ex.: Instagram), usar Lucide com traço 2.5px em grafite, como substituto provisório. Preferir ilustrações do acervo a ícones.

## Checklist de revisão
- [ ] Fundo `--papel-cartaz` (página, painel e palco 3D), nenhum branco puro ou cinza frio
- [ ] Nenhum `border-radius` fora das exceções; controles nativos com `border-radius:0`
- [ ] Nenhum `box-shadow` com blur, nenhum gradiente (nem `repeating-linear-gradient`), nenhum `backdrop-filter`
- [ ] Números em Oswald, títulos em Amatic SC caixa alta
- [ ] Foco visível em ocre em todos os controles
- [ ] Contraste de texto ≥ 4.5:1 (areia-tinta só decorativa)
- [ ] Logos sem distorção, com `alt`; versões `-papel` só em fundo escuro
- [ ] Layout testado em desktop e no celular (abas, paleta lateral, "Ver tudo")
- [ ] Lógica de cálculo, carta e 3D intactos
