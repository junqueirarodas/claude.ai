---
name: powerbi-padrao-jr
description: Padrão visual Junqueira Rodas para dashboards Power BI (paleta, tema, layout, formatação). Use sempre que for criar, editar, revisar ou dar manutenção em qualquer relatório/dashboard Power BI, projeto PBIP/PBIR, visual.json, tema JSON ou medidas DAX de formatação, mesmo que o usuário não peça "padronizar".
---

# Padrão de dashboards Power BI – Junqueira Rodas

Todo dashboard da Junqueira Rodas deve parecer parte da mesma família: mesma paleta, mesmo esqueleto de página, mesmos componentes. Quem abre um relatório novo deve reconhecer onde ficam os filtros, os KPIs e os detalhes sem precisar aprender de novo. Aplique este padrão tanto ao criar quanto em qualquer manutenção. Ao mexer num visual antigo, aproveite para colocá-lo no padrão e diga ao usuário o que mudou.

Os relatórios são salvos como **projeto PBIP** (pastas com arquivos JSON). O trabalho consiste em editar esses arquivos, não o .pbix.

## 1. Paleta

| Papel | Cor | Uso |
|---|---|---|
| Preto | `#3D3C3B` | textos, barra de título dos visuais, botão selecionado, linha de referência (estimado/grupo) |
| Amarelo escuro | `#FCBE05` | fundo dos cards KPI principais, série principal (realizado) em barras e colunas |
| Amarelo claro | `#FBCD2C` | faixa secundária dos cards KPI, cabeçalho de tabelas, segunda série |
| Verde | `#25912F` | variação positiva (↑), rendimento, linhas e áreas de evolução |
| Vermelho (só alerta) | `#C62828` | variação negativa (↓) e alertas. Nunca como cor de série |

Neutros permitidos (fundo, bordas, grades): `#FFFFFF`, `#F2F2F2`, `#D9D9D9`, `#BFBFBF`, `#7F7F7F`.

Nenhuma outra cor deve aparecer, nem mesmo o laranja ou o verde-claro de dashboards antigos. Em gráficos de área, use o verde com transparência (60–80%) em vez de criar um verde-claro. Com mais de 4 categorias, não crie um arco-íris: use uma cor só (`#FCBE05`) e destaque em `#3D3C3B` o item que importa.

Contraste: sobre amarelo, o texto é sempre preto `#3D3C3B`, porque branco sobre amarelo fica ilegível. Texto branco só sobre preto ou verde.

## 2. Esqueleto da página (canvas 1280 × 720, 16:9)

Margem externa de ~16 px e espaçamento de ~8 px entre visuais. De cima para baixo:

1. **Cabeçalho (y 0–90):** logo Junqueira Rodas à esquerda; segmentações em lista suspensa (ex.: Unidades, Talhão Finalizado, Safra, Filtro de Mês) com rótulo em negrito acima; à direita, o bloco "Botões de navegação" com ícones pretos em linha, que levam às outras páginas.
2. **Faixa de KPIs (y ~95–215):**
   - *KPIs principais* (3 a 5 cards largos): parte superior `#FCBE05` com o título (Segoe UI 12) e o valor grande (Segoe UI Bold 28–32), ambos em preto. Parte inferior `#FBCD2C` com os valores secundários no formato `38,5% | 860,19 K` e uma legenda curta (ex.: "colhidas", "talhões encerrados"). Variações usam a seta e a cor da seção 4.
   - *KPIs secundários* (cards menores à direita): aba de título preta com texto branco, corpo branco, valor em Segoe UI 20–24 cinza-escuro e unidade embaixo (ex.: "Cxs / Ton.").
   - *Mini-cards de alerta* (ex.: Carga Recusada): título preto pequeno com ícone ⓘ, valor centralizado.
3. **Linha de análise (2–3 visuais lado a lado):** comparações "realizado x estimado" por dimensão (unidade, variedade etc.).
4. **Linha de detalhe:** séries temporais (semanal, safra) e tabelas operacionais.
5. **Rodapé:** botões de período (`1S`, `1Q`, `1M`, `1SM`, `1SF`). O selecionado tem fundo `#3D3C3B` e texto branco; os demais, fundo branco, borda `#D9D9D9` e texto preto. À direita, "Última atualização" + `dd/mm/aaaa hh:mm:ss` em negrito.

Nem todo dashboard terá todos os blocos, mas a ordem (filtros → KPIs → análise → detalhe → rodapé) e a aparência de cada bloco não mudam.

## 3. Componentes

**Contêiner de visual (vale para todo gráfico ou tabela):** fundo branco, borda `#D9D9D9` com raio 8, sem sombra. Barra de título com fundo `#3D3C3B`, texto branco, Segoe UI Semibold 12, alinhada à esquerda. O título segue o padrão `Métrica por dimensão x estimado (unidade)`, ex.: "Produtividade por unidade x estimado (Caixas por hectare)". Quando o cálculo não for óbvio, coloque um ícone ⓘ com tooltip explicando.

**Colunas/barras realizado x estimado:** coluna em `#FCBE05`. Rótulo de dados (valor abreviado) em cima da coluna e, acima dele, a variação em relação ao estimado (`↑ +6%` verde / `↓ -38%` vermelho). A média do grupo ou a meta é uma linha tracejada `#3D3C3B`, com legenda "Grupo". Ordene as colunas pelo valor. Eixo Y oculto, sem linhas de grade.

**Rendimento / séries semanais:** colunas em `#25912F`, com o rótulo de valor dentro de uma etiqueta clara no topo da coluna.

**Linha/área de evolução:** linha `#25912F` com marcadores e área verde a 70% de transparência. Rótulos nos pontos e eixo X com datas curtas ("09 de set").

**Barras horizontais (ex.: entrega semanal):** barras `#FCBE05`, rótulo no fim da barra e ordem pela categoria (semana).

**Tabelas:** cabeçalho `#FBCD2C` com texto preto em Semibold, linhas alternando `#FFFFFF`/`#F2F2F2`, texto 10 pt e datas em `dd/mm/aaaa`. Ordene pela coluna que indica problema (ex.: "Dias sem saída" em ordem decrescente).

**Segmentações:** lista suspensa, cabeçalho preto Semibold 11, sem borda de contêiner.

## 4. Números e textos (pt-BR)

- Separador decimal é vírgula: `321,1`, `1,50%`.
- Abreviações: `K` para milhares (`860,19 K`) e `Mi` para milhões (`2,24 Mi`), com 2 casas decimais nos cards.
- Percentuais com 1 casa. Variação sempre com sinal e seta: `↑ +4,8%` em `#25912F`, `↓ -32,5%` em `#C62828`.
- Datas: `dd/mm/aaaa`. Nos eixos, `dd de mmm`.
- Textos em português, com rótulos curtos e sem abreviações obscuras.

## 5. Como trabalhar num projeto PBIP

Estrutura (formato PBIR):
```
Projeto.pbip
Projeto.Report/
  definition/report.json            ← themeCollection + resourcePackages
  definition/pages/<pagina>/page.json
  definition/pages/<pagina>/visuals/<visual>/visual.json
  StaticResources/RegisteredResources/   ← tema personalizado, imagens (logo)
Projeto.SemanticModel/              ← modelo (TMDL): medidas DAX
```
Se existir só `Projeto.Report/report.json` (sem `definition/`), o relatório está em **PBIR-Legacy**, em que tudo fica em strings JSON aninhadas. Não edite esse arquivo à mão. Peça ao usuário para ativar em Power BI Desktop *Opções > Recursos em versão prévia > Armazenar relatórios usando o formato PBIR* e salvar de novo. Se não der, oriente a importação do tema por *Exibir > Temas > Procurar temas*.

**Antes de editar:** o Power BI Desktop precisa estar com o projeto **fechado**, senão ele sobrescreve as alterações ao salvar. Se a pasta for um repositório git, confira `git status` para saber o que já estava alterado.

**Fluxo padrão (criar ou manter):**
1. Grave o tema da seção 6 como `JunqueiraRodas.json` e o script da seção 7 como `pbip_jr.py` (numa pasta temporária, não dentro do projeto).
2. `python pbip_jr.py instalar-tema <Projeto.Report> JunqueiraRodas.json`. O script copia o tema, registra-o no `report.json` e faz backup em `report.json.bak`. Pode ser executado de novo sem problema.
3. `python pbip_jr.py auditar <Projeto.Report>`. Ele lista, por visual, cores fora da paleta e fontes que não são Segoe UI.
4. Corrija cada visual apontado no `visual.json`. Na maioria das vezes basta **remover** a formatação local (a propriedade em `visual.objects` ou `visual.visualContainerObjects`) para o visual herdar o tema. Só grave uma cor explícita quando o papel dela for diferente do padrão do tema (ex.: segunda série em `#FBCD2C`).
5. Ajuste posição/tamanho (`position`: x, y, width, height) conforme o esqueleto da seção 2 e revise os títulos.
6. Rode a auditoria de novo até sair "Nenhum desvio". Depois peça ao usuário para abrir no Power BI Desktop e conferir visualmente, já que a auditoria não enxerga layout.

Onde rodar: os arquivos ficam no computador do usuário. Quando houver shell no computador dele, rode lá (é preciso Python 3). Se não houver, copie a pasta `.Report` para o ambiente de trabalho, edite, audite e devolva os arquivos alterados.

**Sintaxe de valores no visual.json:** tudo passa por `{"expr": {"Literal": {"Value": ...}}}`. Texto e cor ficam entre aspas simples (`"'#FCBE05'"`), booleano sem aspas (`"true"`) e número com sufixo (`"12D"`). Cor de preenchimento:
```json
"fill": {"solid": {"color": {"expr": {"Literal": {"Value": "'#FCBE05'"}}}}}
```
Barra de título padrão (normalmente vem do tema e não precisa ser gravada):
```json
"visualContainerObjects": {"title": [{"properties": {
  "show": {"expr": {"Literal": {"Value": "true"}}},
  "text": {"expr": {"Literal": {"Value": "'Produção por unidade x estimado (Volume de caixas)'"}}},
  "fontColor": {"solid": {"color": {"expr": {"Literal": {"Value": "'#FFFFFF'"}}}}},
  "background": {"solid": {"color": {"expr": {"Literal": {"Value": "'#3D3C3B'"}}}}}
}}]}
```
Cor dinâmica vinda de medida (setas e variações):
```json
"fontColor": {"solid": {"color": {"expr": {"Measure": {
  "Expression": {"SourceRef": {"Entity": "_Medidas"}}, "Property": "Cor Variação"}}}}}
```
Mantenha `name`, `$schema` e `query` intactos. Ao criar um visual novo, copie um `visual.json` existente do mesmo tipo como base, gere um `name` novo (hex de 20 caracteres) com pasta de mesmo nome e ajuste `position.z`/`tabOrder`.

**Medidas DAX de apoio** (crie na tabela de medidas do modelo, via TMDL ou pela ferramenta de modelagem do Power BI se estiver disponível):
```dax
Cor Variação = IF ( [Var % vs Estimado] >= 0, "#25912F", "#C62828" )

Rótulo Variação =
VAR v = [Var % vs Estimado]
RETURN IF ( ISBLANK ( v ), BLANK (), IF ( v >= 0, "↑ ", "↓ " ) & FORMAT ( v, "+0.0%;-0.0%" ) )

Última Atualização = "Última atualização " & FORMAT ( MAX ( 'Atualizacao'[DataHora] ), "dd/mm/yyyy hh:nn:ss" )
```
Troque `[Var % vs Estimado]` e `'Atualizacao'[DataHora]` pelos nomes reais do modelo e confira no modelo antes de usar. Para `K`/`Mi`, use cadeia de formato dinâmica ou as unidades de exibição do visual (Milhares/Milhões), não texto fixo.

## 6. Tema oficial (JunqueiraRodas.json)

```json
{
  "name": "JunqueiraRodas",
  "dataColors": ["#FCBE05", "#25912F", "#3D3C3B", "#FBCD2C", "#7F7F7F", "#BFBFBF"],
  "foreground": "#3D3C3B",
  "foregroundNeutralSecondary": "#7F7F7F",
  "foregroundNeutralTertiary": "#BFBFBF",
  "background": "#FFFFFF",
  "backgroundLight": "#F2F2F2",
  "backgroundNeutral": "#D9D9D9",
  "tableAccent": "#FCBE05",
  "good": "#25912F",
  "neutral": "#FCBE05",
  "bad": "#C62828",
  "maximum": "#25912F",
  "center": "#FCBE05",
  "minimum": "#C62828",
  "textClasses": {
    "callout": { "fontSize": 28, "fontFace": "Segoe UI Bold", "color": "#3D3C3B" },
    "title": { "fontSize": 12, "fontFace": "Segoe UI Semibold", "color": "#FFFFFF" },
    "header": { "fontSize": 11, "fontFace": "Segoe UI Semibold", "color": "#3D3C3B" },
    "label": { "fontSize": 9, "fontFace": "Segoe UI", "color": "#3D3C3B" }
  },
  "visualStyles": {
    "*": {
      "*": {
        "title": [{
          "show": true,
          "fontColor": { "solid": { "color": "#FFFFFF" } },
          "background": { "solid": { "color": "#3D3C3B" } },
          "alignment": "left",
          "fontSize": 12,
          "fontFamily": "Segoe UI Semibold",
          "bold": true
        }],
        "background": [{ "show": true, "color": { "solid": { "color": "#FFFFFF" } }, "transparency": 0 }],
        "border": [{ "show": true, "color": { "solid": { "color": "#D9D9D9" } }, "radius": 8 }],
        "dropShadow": [{ "show": false }],
        "labels": [{ "color": { "solid": { "color": "#3D3C3B" } }, "fontSize": 9 }],
        "categoryAxis": [{ "labelColor": { "solid": { "color": "#3D3C3B" } }, "fontSize": 9, "gridlineShow": false }],
        "valueAxis": [{ "show": false, "gridlineShow": false }],
        "legend": [{ "labelColor": { "solid": { "color": "#3D3C3B" } }, "fontSize": 9, "position": "TopLeft" }]
      }
    },
    "page": {
      "*": {
        "background": [{ "color": { "solid": { "color": "#FFFFFF" } }, "transparency": 0 }],
        "outspace": [{ "color": { "solid": { "color": "#FFFFFF" } } }]
      }
    },
    "card": {
      "*": {
        "labels": [{ "color": { "solid": { "color": "#3D3C3B" } }, "fontSize": 28, "fontFamily": "Segoe UI Bold" }],
        "categoryLabels": [{ "color": { "solid": { "color": "#3D3C3B" } }, "fontSize": 10 }]
      }
    },
    "tableEx": {
      "*": {
        "columnHeaders": [{ "fontColor": { "solid": { "color": "#3D3C3B" } }, "backColor": { "solid": { "color": "#FBCD2C" } }, "fontFamily": "Segoe UI Semibold", "fontSize": 10 }],
        "values": [{
          "fontColorPrimary": { "solid": { "color": "#3D3C3B" } },
          "backColorPrimary": { "solid": { "color": "#FFFFFF" } },
          "fontColorSecondary": { "solid": { "color": "#3D3C3B" } },
          "backColorSecondary": { "solid": { "color": "#F2F2F2" } },
          "fontSize": 10
        }],
        "total": [{ "fontColor": { "solid": { "color": "#3D3C3B" } }, "backColor": { "solid": { "color": "#D9D9D9" } } }]
      }
    },
    "pivotTable": {
      "*": {
        "columnHeaders": [{ "fontColor": { "solid": { "color": "#3D3C3B" } }, "backColor": { "solid": { "color": "#FBCD2C" } } }],
        "rowHeaders": [{ "fontColor": { "solid": { "color": "#3D3C3B" } } }]
      }
    },
    "slicer": {
      "*": {
        "title": [{ "show": false }],
        "border": [{ "show": false }],
        "header": [{ "show": true, "fontColor": { "solid": { "color": "#3D3C3B" } }, "fontFamily": "Segoe UI Semibold", "textSize": 11 }],
        "items": [{ "fontColor": { "solid": { "color": "#3D3C3B" } }, "background": { "solid": { "color": "#FFFFFF" } }, "outlineColor": { "solid": { "color": "#BFBFBF" } } }]
      }
    },
    "actionButton": {
      "*": {
        "title": [{ "show": false }],
        "border": [{ "show": true, "color": { "solid": { "color": "#D9D9D9" } }, "radius": 6 }]
      }
    },
    "image": { "*": { "title": [{ "show": false }], "border": [{ "show": false }] } },
    "textbox": { "*": { "title": [{ "show": false }], "border": [{ "show": false }] } },
    "shape": { "*": { "title": [{ "show": false }], "border": [{ "show": false }] } }
  }
}
```

## 7. Script de apoio (pbip_jr.py)

```python
"""Padrão Junqueira Rodas para projetos PBIP.
Uso:
  python pbip_jr.py instalar-tema <pasta .Report> <JunqueiraRodas.json>
  python pbip_jr.py auditar <pasta .Report>
"""
import json, re, shutil, sys
from pathlib import Path

PERMITIDAS = {  # paleta + vermelho de alerta + neutros
    "#3D3C3B", "#FCBE05", "#FBCD2C", "#25912F", "#C62828",
    "#FFFFFF", "#F2F2F2", "#D9D9D9", "#BFBFBF", "#7F7F7F", "#000000",
}
HEX = re.compile(r"#[0-9A-Fa-f]{6}\b")
NOME_TEMA = "JunqueiraRodas.json"


def ler(p):
    return json.loads(Path(p).read_text(encoding="utf-8-sig"))


def gravar(p, dados):
    Path(p).write_text(json.dumps(dados, indent=2, ensure_ascii=False) + "\n", encoding="utf-8")


def instalar_tema(report_dir, tema):
    rd = Path(report_dir)
    rep = rd / "definition" / "report.json"
    if not rep.exists():
        sys.exit("Formato PBIR não encontrado (definition/report.json). Relatório está em PBIR-Legacy: "
                 "importe o tema no Power BI Desktop (Exibir > Temas > Procurar temas) ou converta para PBIR.")
    ler(tema)  # valida JSON do tema
    destino = rd / "StaticResources" / "RegisteredResources"
    destino.mkdir(parents=True, exist_ok=True)
    shutil.copyfile(tema, destino / NOME_TEMA)
    shutil.copyfile(rep, rep.with_suffix(".json.bak"))
    r = ler(rep)
    pacotes = r.setdefault("resourcePackages", [])
    reg = next((p for p in pacotes if p.get("type") == "RegisteredResources"), None)
    if reg is None:
        reg = {"name": "RegisteredResources", "type": "RegisteredResources", "items": []}
        pacotes.append(reg)
    reg["items"] = [i for i in reg.get("items", []) if i.get("type") != "CustomTheme"]
    reg["items"].append({"name": NOME_TEMA, "path": NOME_TEMA, "type": "CustomTheme"})
    tc = r.setdefault("themeCollection", {})
    versao = (tc.get("customTheme") or tc.get("baseTheme") or {}).get("reportVersionAtImport")
    novo = {"name": NOME_TEMA, "type": "RegisteredResources"}
    if versao is not None:
        novo["reportVersionAtImport"] = versao
    tc["customTheme"] = novo
    gravar(rep, r)
    print(f"Tema instalado em {destino / NOME_TEMA}; report.json atualizado (backup: report.json.bak).")


def titulo_visual(v):
    try:
        t = v["visual"]["visualContainerObjects"]["title"][0]["properties"]["text"]
        return t["expr"]["Literal"]["Value"].strip("'")
    except (KeyError, IndexError, TypeError):
        return ""


def auditar(report_dir):
    rd = Path(report_dir)
    problemas = 0
    rep = rd / "definition" / "report.json"
    if rep.exists():
        ct = (ler(rep).get("themeCollection") or {}).get("customTheme") or {}
        if "JunqueiraRodas" not in ct.get("name", ""):
            print(f"[TEMA] Tema personalizado ativo: {ct.get('name') or 'nenhum'} (esperado {NOME_TEMA})")
            problemas += 1
    elif (rd / "report.json").exists():
        print("[AVISO] Relatório em PBIR-Legacy (report.json único); auditoria só de cores.")
    tema = rd / "StaticResources" / "RegisteredResources" / NOME_TEMA
    arquivos = [tema] if tema.exists() else []
    arquivos += sorted(p for p in rd.rglob("*.json") if "StaticResources" not in p.parts and not p.name.endswith(".bak"))
    for arq in arquivos:
        texto = arq.read_text(encoding="utf-8-sig")
        fora = sorted({c.upper() for c in HEX.findall(texto)} - PERMITIDAS)
        fontes = sorted(set(re.findall(r"fontFamily[^']*'([^']+)'", texto)))
        fontes_ruins = [f for f in fontes if "segoe" not in f.lower()]
        if not (fora or fontes_ruins):
            continue
        rotulo = arq.relative_to(rd)
        if arq.name == "visual.json":
            v = ler(arq)
            rotulo = f"{arq.parent.parent.parent.name}/{v.get('name')} ({v.get('visual', {}).get('visualType')}) \"{titulo_visual(v)}\""
        if fora:
            print(f"[COR] {rotulo}: {', '.join(fora)}")
            problemas += 1
        if fontes_ruins:
            print(f"[FONTE] {rotulo}: {', '.join(fontes_ruins)}")
            problemas += 1
    print(f"\n{problemas} problema(s) encontrado(s)." if problemas else "Nenhum desvio do padrão encontrado.")
    return problemas


if __name__ == "__main__":
    if len(sys.argv) >= 4 and sys.argv[1] == "instalar-tema":
        instalar_tema(sys.argv[2], sys.argv[3])
    elif len(sys.argv) >= 3 and sys.argv[1] == "auditar":
        auditar(sys.argv[2])
    else:
        sys.exit(__doc__)
```

## 8. Ao terminar

Resuma para o usuário: o que foi padronizado (tema, visuais corrigidos, layout), o que ainda depende dele (conferir no Desktop, logo, ícones de navegação) e qualquer desvio que tenha sido mantido de propósito, com o motivo.
