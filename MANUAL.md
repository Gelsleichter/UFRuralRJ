---
title: "UFRuralRJ -- Classe LaTeX para formatação de documentos acadêmicos na UFRuralRJ"
author: "Alessandro Samuel-Rosa"
date: "9 Fevereiro 2016"
output: html_document
---

# Apresentação

A classe `UFRuralRJ` constitui um classe LaTeX2e para formatação de documentos acadêmicos na Universidade 
Federal Rural do Rio de Janeiro (UFRuralRJ) de acordo com as recomendações contidas na terceira edição do 
*Manual de instruções para organização e apresentação de dissertações e teses na UFRRJ* (doravante referido 
como [MANUAL][manual]), Seropédica: UFRRJ, 25p, 2006. Trata-se de uma adaptação livre da class `mdtufsm.cls`, 
contida no pacore [`mdtufsm-ppgi v.1.4`][mdtufsm], desenvolvido pela Informática da Universidade Federal de 
Santa Maria ([UFSM][inf]), que é uma adaptação livre da classe `iiufrgs.cls`, contida pacote
[`iiufrgs-4.3.1`][iiufrgs], desenvolvido pelo UFRGS TeX Users Group. A meta é construir uma classe que atenda 
à (quase) totalidade das normas para formatação dos diferentes tipos de documentos acadêmicos produzidos na 
UFRuralRJ.

# Organização do uso do LaTeX

A construção do nosso documento acadêmico depende da criação de um diretório contendo a seguinte estrutura:

    UFRuralRJ
    |- capitulos
    |- figuras
    |- referencias
    |- principal.tex

## Preâmbulo

O preâmbulo é a parte do documento `principal.tex` onde você define os principais aspectos relacionados
à formatação final do seu documento acadêmico. 

### Definições gerais e pacotes

A primeira, e mais importante, definição feita no preâmbulo do documento `principal.tex` é quanto ao tipo de 
documento acadêmico suportado pela classe `UFRuralRJ`. Isso é feito usando o comando 
`\documentclass[<opções>]{<classe>}`. No momento a classe `UFRuralRJ` suporta dois tipos de documento 
acadêmicos: dissertação e tese. Se você estiver trabalhando em sua *tese*, use a opção `tese` conforme abaixo. 
Do contrário, use a opção `diss`.

    %% Definições gerais - tipo de documento
    \documentclass[tese]{UFRuralRJ}

A seguir, é preciso carregar os pacotes que darão suporte adicional à formatação do seu documento acadêmico.
Isso é feito usando o comando `\usepackage[<opções>]{<pacote>}`. Vários pacotes estão disponíveis, mas aqui 
apenas alguns de maior importância serão apresentados. Por exemplo, o fato de usamos acentuação na língua 
portuguesa requer que usemos pacotes que identifiquem corretamente os símbolos usados para a acentuação. Veja
alguns exemplos:
    
    %% Pacotes - língua, codificação e fonte
    \usepackage[brazilian]{babel}
    \usepackage[T1]{fontenc}
    \usepackage[utf8]{inputenc}

Outro pacote de grande utilidade é [`hyperref`][hyperref], o qual permite inserir hyperlinks no documento 
acadêmico. Hyperlinks são de grande utilidade quando o documento é publicado no formato PDF. Para carregar
o pacote `hyperref` usa-se o seguinte comando:

    %% Pacotes - formatação de hyperlinks e urls
    \usepackage[%hidelinks%, 
                bookmarksopen=true, linktoc=page, colorlinks=true,
                linkcolor=blue, citecolor=blue, filecolor=magenta, urlcolor=blue,
                pdftitle={UFRuralRJ -- Classe LaTeX para formatação de documentos acadêmicos na UFRRJ},
                pdfauthor={Graziela Barroso},
                pdfsubject={Tese de Doutorado},
                pdfkeywords={LaTeX, UFRuralRJ, Documentos acadêmicos}
                ]{hyperref}

O pacote `hyperref` possui uma série de opções, as quais são definidas dentro do espaço delimitado pelos 
colchetes no comando `\usepackage`. Essas opções permitem, por exemplo, definir a cor dos hyperlinks no texto,
bem como atribuir propriedades ao documento PDF resultante tais como o seu título e autor.

Finalmente, um importante pacote usado para formtar as citações no texto e a lista de referências 
bibliográficas no final do documento conforme as normas da ABNT: [`abntex2cite`][abntex2cite].

    %% Pacotes - formatação da bibliografia de acordo com as normas da ABNT
    \usepackage[alf, abnt-etal-cite=2, abnt-etal-list = 0]{abntex2cite}

Com o uso do pacote `abntex2cite` você está livre do árduo trabalho de formatar as citações e a lista de 
referências bibliográficas. A única exigência, é claro, é que você tenha todos os dados de suas referências 
bibliográficas organizados em uma base de dados. (Note que o pacote `abntex2cite` precisa, obrigatoriamente, 
ser carregado depois do pacote `hyperref`.)

### Dados para os elementos pré-textuais

Ainda no preâmbulo do documento definimos uma série de parâmetros que serão usados pela `UFRuralRJ` para 
construir as páginas iniciais do documento acadêmico, ou seja, a capa, a folha de rosto, a folha de aprovação,
e o resumo. Esses são os elementos pré-textuais do documento acadêmico. Considere o seguinte exemplo de dados 
de identificação do trabalho:

    %% Identificação do trabalho
    \titulo{UFRuralRJ -- Classe \LaTeX{} para Formatação de Documentos Acadêmicos na UFRRJ}
    \author{Barroso}{Graziela}
    \autoratrue
    \instituto{Instituto de Agronomia}
    \curso{Curso de Pós-Graduação em Agronomia -- Ciência do Solo}
    \area{Ciência do Solo}
    \local{Seropédica}{RJ}{Brasil}

O comando `\titulo{<titulo do documento>}` é utilizada para definir o título do trabalho acadêmico, enquanto o 
comando `\author{<sobrenome do autor>}{<nome do autor>}` serve para identificar o autor, sendo informado 
primeiro o sobrenome, e depois o nome. Note que após a definição do nome do autor, usamos o comando
`\autoratrue`. Esse comando serve para informar a `UFRuralRJ` que o autor é do gênero feminino, ou seja, 
trata-se de uma autora. Qual a importância disso? Bem, a `UFRuralRJ` foi arquitetada de maneira a lidar, 
automaticamente, com as definições relacionadas ao gênero do autor. Por exemplo, no caso de uma tese elaborada 
por um autor do gênero feminino, `UFRuralRJ` identificará automaticamente que o título atribuído é de *doutora*
ao invés de *doutor*, desde que o comando `\autoratrue` seja utilizado. Caso o autor seja do gênero masculino,
basta remover o comando `\autoratrue` do documento, ou substituí-lo pelo comando contrário `\autorafalse`.

A utilidade do próximo comando usado na identificação do trabalho é bastante óbvia. 
`\instituto{<nome do instituto>}` refere-se ao nome do instituto da UFRRJ no qual o curso de pós-graduação está
lotado. No exemplo acima o nome do instituto foi inserido por extenso. Contudo, também poderia ter sido usada o
comando `\IA`, ou seja, `\instituto{\IA}`. Outros comandos disponíveis para definir o nome do instituto sâo:

* `\IA`: Instituto de Agronomia
* `\IB`: Instituto de Ciências Biológicas e da Saúde
* `\ICE`: Instituto de Ciências Exatas
* `\ICHS`: Instituto de Ciências Humanas e Sociais
* `\IE`: Instituto de Educação
* `\IF`: Instituto de Florestas
* `\IM`: Instituto Multidisciplinar
* `\IT`: Instituto de Tecnologia
* `\IV`: Instituto de Veterinária
* `\IZ`: Instituto de Zootecnia

O comando `\curso{\nome do curso>}`, como pode-se adivinhar, serve para definir o nome do seu curso de
pós-graduação. Talvez, num futuro próximo, `UFRuralRJ` também incluirá comandos com os nomes dos cursos de 
pós-graduação assim como mostrado acima para os institutos. Segue-se que `\area{<area de concentracao>}` serve
para definir a área de concentração do trabalho acadêmico e/ou do curso de pós-graduação. Enquanto isso, 
`\local{<cidade>}{<estado>}{<país>}` especifica o local da defesa, o qual deve estar na seguinte ordem: cidade,
estado, país. Note que a opção da classe `UFRuralRJ` é por não traduzir nomes próprios em português para outras
línguas. Assim, o nome da universidade, do instituto, e do curso de pós-graduação aparecem sempre em português.

Na sequência, é preciso informar `UFRuralRJ` a cerca dos seus orientadores. Esses dados são usados para 
construir a folha de rosto do seu documento acadêmico. Suponhamos que o seu orientador seja do gênero feminino,
ou seja, uma orientadora, e que, além dela, você possua dos orientadores. Nesse caso, os dados a cerca dos 
seus orientadores devem ser informados da seguinte maneira:

    %% Identificação dos orientadores
    \advisor[Professora]{Dra.}{Dobereimer}{Johana}{UFRRJ}
    \coadvisor[Pesquisador]{Dr.}{Salles}{Hilton}
    \coadvisor[Professor]{Dr.}{Costa}{Fernando}
    
Todas as informações a cerca do orientador são passadas à `UFRuralRJ` usando o comando `\advisor[]{}{}{}{}`. 
Isso inclui, nesta ordem, o cargo ocupado na Universidade (Professor, Pesquisador), o maior título acadêmico 
(Dr., Dra., MSc.), e a sigla da instituição onde está lotado. Note que, assim como no nome do autor do 
documento academico, primeiro informa-se o sobrenome e depois o nome do orientador. As mesmas regras valem 
para os coorientadores, cujas informações são passadas à `UFRuralRJ` usando o comando `\coadvisor[]{}{}{}`. A
diferença aqui é que não há necessidade de informar a sigla da instituição onde seus coorientadores estão
lotados. (NOTA: num futuro próximo não haverá necessidade de informar o cargo ocupado na Universidade, nem
a sigla da instituição onde está lotado.)

Finalmente, as informações a cerca da defesa são passadas à `UFRuralRJ` usando dois comandos: 
`\committee[]{}{}{}` e `\date{}{}{}`. Veja o exemplo abaixo onde o comitê examinador possui cinco membros:

    %% Informações sobre a defesa
    \committee[Dr.]{Raithe}{Waldemar}{UFRRJ}
    \committee[Dra.]{Campos}{Maria Aparecida}{UFRRJ}
    \committee[Dr.]{Peçanha}{Gilberto Gastim}{UFRRJ}
    \committee[Dra.]{Souza}{Tânia Maria Melquiades de}{UFRRJ}
    \committee[Dr.]{Groszman}{Américo}{UFRRJ}
    \date{30}{Fevereiro}{2001}

O comando `\committee[]{}{}{}` espera quadro informações, nesta ordem: o maior título acadêmico (Dr., Dra.,
MSc.), o sobrenome, o nome, e a sigla da instituição onde está lotado. Note que `\committee[]{}{}{}` pode 
ser usado tantas vezes quantos forem os membros do comitê examinador, sendo importante observar que a primeira 
ocorrência define o presidente do comitê examinador. Em geral, o presidente do comitê examinador é o seu
próprio orientador. E o comando `\date{<dia>}{<mes>}{<ano>}`, conforme pode-se adivinhar, serve para informar a
data da defesa do documento acadêmico (na ordem dia, mês, ano), lembrando que o nome do mês deve ser redigido
sempre em português.

## O corpo do documento acadêmico

Em seu documento principal (*master*), o início do documento acadêmico propriamente dito é marcado pelo 
seguinte comando:

    %% Início do documento
    \begin{document}

Já o fim do documento acadêmico é marcado por:

    %% Fim do documento
    \end{document}
    
Assim sendo, tudo aquilo que constitui o documento acadêmico, sejam eles elementos pré-textuais, textuais, e 
pós-textuais, são inserido entre os comandos `\begin{document}` e `\end{document}`.

### Elementos pré-textuais obrigatórios

Você precisa informar `UFRuralRJ` onde os elementos pré-textuais devem ser inseridos. Para isso, basta usar os
seguintes comandos (nesta ordem):

    %% Inserir capa, folha de rosto, e folha de aprovação
    \maketitle
    \makeapprove

Pronto!!! Desde que todas as informações necessárias tenham sido passadas à `UFRuralRJ` acima, no preâmbulo do 
seu documento principal, os dois simples comandos `\maketitle` e `\makeapprove` se encarregarão do serviço de
formatar e posicionar no local correto a capa, a folha de rosto, e a folha de aprovação do seu documento 
acadêmico, sem que você tenha que fazer qualquer esforço. Mas lembre-se de que eles devem ser inseridos sempre
após `\begin{document}`.

### Elementos pré-textuais opcionais



### Mais elementos pré-textuais obrigatórios

#### Resumo do documento acadêmico

Um importante elemento pré-textual obrigatório é o resumo do documento acadêmico. A classe `UFRuralRJ` possui
dois tipos de resumo, cada um pensado para um tipo de documento acadêmico. O primeiro deles é o que chamamos de
*resumo geral*. O resumo geral é usado em documentos acadêmicos construídos usando capítulos individuais, ou
seja, capítulos preparados de maneira que possam ser lidos individualmente, muitas vezes baseados em 
trabalhos publicados em revistas científicas na forma de artigo, revisão bibliográfica, ou nota científica. 
O outro tipo de resumo do documento acadêmico oferecido por `UFRuralRJ` é o que chamamos de *resumo simples*, 
o qual corresponde ao resumo de todo o documento acadêmico quando o mesmo é construído a partir de capítulos 
sequenciais, ou seja, como \emph{texto corrido}.

Consideremos o exemplo acima, onde nosso documento acadêmico constitui uma tese de doutorado composta por 
capítulos individuais. Nesse caso, usa-se o *resumo geral*, primeiro em português:

    %% Definições do resumo geral
    \def\tituloPT{UFRuralRJ -- Classe \LaTeX{} para formatação de documentos acadêmicos na UFRRJ}
    \def\chavesPT{\LaTeX. UFRuralRJ. Documentos acadêmicos}
    \def\nivelPT{Doutorado em Agronomia, Ciência do Solo}
    
    %% Resumo geral
    \generalabstracttrue
    \begin{generalabstract}{brazilian}{\tituloPT}{\chavesPT}{\nivelPT}
    Este é o resumo geral em português de uma tese organizada na forma de capítulos individuais.
    \end{generalabstract}

Depois em inglês:

    %% General abstract definitions
    \def\tituloEN{UFRuralRJ -- \LaTeX{} class for formatting academic documents at UFRRJ}
    \def\chavesEN{\LaTeX. UFRuralRJ. Academical documents}
    \def\nivelEN{Doctor of Science in Agronomy, Soil Science}
    
    %% General abstract
    \generalabstracttrue
    \begin{generalabstract}{english}{\tituloEN}{\chavesEN}{\nivelEN}
    This is the English abstract of a thesis organized in the form of individual chapters.
    \end{generalabstract}

Primeiro, vejamos qual a diferença entre o *resumo geral* e o *resumo simples*. Note, nos exemplos acima, a
macro `\generalabstracttrue`. É esta macro a responsável por informar à `UFRuralRJ` que o resumo que estamos
construíndo é do tipo geral ao invés de simples. Assim, no caso de *resumo simples*, basta remover a macro
`\generalabstracttrue`, ou usar `\generalabstractfalse`. Simples assim!!!

Vejamos agora os outros elementos usados para definir o resumo de nosso documento acadêmico. Para ambos o 
*resumo geral* e o *resumo simples*, o resumo do documento acadêmico sempre é construído usando o ambiente
`generalabstract`, o qual aceita cinco informações: o idioma do resumo, o título do documento acadêmico, as 
palavras-chave, o nível do grau obtido, e o texto do resumo.

    \begin{generalabstract}{<idioma>}{<titulo>}{<palavras-chaves>}{<nivel>}
    <texto>
    \end{generalabstract}

Com excessão do texto do resumo, todas as outras informações são passadas entre chaves, conforme demonstrado
acima. A soma dessas informações geralmente resulta em um linha bastante longa. A fim de facilitar a
manipulação e leitura de nosso documento, podemos usar as funcionalidades do LaTeX e criar definições para
cada um dos itens do resumo usando o comando [`\def`][def]. Aqui, o comando `\def` recebe dois argumentos: o 
primeiro é a identificação daquilo que estamos definindo; o segundo é o seu conteúdo. Assim, o comando

    \def\chavesPT{\LaTeX. UFRuralRJ. Documentos acadêmicos}

resulta na definição de um novo comando chamado `\chavesPT`, o qual contém as palavras-chave em português, tal 
qual definido em `{\LaTeX. UFRuralRJ. Documentos acadêmicos}`. A função do novo comando `\chavesPT` é inserir,
no local onde for usado, as palavras-chave em português. (Note que o uso de `\def` é puramente estética.)

#### Listas e sumário

Os últimos elementos pré-textuais obrigatórios são as listas e os sumários. Atualmente, `UFRuralRJ` suporta o
uso de quatro tipos de listas: figuras, tabelas, apêndices, e anexos. Para inserir essas listas no documento 
basta usar os seguintes comandos:

    \listoffigures  %% Lista de figuras
    \listoftables   %% Lista de tabelas
    \listofappendix %% Lista de apêndices
    \listofannex    %% Lista de anexos

Para inserir o [sumário][toc], basta usar o seguinte comando:

    \tableofcontents

Novamente, tudo muito simples, graças à capacidade de `UFRuralRJ` identificar, automaticamente, quais itens ao
longo do texto pertencem a cada lista ou ao sumário. Caso seu documento não possua figuras, tabelas, apêndices,
ou anexos, basta remover o respectivo comando mostrado acima.

### Corpo principal do documento acadêmico

O corpo principal do documento acadêmico é constituído pelo texto propriamente dito, isto é, aquilo que você 
escreveu a cerca de suas experiências científicas ao longo dos anos de seu curso. A forma de organização desse 
texto pode variar conforme descrito acima. Também existem diferentes maneira de você gerenciar esse texto. Uma 
delas é redigindo todo o texto no seu documento `*.tex` principal. Contudo, do ponto de vista organizacional, 
essa não é uma boa estratégia pois o seu documento `*.tex` principal ficará extremamente longo, dificultando a 
navegação ao longo do mesmo. Além disso, um documento muito longo acaba usando grande quantidade da memória do 
seu computador.

A melhor estratégia de gerenciar o texto de seu documento acadêmico é usar um arquivo individual para cada 
parte ou capítulo. Especificamente, você usa um arquivo `*.tex` individual para escrever a Introdução Geral,
outro arquivo `*.tex` para o Capítulo I, outro arquivo `*.tex` para as Conclusões Gerais, e assim por diante.
Apesar do exemplo para documentos acadêmicos organizados na forma de capítulos individuais, o mesmo se aplica
para documentos em texto corrido. Por exemplo, imagine que você escreveu tese com cinco grandes partes 
principais: Introdução, Revisão da Literatura, Material e Métodos, Resultados, Discussão, e Conclusões. Basta
escrever cada uma dessas grandes partes principais em um arquivo `*.tex` individual.

Os arquivos `*.tex` individuais usados para redigir cada capítulo ou cada grande parte principal do documento
acadêmico devem ser armazenados em um diretório também individual a fim de garantir melhor organização do 
trabalho. Feito isso, basta usar o comando [`\include`][include], conforme segue:

    %% Incluir texto do corpo principal
    \include{capitulos/introducao.tex}
    \include{capitulos/capitulo01.tex}
    \include{capitulos/capitulo02.tex}
    \include{capitulos/conclusao.tex}

No nosso exemplo, todos os arquivos `*.tex` individuais estão armazenados em um diretório chamado `capitulos`.
Os nomes dos arquivos permitem adivinhar o seu conteúdo. Aqui, o comando `\include` cumprirá a tarefa de 
incluir, exatamente neste ponto do documento, o conteúdo da Introdução Geral, dos dois capítulos, e da 
Conclusão Geral. Se, por acaso, mais tarde, você e seus orientadores decidirem modificar a ordem dos capítulos
no documento acadêmico, basta alterar a ordem em que cada arquivo `*.tex` é incluído. Simples assim!

O último item do corpo principal do documento acadêmico é a lista de referências bibliográficas. Para inserir 
essa lista no seu documento acadêmico basta usar simples o comando [`\bibliography`][bibliography]:

    %% Inserir lista de referências bibliográficas
    \bibliography{referencias/biblio.bib}

onde `referencias` é o nome do diretório onde se encontra sua base de dados de referências bibliográficas no 
formato [BibTeX][bibtex], e `biblio.bib` é o nome dessa base de dados de referências bibliográficas.



[abntex2cite]: http://www.abntex.net.br/
[bibtex]: https://en.wikibooks.org/wiki/LaTeX/Bibliography_Management#BibTeX
[bibliography]: https://en.wikibooks.org/wiki/LaTeX/Bibliography_Management
[def]: https://en.wikibooks.org/wiki/TeX/def
[iiufrgs]: http://www.inf.ufrgs.br/utug
[inf]: http://www.inf.ufsm.br
[include]: https://en.wikibooks.org/wiki/LaTeX/Modular_Documents#Getting_LaTeX_to_process_multiple_files
[hyperref]: https://en.wikibooks.org/wiki/LaTeX/Hyperlinks
[manual]: http://www.ufrrj.br/portal/modulo/dppg/Formularios_normas/manual_teses.pdf
[mdtufsm]: https://code.google.com/p/mdtufsm-ppgi/
[toc]: https://en.wikibooks.org/wiki/LaTeX/Document_Structure#Table_of_contents
