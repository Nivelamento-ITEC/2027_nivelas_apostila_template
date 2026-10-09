# Manual de Redação e Padronização LaTeX

**Oficina de Nivelamento ITEC - UFPA**

Este documento estabelece as diretrizes de formatação, nomenclatura e estruturação das apostilas do Nivelamento. O objetivo desta arquitetura é garantir que nosso material tenha qualidade profissional, seja escalável e permita que dezenas de voluntários trabalhem simultaneamente sem gerar conflitos de compilação ou quebras de layout.

O cumprimento destas regras é obrigatório para evitar conflitos de compilação e garantir a identidade visual do projeto.

---

# PARTE 1: MANUAL DO REDATOR

## 1. Regras de Ouro e Práticas Proibidas

A premissa desta arquitetura é a **separação entre conteúdo e forma**. O redator foca no texto e na lógica didática; o sistema cuida do layout.

*   ❌ **Proibido usar espaçamentos manuais arbitrários:** Não utilize `\vspace{}`, `\hspace{}`, `\newline` ou `\\` repetidos para forçar quebras de página ou alinhar texto.
*   ❌ **Proibido formatar caixas e cores manualmente:** Não utilize `\begin{tcolorbox}` diretamente, nem modifique a cor do texto com `\textcolor{red}{}` para criar avisos.
*   ❌ **Proibido usar pacotes de layout locais:** Não insira `\usepackage{}` no meio dos arquivos de conteúdo. Toda dependência deve ser solicitada à coordenação para inclusão no `/setup`.

---

## 2. Nomenclatura e Vocabulário de Arquivos

Para evitar sobrescritas quando múltiplos voluntários unem seus arquivos no documento principal, adote o padrão corporativo **Snake Case** (tudo minúsculo, sem espaços, sem acentos ou caracteres especiais). 

**Padrão:** `[prefixo]_[eixo]_[assunto]_[descrição].[extensão]`

| Prefixo | Descrição | Exemplo Correto | Exemplo Incorreto (Proibido) |
| :--- | :--- | :--- | :--- |
| `cap_` | Capítulos e seções (texto LaTeX) | `cap_fi_cinematica.tex` | `Cinematica Final.tex` |
| `fig_` | Imagens rasterizadas (PNG, JPG, SVG) | `fig_pc_funcoes_parabola_concavidade.png` | `grafico 1.png` |
| `tkz_` | Gráficos e vetores gerados em TikZ | `tkz_qi_ligacoes_covalente.tex` | `desenho_novo.tikz` |
| `tab_` | Tabelas estruturais | `tab_pc_trigonometria_angulos_notaveis.tex` | `tabela_trig.tex` |
| `cod_` | Snippets de programação/algoritmos | `cod_pg_lacos_repeticao.tex` | `codigo_while.txt` |

É estritamente proibido inventar abreviações para nomear arquivos. Você deve utilizar **obrigatoriamente** as tags oficiais listadas abaixo na composição do nome do arquivo (`[prefixo]_[eixo]_[tag_oficial]_[detalhe].[extensão]`).

### Eixo: Pré-Cálculo (`pc`)
| Módulo / Apostila | Tag Oficial Obrigatória | Exemplo de Uso Correto (Imagem) |
| :--- | :--- | :--- |
| Apostila 01 - Aritmética | `aritmetica` | `fig_pc_aritmetica_fracoes_pizza.png` |
| Apostila 02 - Álgebra Básica | `algebra` | `fig_pc_algebra_produtos_notaveis.png` |
| Apostila 03 - Trigonometria | `trigonometria` | `tkz_pc_trigonometria_ciclo_radianos.tex`|
| Apostila 04 - Conjuntos | `conjuntos` | `fig_pc_conjuntos_diagrama_venn.png` |
| Apostila 04 - Funções | `funcoes` | `fig_pc_funcoes_afim_raiz.png` |

*Nota: Não use "trig", "func", "arit". Copie a tag exata da coluna central.*

---

## 3. Catálogo de Ambientes Semânticos

Sempre que precisar destacar uma informação ou criar uma estrutura acadêmica, utilize os macros do Nivelamento. A numeração e as cores institucionais do eixo são aplicadas automaticamente.

**Atenção à Sintaxe de Etiquetas (Labels):** Para garantir que a numeração automática do gabarito e as referências cruzadas funcionem, os ambientes didáticos base exigem **dois colchetes sequenciais**: o primeiro para o título, e o segundo para a etiqueta oficial de rastreio. Se a questão não tiver título, você deve deixar o primeiro colchete vazio `[]`.

### Elementos Didáticos Base
```latex
\begin{exemplo}[Cálculo de Área][exemplo:pc_geometria_area]
    Considere um triângulo retângulo onde a base mede...
\end{exemplo}

% Exemplo SEM título especial, usando apenas colchetes vazios na primeira posição
\begin{exercicio}[][ex:pc_algebra_eq_segundo_grau]
    Resolva a equação de segundo grau: $x^2 - 5x + 6 = 0$.
\end{exercicio}

\begin{desafio}[Questão de Olimpíada][desafio:pc_geometria_angulos]
    Demonstre que a soma dos ângulos internos...
\end{desafio}

\begin{gabarito}{ex:pc_algebra_eq_segundo_grau} % Aponte para a exata etiqueta do exercício
    As raízes são $x_1 = 2$ e $x_2 = 3$.
\end{gabarito}
```

---

## 4. Referenciamento e Etiquetas (Labels)

É obrigatório que **todas** as estruturas lógicas do documento (seções, figuras, tabelas, equações, códigos e blocos didáticos) possuam uma etiqueta de identificação.

O formato da etiqueta deve respeitar a sintaxe de agrupamento do LaTeX combinada com as tags oficiais de cada eixo:

**Formato Geral:** `[categoria]:[eixo]_[assunto]_[detalhe]`

### Categorias Oficiais para Labels

| Estrutura | Prefixo (Categoria) | Exemplo de Uso Correto |
| :--- | :--- | :--- |
| **Seções e Capítulos** | `sec:` | `\label{sec:pc_trigonometria_introducao}` |
| **Subseções** | `subsec:` | `\label{subsec:fis_dinamica_atrito_estatico}` |
| **Figuras e Gráficos** | `fig:` | `\label{fig:qi_termoquimica_grafico_entalpia}` |
| **Tabelas** | `tab:` | `\label{tab:pg_sintaxe_operadores_logicos}` |
| **Equações Matemáticas**| `eq:` | `\label{eq:mat_geometria_area_circulo}` |
| **Trechos de Código** | `lst:` | `\label{lst:pg_repeticao_while_python}` |
| **Exercícios** | `ex:` | `[ex:pc_algebra_eq_segundo_grau]` * |
| **Exemplos** | `exemplo:` | `[exemplo:pc_geometria_area]` * |
| **Desafios** | `desafio:` | `[desafio:pc_geometria_angulos]` * |
| **Caixas (Atenção, Dica)**| `box:` | `\label{box:pc_conjuntos_atencao_divisao}` |

**Atenção à Sintaxe de Aplicação:** 
As estruturas textuais comuns (seções, figuras, tabelas, equações) recebem a etiqueta através do comando tradicional `\label{}` inserido dentro delas. 

* **Exceção (Ambientes Didáticos):** Para Exercícios, Exemplos e Desafios, o LaTeX **NÃO** aceita o comando `\label{}` solto no texto. A etiqueta deve ser obrigatoriamente passada no **segundo colchete** da declaração do ambiente, sem o comando `\label`.

**Exemplo da diferença:**
```latex
% Correto para uma equação (usa \label interno)
\begin{equation}
    x^2 = 4
    \label{eq:mat_basica_quadrado}
\end{equation}

% Correto para um exercício (usa o segundo colchete, sem \label)
\begin{exercicio}[Cálculo Simples][ex:mat_basica_quadrado_ex]
    Qual o valor de $x$?
\end{exercicio}
```

---

# PARTE 2: MANUAL DO ARTÍFICE

Esta seção é dedicada ao detalhamento e ao funcionamento das engrenagens internas do template e os protocolos de manutenção da infraestrutura modular.

## 5. Arquitetura do Template e Diretórios

O template está dividido em duas áreas de escopo isolado. Redatores operam **apenas** no diretório de conteúdo.

```text
/
├── main.tex                         (Arquivo raiz de compilação)
├── README.md                        (Este manual de diretrizes)
│
├── /conteudo                        (Área de Trabalho da Equipe)
│   └── cap_niv_tutorial.tex         (Exemplo de arquivo de texto)
│
└── /setup                           (Uso Exclusivo da Coordenação/Revisão)
    ├── /assets                      (Marcas e identidades visuais institucionais)
    │   ├── /eixos_icones            (Arquivos SVG com logo dos Eixos)
    │   ├── /titulo_texto            (Arquivos SVG com a logo "Nivelamento" na cor dos Eixos)
    │   └── /ufpa_itec               (Arquivos SVG das entidades colaboradoras do Nivelamento)
    │
    ├── /pre_textual                 (Molduras de diagramação fixa)
    │   ├── capa_principal.tex
    │   ├── capa_secundaria.tex
    │   └── folha_de_rosto.tex
    │
    ├── nivelamento_ambientes.sty    (Definições de caixas, cabeçalhos e gráficos)
    ├── nivelamento_base.sty         (Pacotes de compilação, idioma e matemática)
    ├── nivelamento_design.sty       (Paleta de cores e macros de logotipos)
    └── nivelamento_referencias.sty  (Normas ABNT e formatação de links)
```
---

## 6. Módulos Base

Para suportar o volume crescente de alunos e permitir que a equipe de voluntários trabalhem sem quebrar o documento, o código que governa as apostilas foi retirado do arquivo principal (`main.tex`) e dividido em quatro "motores" dedicados (os arquivos `.sty` localizados na pasta `/setup`). 

### Módulo Base (`Nivelamento_base.sty`)

O arquivo `nivelamento_base.sty` atua como o alicerce estrutural de todo o projeto em $\LaTeX$. Ele não define a estética, mas garante que tudo funcione de maneira estável e padronizada.

Para facilitar a manutenção técnica, as responsabilidades deste arquivo estão divididas em quatro pilares funcionais:

*   **1. Codificação e Localização (Idioma)**
    *   **O que faz:** Carrega pacotes fundamentais do sistema, como `inputenc`, `fontenc` e `babel`.
    *   **Impacto prático:** É este bloco que ensina o LaTeX a "falar" português. Ele garante que caracteres especiais do nosso idioma sejam processados corretamente sem quebrar a compilação, além de automatizar regras complexas, como a hifenização correta no final das linhas de texto.

*   **2. Geometria da Página**
    *   **O que faz:** Controla o pacote `geometry`.
    *   **Impacto prático:** Define matematicamente o tamanho do papel (A4) e estabelece as margens (superior, inferior, esquerda e direita). Ao isolarmos essa configuração aqui, impedimos que um erro humano altere acidentalmente as margens de uma única apostila, garantindo uniformidade na impressão de todos os eixos.

*   **3. Motores Matemáticos**
    *   **O que faz:** Incorpora a suíte completa da *American Mathematical Society* (pacotes `amsmath`, `amssymb`, `amsfonts`, entre outros).
    *   **Impacto prático:** Como a oficina lida fortemente com áreas de Exatas (como Pré-Cálculo e Física), este pilar fornece todo o arsenal de símbolos matemáticos, matrizes, fontes cursivas e alinhamento de equações complexas que os redatores necessitam para estruturar exemplos, exercícios resolvidos e demonstrações.

*   **4. Suporte a Mídias e Estruturas Básicas**
    *   **O que faz:** Importa bibliotecas essenciais de renderização, como `graphicx` e `float`.
    *   **Impacto prático:** Habilita o documento a importar imagens (PNG, JPG, SVG) de outras pastas e a ancorá-las corretamente na página, evitando que uma figura ou tabela flutue para um local indesejado e quebre a continuidade da leitura.

A regra para atualizar este arquivo é a universalidade. Se, no futuro, o projeto necessitar de um novo pacote de uso geral (por exemplo, um pacote para desenhar tabelas mais elegantes, como o `booktabs`), ele deve ser declarado exclusivamente dentro deste arquivo `nivelamento_base.sty`, e nunca no `main.tex`. Dessa forma, o novo recurso é imediatamente herdado por todos os arquivos do Nivelamento de forma silenciosa e centralizada.

### Módulo de Identidade Visual (`nivelamento_design.sty`)

Ele centraliza toda a identidade visual do Nivelamento e adapta a aparência da apostila de acordo com o eixo que está sendo compilado.

O coração deste arquivo é a macro condicional `\setDesign{}`, que funciona como uma chave mestra. Quando o coordenador digita `\setDesign{PC}` no arquivo principal, este módulo intercepta o comando e injeta instantaneamente toda a identidade do Pré-Cálculo na engrenagem do PDF.

Para blindar o layout e automatizar a estética, as responsabilidades deste arquivo estão divididas em três frentes:

*   **1. Paleta de Cores Matemáticas**
    *   **O que faz:** Utiliza o pacote `xcolor` para definir códigos hexadecimais exatos. Ele substitui cores rígidas por variáveis universais, nomeando-as como `main` (cor primária) e `main-dark` (cor de contraste).
    *   **Impacto prático:** Garante que todo o documento se adapte como um tema de sistema operacional. Se o eixo for Pré-Cálculo, a cor `main` pinta títulos, bordas e ícones de azul. Se o `main.tex` for alterado para Física, a mesma variável `main` injeta vermelho em todo o arquivo. O redator nunca precisa se preocupar com cores.

*   **2. Roteamento de Logotipos (Assets Institucionais)**
    *   **O que faz:** Cria macros semânticas (como `\logoTextoNivelamento` ou `\logoIconeEixo`) que embutem os caminhos de diretório exatos apontando para a pasta `/setup/assets_institucionais`.
    *   **Impacto prático:** Isola a complexidade das pastas. Os arquivos da capa e folha de rosto "puxam" essas variáveis cegas. É este módulo que decide se o ícone renderizado será o ícone do Eixo de Física ou o do Pré-Cálculo, impedindo que voluntários precisem caçar imagens soltas no repositório.

*   **3. Automação de Ementas e Nomenclaturas**
    *   **O que faz:** Armazena o nome oficial da disciplina (variável `\eixo`) e o longo parágrafo explicativo que a coordenação exige na segunda página (variável `\descricaoEixo`).
    *   **Impacto prático:** Padroniza a comunicação institucional. O redator não precisa digitar a ementa do curso ou lembrar o nome dos diretores do ITEC; o módulo preenche os documentos oficiais automaticamente, zerando o risco de inconsistências entre as apostilas.

A manutenção neste arquivo será extremamente rara e ocorrerá, via de regra, apenas quando a Oficina de Nivelamento inaugurar um novo eixo de ensino. Para expandir o sistema, o gestor não deve alterar os códigos antigos. O procedimento correto é copiar um bloco condicional inteiro (por exemplo, o bloco do `PC`), colá-lo ao final do arquivo, alterar a sigla identificadora (ex: `\IfSubStr{#1}{XX}`) e substituir os códigos hexadecimais e os caminhos dos novos SVGs. A arquitetura de variáveis garantirá que o novo eixo funcione perfeitamente com todas as capas e caixas semânticas já existentes.

### 7. Módulo de Estruturas Didáticas (`nivelamento_ambientes.sty`)

Este arquivo é o núcleo de diagramação avançada do projeto e o principal responsável por garantir a premissa de que o redator foca no conteúdo enquanto o sistema cuida do *layout*.

Seu objetivo é encapsular códigos complexos de desenho vetorial e formatação tipográfica dentro de comandos simples e intuitivos (como `\begin{exercicio}`). 

As competências deste módulo está estruturada em três frentes de atuação tipográfica e visual:

*   **1. Motores de Caixas e Meta-estilos (`tcolorbox`)**
    *   **O que faz:** Utiliza a biblioteca `tcolorbox` para desenhar os blocos visuais. Primeiro, ele cria "meta-estilos" (como o `estiloQuestao` e o `estiloNivelamento`), que funcionam como o CSS de uma página web, definindo regras universais de espaçamento interno (padding), cantos arredondados, quebra automática de páginas e sombras.
    *   **Impacto prático:** Garante coesão geométrica. Como todos os ambientes didáticos herdam esses meta-estilos, qualquer ajuste milimétrico feito pelo gestor (como aumentar a espessura da borda lateral) será propagado instantaneamente para todos os exercícios, exemplos e desafios de todas as apostilas.

*   **2. Ambientes Semânticos (Automação Didática)**
    *   **O que faz:** Transforma os meta-estilos em comandos reais para a equipe através da diretiva `\DeclareTColorBox`. Ele amarra a formatação visual a contadores automáticos, injeta os ícones do pacote `fontawesome` (como a lâmpada do Exemplo ou o troféu do Desafio) e gerencia a lógica das etiquetas (labels) em dois colchetes.
    *   **Impacto prático:** É o que permite a numeração inteligente. Este bloco rastreia em qual capítulo o redator está e gera numerações como "Exercício 1.1" de forma autônoma. Ele também impede que o gabarito perca a sincronia com a sua respectiva questão, gerindo as referências cruzadas.

*   **3. Hierarquia de Títulos e Navegação (`titlesec` e `tocloft`)**
    *   **O que faz:** Intercepta os comandos nativos do LaTeX (`\section`, `\subsection` e `\tableofcontents`) e os redesenha para aplicar a identidade visual do Nivelamento.
    *   **Impacto prático:** Substitui os títulos genéricos por uma hierarquia forte e corporativa. Além disso, formata o Sumário com pontilhados e espaçamentos profissionais, removendo qualquer necessidade de o redator diagramar essas páginas iniciais.

A intervenção neste arquivo será necessária apenas quando a organização dos Eixos decidir criar **uma nova categoria didática** no material. 

Por exemplo, se for decidido que as apostilas agora terão blocos de "Curiosidade" ou "Atenção", o gestor não precisa programar do zero. Basta copiar a estrutura do `\DeclareTColorBox` de um ambiente já existente (como o Exemplo), alterar o nome do comando de chamada, substituir o ícone da fonte `fontawesome` e ajustar a cor (utilizando as variáveis `main` ou cores de alerta, como `red!80!black`).# 2027_nivelas_apostila_template
