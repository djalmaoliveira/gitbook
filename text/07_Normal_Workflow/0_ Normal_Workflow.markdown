﻿## Fluxo Normal de Trabalho ##

Altere alguns arquivos, então adicione seus conteúdos alterados para o index:

    $ git add file1 file2 file3

Você agora está pronto para realizar o commit. Você pode ver o que será levado
para commit usando linkgit:git-diff[1] com a opção --cached:

    $ git diff --cached

(Sem a opção --cached, linkgit:git-diff[1] mostrará a você qualquer modificação
que você tem feito mas ainda não foi adicionado no index). Você pode também 
conseguir uma breve sumário da situação com linkgit:git-status[1]:

    $ git status
    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #	modified:   file1
    #	modified:   file2
    #	modified:   file3
    #

Se você precisar fazer qualquer ajustes a mais, então faça-o agora, e então
adicione qualquer novo conteúdo modificado no index. Finalmente, commit
suas mudanças com:

    $ git commit

Isso irá novamente mostrar a você uma mensagem descrevendo as mudanças, e
então gravar uma nova versão do projeto.

Alternativamente, ao invés de executar `git add`, você pode usar:

    $ git commit -a
    
que irá automaticamente avisar sobre quaisquer arquivos modificados (mas não 
novos), adicioná-los no index, e realizar o commit, tudo de uma vez.

Uma nota sobre as mensagens de commit: Embora não necessário, é uma boa
ideia iniciar a mensagem de commit em uma linha curta (menos do que
50 caracteres) resumindo as mudanças, seguido por uma linha em branco e então,
mais uma descrição profunda. Ferramentas que transformam commits em emails, por
exemplo, usam a primeira linha para o Assunto: e o resto da mensagem do commit 
para o corpo do email.


#### Git percebe conteúdo não arquivos ####

Muitos sistemas de controle de revisões dispõem de um comando "add" que
chama o sistema para iniciar a busca por mudanças em novos arquivos. O comando
"add" faz algumas coisas das mais simples as mais poderosas: `git add` é usado
ambos para arquivos novos e arquivos alterados, e em ambos os casos fornece um 
snapshot dos arquivos dados e os que estão no index, prontos para inclusão no 
próximo commit. 

[gitcast:c2_normal_workflow]("GitCast #2: Fluxo Normal de Trabalho")