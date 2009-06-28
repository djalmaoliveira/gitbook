﻿## O Modelo de Objetos do Git ##

### O SHA ###

Todas as informações necessárias para representar a história do projeto
são armazenados em arquivos referenciados por um "nome do objeto" de 40
dígitos que se parece com isso:

    6ff87c4664981e4397625791c8ea3bbb5f2279a3

Você verá esses 40 dígitos em todo lugar no Git.
Em cada caso o nome é calculado baseado no valor hash SHA1 do conteúdo do
objeto. O hash SHA1 é uma função criptográfica.
O que isso significa para nós é que ele é virtualmente impossível de encontrar
dois objetos diferentes com o mesmo nome. Isso tem inúmeras vantagens; entre
outras:

- Git pode rapidamente determinar se dois objetos são idênticos ou não, somente
  comparando os seus nomes.
- Visto que os nomes dos objetos são calculados da mesma forma em todo o
  repositório, o mesmo conteúdo armazenado em dois repositórios sempre será
  armazenado sobre o mesmo nome.
- Git pode detectar erros quando lê um objeto, através da checagem do nome
  do objeto que ainda é o hash SHA1 do seu conteúdo.

### Os Objetos ###

Todo objeto consiste de 3 coisas - um **tipo**, um **tamanho** e **conteúdo**.
O _tamanho_ é simplesmente o tamanho do conteúdo, o conteúdo depende do tipo
que o objeto é, e existem quatro tipos diferentes de objetos:
"blob", "tree", "commit", and "tag".

- Um **"blob"** é usado para armazenar dados do arquivo - é geralmente um
  arquivo.
- Um **"tree"** é basicamente como um diretório - ele referencia um conjunto
  de outras trees e/ou blobs (ex.: arquivos e sub-diretórios)
- Um **"commit"** aponta para uma simples tree, fazendo com que o projeto
  se parecesse em um determinado ponto no tempo. Ele contém meta informações
  sobre aquele ponto no tempo, por exemplo um timestamp, o autor das modificações
  desde o último commit, um ponteiro para um commit anterior, etc.
- Uma **"tag"** é uma forma de marcar um commit específico de alguma forma
  como especial. Ele é normalmente usado para identificar certos commits como
  versões/revisões específicas ou alguma coisa junto a aquelas linhas.

Quase tudo do Git é construído através da manipulação dessa simples estrutura
de quatro diferentes tipos de objetos. Eles são organizados dentro se seu
próprio sistema de arquivos que estão sobre o sistema de arquivos de sua
máquina.

### Diferenças do SVN ###

É importante notar que isso é muito diferente da maioria dos sistemas SCM com
que você pode estar familiarizado. Subversion, CVS, Perforce, Mercurial e como
todos eles usam sistemas _Delta Storage_ - como eles armazenam as diferenças
entre um commit e o próximo. Git não faz isso - ele armazena um snapshot de
todos os arquivos de seu projeto como eram nessa estrutura em árvore no momento
de cada commit, é claro que isso não significará (necessariamente) que seu 
histórico do repositório atingirá um tamanho enorme. Usando "git gc", o Git fará
alguma limpeza interna, incluindo compressão de arquivos de revisão. Esse é um 
conceito muito importante para entender quando estiver usando Git.
