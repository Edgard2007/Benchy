# BenchMetrics

Site acadêmico de 5 páginas em HTML puro, sem frameworks, sem folhas de estilo externas e sem
Tailwind. Toda a formatação visual é feita com o atributo `style=""` diretamente nas tags
(CSS Inline), conforme exigido pela atividade.

## Estrutura de arquivos

```
/
├── home.html          → Página inicial (hero, recursos, tabela de testes suportados)
├── catalogo.html       → Galeria de imagens + tabela de cenários de teste + busca
├── dashboard.html      → Tabelas de diagnóstico (CPU/GPU) + formulário "Registrar Novo Teste"
├── termos.html          → Termos de Uso
├── privacidade.html    → Política de Privacidade
└── README.md            → Este arquivo
```

Não há mais pasta `css/` nem arquivos `.css`: cada elemento carrega seu próprio `style=""`.
O projeto não usa JavaScript: a seleção de cenários em `catalogo.html` usa o elemento
nativo `<details>`/`<summary>`: cada capa é um botão que abre os detalhes do jogo, e o atributo
`name="cenario"` garante que só um fique aberto por vez. Para incluir um jogo, copie um bloco
`<details>` dentro da `<div>` em grade e troque imagem, título e dados.

## Onde alterar cada coisa

- **Cores**: procure pelos códigos hexadecimais dentro dos atributos `style`. A paleta usada em
  todo o site é:
  - `#FCEE0A` — amarelo (cor primária / destaque)
  - `#FF003C` — vermelho (alerta / acento)
  - `#00F0FF` — ciano (dados / métricas)
  - `#100e0b` / `#0b0a08` — fundo escuro
  - `#121212` — painéis e cabeçalho/rodapé
  - `#e5e2e1` — texto principal / `#ccc7ab` — texto secundário
- **Fundo "Aura" (grade neon)**: é o mesmo bloco de 3 `<div>` (linhas de grade + dois brilhos
  radiais em `mix-blend-mode: screen`) repetido no topo do `<body>` de cada página, logo após a
  tag `<body>`. Para ajustar a posição ou intensidade dos brilhos, edite os valores de
  `radial-gradient(circle at X% Y%, ...)` e `filter: blur(...)`.
- **Menu de navegação**: repetido em cada página dentro da tag `<header>`. O link da página atual
  tem `color:#FCEE0A` e `border-bottom:2px solid #FCEE0A`.
- **Tabelas**: usam `<table>`/`<thead>`/`<tbody>`/`<tr>`/`<th>`/`<td>` padrão; a cor de fundo
  listrada usa `background-color:rgba(255,255,255,0.02)` nas linhas alternadas.
- **Formulário** (`dashboard.html`): campos `name="..."` correspondem aos dados que seriam
  enviados caso o formulário fosse conectado a um backend real. Atualmente `action="#"`, ou seja,
  não envia dados a lugar nenhum.

## Responsividade

Como o projeto não usa `<style>` nem media queries (proibidas pela regra de CSS 100% inline),
a responsividade é obtida apenas com técnicas que funcionam dentro do atributo `style`:
`display:flex` com `flex-wrap:wrap`, `display:grid` com `repeat(auto-fit, minmax(...))` e a
função `clamp()` para tamanhos de fonte e espaçamentos fluidos.

## Privacidade e Termos

Os textos completos estão em `termos.html` e `privacidade.html`. Como o site é estático e o
formulário não envia dados a nenhum servidor, não há coleta real de dados pessoais — os
documentos deixam isso explícito e descrevem os princípios que deveriam ser seguidos (LGPD,
Privacy by Design) caso o formulário seja conectado a um backend no futuro.

Home com 5 fotos da equipe; catálogo com grade de cenários selecionáveis. Fotos em assets/.
