# 📘 Guia Definitivo do Nivelamento ITEC - UFPA

Bem-vindo à equipe de construção do material didático do **Nivelamento ITEC - UFPA**. Este documento é o mapa do nosso repositório e o manual oficial de como trabalhamos juntos no LaTeX. 

Nossa arquitetura baseia-se em um princípio fundamental: **A separação absoluta entre o conteúdo (texto) e a forma (layout)**. 
Para manter a organização e a escalabilidade, permitindo que dezenas de voluntários atuem simultaneamente sem quebrar o código, dividimos nosso fluxo de trabalho e este manual em dois papéis distintos: **Redatores** e **Artífices**.

---

## ✍️ BLOCO 1: MANUAL DO REDATOR

Seu papel como redator é focar puramente no conteúdo, na lógica didática e na precisão científica. O sistema de compilação cuidará do design e da padronização de forma autônoma.

### 1. Regras de Ouro e Práticas Proibidas
*   ❌ **Foque no texto, não no layout:** É terminantemente proibido forçar quebras ou espaçamentos manuais arbitrários (não utilize `\vspace{}`, `\hspace{}`, `\newline` ou `\\` repetidamente).
*   ❌ **Não crie caixas e cores manualmente:** Não utilize `\begin{tcolorbox}` diretamente para tentar criar blocos bonitos, nem use `\textcolor{}{}`. Nós temos ambientes próprios para isso.
*   ❌ **Sem pacotes locais:** Nunca insira `\usepackage{}` no meio dos arquivos de conteúdo. Toda dependência deve ser solicitada aos Artífices.

### 2. Padrões de Arquivos (Snake Case)
Para evitar sobrescritas, adotamos o **Snake Case** (tudo minúsculo, sem acentos, sem espaços) para nomear arquivos. O formato obrigatório é:
`[prefixo]_[eixo]_[tag_oficial]_[detalhe].[extensão]`

**Prefixos obrigatórios:**
*   `cap_`: Capítulos e seções de texto (ex: `cap_fi_cinematica.tex`)
*   `fig_`: Imagens estáticas PNG/JPG (ex: `fig_pc_funcoes_raiz.png`)
*   `tkz_`: Gráficos gerados em TikZ (ex: `tkz_qi_ligacao.tex`)
*   `tab_`: Tabelas (ex: `tab_pc_trigonometria.tex`)
*   `cod_`: Snippets de código (ex: `cod_pg_repeticao.tex`)

**Atenção às Tags Oficiais (Exemplo do Pré-Cálculo - `pc`):** 
Use as tags oficiais da apostila (`aritmetica`, `algebra`, `trigonometria`, `conjuntos`, `funcoes`). Não invente abreviações ("arit", "trig", etc).

### 3. Ferramentas: Ambientes Didáticos Semânticos
Sempre que precisar destacar uma informação acadêmica, use nossos macros. Eles aplicam as cores e numerações institucionais de forma automática.
**Atenção à sintaxe:** Para que o gabarito funcione, nossos ambientes exigem **dois colchetes sequenciais**: `[Título do Bloco][etiqueta_de_rastreio]`. Se não houver título, deixe o primeiro colchete vazio.

```latex
% Exemplo COMPLETO com título
\begin{exemplo}[Cálculo de Área][exemplo:pc_geometria_area]
    Considere um triângulo retângulo onde...
\end{exemplo}

% Exercício SEM TÍTULO (note o primeiro colchete vazio)
\begin{exercicio}[][ex:pc_algebra_eq_segundo_grau]
    Resolva a equação $x^2 - 5x + 6 = 0$.
\end{exercicio}

% Gerando o Gabarito (apontando para a etiqueta do exercício)
\begin{gabarito}{ex:pc_algebra_eq_segundo_grau}
    As raízes são $x_1 = 2$ e $x_2 = 3$.
\end{gabarito}
```

### 4. Sistema de Referenciamento e Etiquetas (Labels)
Todas as estruturas textuais, imagens e equações devem possuir uma etiqueta com o prefixo correto: `[categoria]:[eixo]_[assunto]_[detalhe]`.

*   **Prefixos comuns:** `sec:` (Seções), `fig:` (Figuras), `tab:` (Tabelas), `eq:` (Equações). Estas são aplicadas usando o clássico `\label{}` dentro do elemento.
*   **Prefixos de Ambientes:** `ex:` (Exercícios), `exemplo:`, `desafio:`. **Exceção importante:** Como visto no tópico anterior, nos ambientes didáticos você **NÃO** usa `\label{}`, você insere a etiqueta diretamente no segundo par de colchetes `[][]` do ambiente.

### 5. Figuras e Tabelas (Padrão ABNT e Fontes)
É **obrigatório** o uso de legendas (`\caption{}`) em todas as figuras e tabelas do material. Além disso, aplicamos o rigor do padrão ABNT para as inserções:

*   **Citação no texto:** Toda figura ou tabela deve ser citada no texto de forma explícita **antes** de aparecer visualmente no documento (ex: *"Como podemos observar na Figura \ref{fig:pc_funcoes_raiz}..."*).
*   **Fonte Obrigatória:** Logo após a legenda da figura ou tabela, você deve referenciar a autoria do conteúdo:
    *   Use o comando `\fonteNivelamento` caso a imagem ou tabela seja de autoria da própria equipe do projeto.
    *   Use o comando `\fonte{Nome do Autor ou Referência}` para materiais extraídos da internet, livros ou provas de vestibulares.

**Exemplo de Aplicação:**
```latex
Como vemos na Figura \ref{fig:pc_funcoes_raiz}, o gráfico intercepta...

\begin{figure}[H]
    \centering
    \includegraphics[width=0.5\textwidth]{fig_pc_funcoes_raiz.png}
    \caption{Comportamento da raiz na função afim}
    \label{fig:pc_funcoes_raiz}
    \fonteNivelamento % ou \fonte{Livro XYZ, p. 45}
\end{figure}
```

---

## 🛠️ BLOCO 2: MANUAL DO ARTÍFICE

Se você atua na manutenção, infraestrutura e revisão técnica do template, este é o seu domínio. Esta seção explica os mecanismos profundos do projeto.

### 1. Arquitetura Modular e Escopo
O código complexo que governa a apostila foi extraído do arquivo raiz e dividido em "motores". Redatores operam estritamente dentro da pasta `/conteudo`. Os artífices mantêm o ambiente de configurações na pasta `/setup`.

```text
/
├── main.tex                         (Arquivo raiz e orquestrador)
├── /conteudo                        (Área restrita de Redatores)
└── /setup                           (Núcleo de Infraestrutura)
    ├── /assets                      (Identidade visual em SVG)
    ├── /pre_textual                 (Diagramação de capas)
    └── *.sty                        (Motores modulares)
```

### 2. Os Mecanismos Internos (Pacotes `.sty`)

Para blindar o documento contra falhas catastróficas, dividimos as responsabilidades do sistema em três pacotes vitais localizados em `/setup`:

#### A. O Alicerce: `nivelamento_base.sty`
O núcleo duro de estabilidade, sem responsabilidades visuais, mas essencial para a compilação:
*   **Codificação e Idioma:** Carrega `inputenc` e `babel`, resolvendo hifenizações complexas em português e suporte a caracteres acentuados.
*   **Geometria Estática:** O pacote `geometry` define margens fixas globais A4, impedindo que falhas humanas em documentos isolados alterem a margem de impressão.
*   **Motores Matemáticos:** Centraliza os poderosos pacotes AMS (`amsmath`, `amssymb`), vitais para as demandas das disciplinas de exatas.
*   *Protocolo de Atualização:* Todo novo pacote geral (como `booktabs` para tabelas) precisa ser inserido aqui, jamais no `main.tex`.

#### B. Identidade Adaptativa: `nivelamento_design.sty`
Este módulo é o gestor de temas dinâmicos. Ao alterar a chave `\setDesign{Eixo}` no `main.tex`, ele injeta visual instantâneo em todo o PDF.
*   **Variáveis de Cor (`xcolor`):** Em vez de escrever "azul" ou "vermelho", o sistema usa variáveis lógicas (`main` e `main-dark`). O redator aplica a classe, o `.sty` decide que cor será impressa baseada no eixo ativo.
*   **Roteamento de SVG Institucional:** Variáveis opacas como `\logoIconeEixo` apontam dinamicamente para os ícones corretos dentro de `/assets`, montando capas institucionais complexas automaticamente.
*   *Protocolo de Atualização:* Para cadastrar um novo eixo didático, copie um bloco condicional inteiro (como o do `PC`), adapte a sigla e atualize as chaves hexadecimais de cor.

#### C. Engenharia Didática: `nivelamento_ambientes.sty`
Onde a magia visual acontece. Traduz códigos tipográficos gigantescos em comandos limpos para os redatores.
*   **Meta-estilos (CSS-like):** O pacote `tcolorbox` é utilizado para criar estilos unificados. Espaçamento (padding), sombra e arredondamento são definidos aqui. Alterar 1 milímetro de borda aqui ajusta todas as apostilas do Nivelamento.
*   **Automação Semântica e Rastreadores:** O comando `\DeclareTColorBox` amarra os meta-estilos, injeta logotipos do pacote `fontawesome` (a lâmpada do exemplo, o troféu do desafio) e cria a numeração automática inteligente que interage com o gabarito.
*   **Redesenho de Títulos:** Modifica as chamadas nativas do LaTeX (`\section`) via pacote `titlesec`, substituindo a fonte sem graça por nossa tipografia corporativa.
*   *Protocolo de Atualização:* Para criar uma nova caixa (ex: "Fique Atento!"), clone o código `\DeclareTColorBox` de uma caixa parecida, troque o ícone, defina uma cor e preserve a herança dos meta-estilos genéricos.
