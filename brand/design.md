# Bongarbit · design.md — Calculadora de Engome

Guia para reajustar https://bongarbit-org.github.io/calculadora-engome/ dentro da identidade Bongarbit (Escola de Luteria da Xambá). Implementar no repositório com Claude Code.

**Tese visual:** a tecnologia não vem de fora, já existe na comunidade. Tudo é impresso popular — xilogravura, papel, tinta. Nada de estética de software (sem gradiente, sem sombra suave, sem blur, sem cantos arredondados).

## Como usar este pacote
1. Copiar `design-handoff/` para o repositório (ex.: `/assets/brand/`).
2. Carregar os tokens, nesta ordem:
```html
<link rel="stylesheet" href="assets/brand/tokens/fonts.css">
<link rel="stylesheet" href="assets/brand/tokens/colors.css">
<link rel="stylesheet" href="assets/brand/tokens/typography.css">
<link rel="stylesheet" href="assets/brand/tokens/spacing.css">
<link rel="stylesheet" href="assets/brand/tokens/effects.css">
<link rel="stylesheet" href="assets/brand/tokens/base.css">
```
3. `fonts.css` aponta para `../assets/fonts/` — manter a estrutura de pastas ou ajustar os caminhos.
4. Estilizar sempre com `var(--*)`; não inventar cores ou tamanhos fora dos tokens.
5. **Não alterar a lógica da calculadora** — só apresentação.

## Logos (assets/logo/)
| Arquivo | Uso |
|---|---|
| `lockup-horizontal.png` | Marca completa. Cabeçalho em telas largas. |
| `lockup-papel.png` | Mesma marca sobre fundo papel. |
| `wordmark.png` | Só o nome "bongarbit". Cabeçalho mobile. |
| `wordmark-papel.png` | Wordmark sobre fundo papel. |
| `simbolo.png` | Símbolo isolado. Favicon / ícone (≥32px). |
| `tagline.png` | "Escola de Luteria…" manuscrito. Abaixo do wordmark. |
| `ornamento.png` / `ornamento-papel.png` | Pontos + onda sonora. Divisor assinatura sob o wordmark e entre seções. |

Ilustração de apoio: `assets/ilustracoes/cabaca.png` (pode ilustrar o topo ou o estado vazio).

Regras: não redesenhar, recolorir, distorcer ou aplicar efeitos. O lettering é desenho à mão dos autores **Adelson Boris** e **Philipe Camarão** — nunca substituir por fonte. Respiro mínimo em volta = altura do "o" do wordmark. Sempre com `alt` descritivo (`alt="Bongarbit — Escola de Luteria da Xambá"`).

## Cores
Base: papel `--papel-cartaz #f0d6b8` (fundo da página), tinta `--preto-grafite #161512` (texto, linhas, botões).

| Token | Hex | Uso na calculadora |
|---|---|---|
| `--papel-cartaz` | #f0d6b8 | Fundo da página |
| `--papel` | #ead6bf | Superfície de cards/painéis |
| `--papel-claro` | #f6e9d8 | Campos de input |
| `--preto-grafite` | #161512 | Texto, bordas, botão primário |
| `--terracota-tinta` | #963720 | Títulos, resultado em destaque, links |
| `--terracota-queimada` | #b14826 | Ação de destaque, erro |
| `--ocre-cabaca` | #d4752d | Foco (outline) |
| `--areia-tinta` | #be7f5e | Subtítulos discretos (só em tamanho grande) |
| `--verde-baoba` | #31671f | Sucesso |
| `--azul-caixas-dagua` | #376182 | Informação / dica |
| `--amarelo-ocre` | #d0962d | Aviso |

Paleta sempre quente; se a tela parecer fria, está errada. Verde-limão e laranja EPI só existem no equipamento da mascote — nunca como cor de interface.

## Tipografia (fontes substitutas)
- `--font-hand` Amatic SC 700 — títulos grandes em CAIXA ALTA (`CALCULADORA DE ENGOME`). Só ≥32px.
- `--font-sans` Cabin — corpo, labels, botões. Labels/kickers em caixa alta, 700.
- `--font-condensed` Oswald 600–700 — **números**: medidas, resultados, unidades (cm, mm).
- Papéis prontos: `--type-display`, `--type-headline`, `--type-lede`, `--type-kicker`, `--type-body`, `--type-small`, `--type-numeral`.

## Forma
- Cantos: `0` em tudo. Exceções: selo de data `6px`, tags `pill`, radio/pontos círculo.
- Bordas: `2px solid var(--preto-grafite)` em inputs, botões e cards; `3px` em avisos/diálogos.
- Profundidade: `--shadow-carimbo` (3px 3px 0 grafite) — bloco de tinta deslocado, nunca sombra difusa.
- Moldura de cartaz (opcional, no container principal): régua dupla preta — 7px externa, 4px de papel, 5px interna.
- Espaçamento: escala `--sp-1`…`--sp-9` (4–96px).

## Componentes da calculadora
- **Input numérico:** fundo `--papel-claro`, borda 2px grafite, canto 0, número em Oswald. Unidade à direita em Cabin 700 caixa alta. Foco: `outline: 3px solid var(--ocre-cabaca); outline-offset: 2px`.
- **Select:** mesmo estilo; seta `▼` em grafite.
- **Botão primário (Calcular):** fundo grafite, texto papel, Cabin 700 caixa alta, `--shadow-carimbo`. Hover: `translate(-2px,-2px)` + `--shadow-carimbo-lg`. Press: `translate(3px,3px)` + sombra 0. Transição 120–200ms `--ease-print`, sem bounce.
- **Botão secundário:** fundo transparente, borda 2px grafite, mesmo comportamento.
- **Resultado:** card `--papel` com borda 2px e carimbo; valor em `--type-numeral` (ou maior) em `--terracota-tinta`; rótulo em kicker caixa alta.
- **Tabela de medidas:** linhas 2px grafite no cabeçalho, 1px `--papel-escuro` entre linhas; números alinhados à direita em Oswald.
- **Aviso de segurança (EPI):** borda 3px, tom afetuoso e sereno — "A Xambarina já tá de óculos. E você?" — nunca alarmista.
- **Divisor:** `ornamento.png` centralizado entre o cabeçalho e o conteúdo.

## Layout
Composição centrada e simétrica, como o cartaz: kicker institucional → wordmark → ornamento → título → lede terracota → calculadora → rodapé com créditos.
- Largura máxima ~840px, fluida no mobile (`max-width`, sem larguras fixas).
- Fundo chapado de papel. Sem foto de fundo, sem padrão, sem gradiente.

## Texto
- Português brasileiro, tratamento por *você*, imperativo convidativo: "Informe o diâmetro do tambor", "Calcule o tamanho do couro".
- Títulos e kickers em CAIXA ALTA; corpo em caixa de frase.
- Nomes reais dos instrumentos e lugares: Engome, Agbê, Tambor Falante, Berimbau; Portão do Gelo, Olinda, Recife Antigo.
- Sem emoji. Contatos por extenso: `BONGARBIT.ORG`, `@BONGARBIT`.
- Rodapé: "MINISTÉRIO DA CULTURA E PROGRAMA ROUANET NORDESTE APRESENTAM" (kicker) + créditos de identidade: Adelson Boris e Philipe Camarão.

## Ícones
Não há sistema de ícones da marca. Se precisar (ex.: Instagram), usar Lucide com traço 2.5px em grafite, como substituto provisório. Preferir ilustrações do acervo a ícones.

## Checklist de revisão
- [ ] Fundo `--papel-cartaz`, nenhum branco puro ou cinza frio
- [ ] Nenhum `border-radius` fora das exceções
- [ ] Nenhum `box-shadow` com blur, nenhum gradiente, nenhum `backdrop-filter`
- [ ] Números em Oswald, títulos em Amatic SC caixa alta
- [ ] Foco visível em ocre em todos os campos
- [ ] Contraste de texto ≥ 4.5:1 (areia-tinta só em texto grande)
- [ ] Logos sem distorção, com `alt`
- [ ] Lógica de cálculo intacta
