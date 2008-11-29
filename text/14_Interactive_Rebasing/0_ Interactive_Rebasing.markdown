## Rebasing Interativo ##

Voc� pode tamb�m realizar um rebase interativamente. Isso � usado muitas vezes
para re-escrever seus pr�prios objetos commit antes de envi�-los para algum 
lugar. Isso � uma forma f�cil de dividir, juntar, ou re-ordenar os commits
antes de compartilh�-los com os outros. Voc� pode tamb�m us�-lo para limpar 
commits que voc� tenha baixado de algu�m quando estiver aplicando ele 
localmente.

Se voc� tem um n�mero de commits que voc� gostaria de alguma maneira modificar
durante o rebase, voc� pode invocar o modo interativo passando um '-i' ou 
'--interactive' para o comando 'git rebase'.

	$ git rebase -i origin/master

Isso invocar� o modo de rebase interativo sobre todos os commits que voc� tem 
feito desde a �ltima vez que voc� realizou um pull (ou merge de um reposit�rio
origin).

Para ver de antem�o quais s�o os commits, voc� pode executar dessa forma:
	
	$ git log origin/master..

Uma vez que voc� rodar o comando 'rebase -i', voc� ser� levado para o seu 
editor com algo parecido com isso:

	pick fc62e55 added file_size
	pick 9824bf4 fixed little thing
	pick 21d80a5 added number to log
	pick 76b9da6 added the apply command
	pick c264051 Revert "added file_size" - not implemented correctly

	# Rebase f408319..b04dc3d onto f408319
	#
	# Commands:
	#  p, pick = use commit
	#  e, edit = use commit, but stop for amending
	#  s, squash = use commit, but meld into previous commit
	#
	# If you remove a line here THAT COMMIT WILL BE LOST.
	# However, if you remove everything, the rebase will be aborted.
	#

Isso significa que existem 5 commits desde o �ltimo push realizado e lhe dar�
uma linha por commit com o seguinte formato:

	(action) (partial-sha) (short commit message)

Agora, voc� pode alterar a a��o (que � por padr�o 'pick') para qualquer um 
'edit' ou 'squash', ou deix�-lo como 'pick'. Voc� tamb�m pode re-ordenar os
commits movendo as linhas como voc� quiser. Ent�o, quando voc� sair do editor,
o git tentar� aplicar os commits como eles est�o organizados agora e realizar a
a��o especificada.

Se 'pick' � especificado, ele simplesmente tentar� aplicar o patch e salvar o
commit com a mesma mensagem de antes.

Se 'squash' � especificado, ele combinar� aquele commit com um anterior para 
criar um novo commit. Voc� cair� novamente em seu editor para juntar as 
mensagens de commit dos dois commits que agora s�o combinados. Ent�o, se voc�
sair do editor com isso:

	pick   fc62e55 added file_size
	squash 9824bf4 fixed little thing
	squash 21d80a5 added number to log
	squash 76b9da6 added the apply command
	squash c264051 Revert "added file_size" - not implemented correctly

Ent�o voc� ter� que criar uma �nica mensagem de commit dele:

	# This is a combination of 5 commits.
	# The first commit's message is:
	added file_size

	# This is the 2nd commit message:

	fixed little thing

	# This is the 3rd commit message:

	added number to log

	# This is the 4th commit message:

	added the apply command

	# This is the 5th commit message:

	Revert "added file_size" - not implemented correctly

	This reverts commit fc62e5543b195f18391886b9f663d5a7eca38e84.

Uma vez que voc� tem editado a mensagem de commit e sair do editor,
o commit ser� salvo com a sua nova mensagem.    

Se 'edit' � especificado, far� a mesma coisa, mas desde ent�o para antes
de mover para o pr�ximo commit e o levar� para a linha de comando para voc� 
poder corrigir o commit, ou modificar o conte�do do commit de alguma forma.

Se voc� queria dividir um commit, por exemplo, voc� especificaria 'edit' para
esse commit:

	pick   fc62e55 added file_size
	pick   9824bf4 fixed little thing
	edit   21d80a5 added number to log
	pick   76b9da6 added the apply command
	pick   c264051 Revert "added file_size" - not implemented correctly

E ent�o quando voc� for levado para a linha de comando, voc� reverter� aquele 
commit em dois (ou mais) novos. Digamos que o 21d80a5 modificou dois arquivos, 
arquivo1 e arquivo2, e voc� queria dividir eles em commits separados. Voc� 
poderia fazer isso depois que o rebase deix�-lo na linha de comando:

	$ git reset HEAD^
	$ git add file1
	$ git commit 'first part of split commit'
	$ git add file2
	$ git commit 'second part of split commit'
	$ git rebase --continue

E agora ao inv�s dos 5 commits, voc� ter� 6.	

A �ltima coisa �til que o modo interativo do rebase pode fazer � retirar 
commits para voc�. Se ao inv�s de escolher 'pick', 'squash' ou 'edit' para a
linha do commit, voc� simplesmente remove a linha e isso remover� o commit do 
hist�rico.