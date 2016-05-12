# Versão 0.10 (11-Maio-2016)
* Automatiza a formatação dos itens da parte preliminar do documento acadêmico quando usadas as opções 
  'twoside' e 'openright'. Quando usadas essas opções, os itens da parte preliminar do documento acadêmico
  devem ser impressos somente nas páginas do lado direito (páginas ímpares), ficando as páginas do lado 
  esquerdo (páginas pares) em branco. A solução implementada usa o pacote `afterpage`, sendo completamente
  eficiente apenas quando os itens da parte preliminar do documento acadêmico tiverem, no máximo, duas páginas.
  Soluções manuais deverão ser implementadas quando o número de páginas for superior à dois.

# Versão 0.9 (20-Abril-2016)
* Corrige texto de definição da data de aprovação do documento acadêmico.
* Automatiza conversão da data numérica para nominal (mês).
* Ajusta o posicionamento da nota de rodapé usada com o título do capítulo (`\chapternote{<footnote>}`).
* Corrige a largura da numeração das seções no sumário (`<numwidth>`) a fim de evitar a sobrepocição 
  número/texto quando a numeração da seção atinge mais do que dois dígitos.
* Inclui as opções da classe `twoside` e `openright` para formatação do documento acadêmico quando o mesmo
  é impresso em frente e verso.
* Corrige o tamanho da margem superior da página inicial dos itens principais do corpo do texto (1 cm abaixo 
  da margem superior).
* Inclui exemplo de documento acadêmico impresso em frente e verso.
* Inclui nova versão do manual de uso em http://samuel-rosa.github.io/UFRuralRJ/_book/.

# Versão 0.8 (11-Fevereiro-2016)
* Melhoria dos contadores de artigos (documentos organizados na forma de capítulos individuais), apêndices e 
anexos a fim de usar corretamente comandos como `\label` e `\autoref`.

# Versão 0.7 (09-Fevereiro-2016)
* Várias pequenas correções na formatação do sumário e numeração de itens ao longo do texto foram feitas.
* Os dois modelos de documento foram atualizados levando em conta as últimas modificações da classe.
* O manual de uso da classe foi criado.

# Versão 0.6 (08-Fevereiro-2016)
* A formatação da numeração alfabética dos apêndices e anexos foi aprimorada usando contadores próprios para 
cada um deles.
* A numeração romana dos capítulos quando do documento em forma de capítulos (possivelmente baseados em 
artigos) foi otimizada usando um contador específico.
* O novo comando ```\chapternote``` foi criado para adicionar nota de rodapé não numerada ao título dos 
capítulos quando do documento organizado na forma de capítulos.

# Versão 0.5 (05-Fevereiro-2016)
* A configuração do sumário foi melhorada significativamente. Isso inclui a adição de espaço vertical antes e
  depois do título de cada capítulo, além da indentação sequencial das seções e subseções. Agora o Apêndice e o
  Anexo também recebem numeração arábica na sequência dos capítulos anteriores. O mesmo ocorre com a lista de
  Referências Bibliográficas, graças ao uso do pacote ```tocbibind```.
    + No caso da inclusão de ambos Anexo e Apêndice, a segunda entrada aparece, erroneamente, com numeração
    em estilo alfabético.
* A formatação das primeiras páginas da tese (capa, folha de rosto, etc) foi melhorada usando o pacote babel.
  Isso dispensa a necessidade de informar todos os dados no texto pois padrões internos foram definidos de
  acordo com o tipo de documento. Erros de formatação (tamanho de fonte) também foram corrigidos.
* A definição do espaçamento vertical antes e depois das seções no texto foi modificada com a finalidade de 
  melhorar a aparência do texto. Agora, mais espaço vertical é deixado acima do que abaixo do título da seção.
* O ambiente ```generalabstract``` também foi melhorado. Ele agora inclui um quarto argumento (o primeiro define o idioma, o segundo o título, e o terceiro as palavras-chave) dedicado à definição do título que será recebido.
  Por exemplo: 'Doutor em Ciências'. Este quarto argumento é necessário para atender às necessidades dos
  diferentes idiomas em que o ```generalabstract``` é escrito.
* O ambiente ```chapterabstract``` foi modificado no que diz respeito à definição do espaçamento entre linhas. 
Anteriormente, o espaçamento entre linhas no ```chapterabstract``` (simples) era definido em função do
espaçamento entre linhas do texto no carpo do documento. Isso resultava eficiente quando o texto no corpo do
documento estava com espaçamento entre linhas de 1,5. Agora o ```chapterabstract``` e o resto do texto possuem o
mesmo espaçamento entre linhas.

# Versão 0.4 (21-Out-2015)
* Duas novas opções para a classe foram criadas: `header`, para incluir um
  cabeçalho com um título curto do capítulo (`\shorttitle{}`), e `newmargins`,
  para produzir margens otimizadas para uso do espaço da página (2 cm em ambos
  os lados direito e esquerdo, e 2.5 cm no topo e base da página).
* Corrigido bug que inseria o número da página na primeira página dos capítulos.

# Versão 0.3 (08-Out-2015)
* Novo ambiente `\generalabstract` para construir o resumo geral usando 
  informações sobre a língua escolhida para o documento (pacote babel);
* Informações sobre os diferentes tipos de documentos acadêmicos agora são 
  definidas automaticamente conforme a língua escolhida usando o pacote babel;
* Alguns comandos foram redefinidos usando uma escrita em língua portuguesa
  para facilitar o uso da classe por alunos que não dominam a língua inglesa,
  comumente usada para a definição dos comandos.
* Dois exemplos estão disponíveis: um em texto corrido, o outro com capítulos
  individuais.

# Versão 0.2 (16-Jun-2015)
* As palavras-chave em português são separadas por vírgula;
* O comando `\altCurso{}`, usado para fornecer um nome alternativo para o curso,
  foi desativado;
* Usando `\noindent{}` para evitar indentação da primeira linha do resumo e
  abstract;
* Novos comandos `\chapterabstract{}` e `\formatchapter`, usados para adicionar
  o resumo dos capítulos individuais em diferentes línguas, e formatar o início
  do texto do capítulo.

# Versão 0.1 (19-Jan-2015)
* Primeira versão da classe LaTeX UFRuralRJ;
* Classe em desenvolvimento.
