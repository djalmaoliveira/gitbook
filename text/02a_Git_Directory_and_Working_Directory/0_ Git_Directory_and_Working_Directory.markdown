## Diret�rio Git e Diret�rio de Trabalho ##

### O Diret�rio Git ###

O 'diret�rio git' � o diret�rio que armazena todos os hist�ricos Git e meta
informa��es do seu projeto - incluindo todos os objetos (commits, trees,blobs,
tags), todos os ponteiros onde os diferentes branches est�o e muito mais.

Existe somente um Diret�rio Git por projeto (o oposto de um por sub diret�rio
como no SVN ou CVS), e que o diret�rio � (por padr�o, embora n�o 
necessariamente) '.git' na raiz do seu projeto. Se voc� olha no conte�do desse
diret�rio, voc� pode ver todos os seus importantes arquivos:

    $>tree -L 1
    .
    |-- HEAD         # aponta para o seu branch atual
    |-- config       # suas configura��es preferenciais
    |-- description  # descri��o do seu projeto 
    |-- hooks/       # pre/post action hooks
    |-- index        # arquivo de index (veja a pr�xima se��o)
    |-- logs/        # um hist�rico de onde seus branches tem estado
    |-- objects/     # seus objetos (commits, trees, blobs, tags)
    `-- refs/        # ponteiros para os seus branches

(podem existir alguns outros arquivos/diret�rios aqui mas eles n�o s�o importantes agora)


### O Diret�rio de Trabalho ###

O 'diret�rio de trabalho' do Git � o diret�rio que det�m o checkout atual dos 
arquivos sobre o qual voc� est� trabalhando. Arquivos nesse diret�rio s�o
frequentemente removidos ou renomeados pelo Git quando voc� troca de branches - 
isso � normal. Todos os seus hist�ricos s�o armazenados no diret�rio Git; o 
diret�rio de trabalho � simplesmente um lugar tempor�rio de checkout onde voc� 
pode modificar os arquivos at� o pr�ximo commit.