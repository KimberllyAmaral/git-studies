# Estudos Sobre Git
Git é uma ferramenta usada por desenvolvedores para gerenciar o controle das versões de suas aplicações.
#### Commits capturam o estado do seu código no momento
* git commit
#### Uma branch é uma ramificação do seu projeto
* git branch [nome da nova branch]
#### Para mudar de branch 
* git checkout [nome da branch para a qual você deseja mudar]
#### Juntar a branch atual com outra branch
* git merge [nome da branch que você deseja juntar]
#### Juntar a branch para a qual você deseja ir para a branch principal
* git checkout [branch para qual você deseja ir]; git merge [nome da branch principal]
#### O rebase deixa a sequencia de commits linear, pega os commits de um lugar, copia e cola em outro...
Neste comando o commit continua existindo no local de origem, ele só estará visível de forma linear na branch que você escolheu.
* git rebase [nome da branch onde você deseja colocar os commits]
### HEAD é um nome simbólico para o commit atualmente ativo (que sofreu checkout por último)
> Soltar o HEAD significa anexá-lo a um commit em vez de anexá-lo a um ramo. Antes do estado solto ("detached"), é assim como se parece:
* git checkout [nome do head]

### Hashes
> você terá de usar o comando **git log** para ver os hashes. O git exige que você especifique a quantidade de caracteres do hash suficiente para identificar unicamente o commit.
#### HEAD^ permite andar pela arvore de commits
* git checkout HEAD^ 
#### O comando HEAD^ pode ser cansativo, por isso use o operador ~ para andar entre um número maior de commits
* git HEAD~[número de commits]
* git HEAD~4
> Para trocar ramos de lugar, você pode redefinir diretamente o commit para o qual um ramo aponta com a opção -f <

Exemplo: Move (à força) o ramo main 3 ancestrais acima do HEAD.
* git branch -f main HEAD~3

#### Revertendo mudanças no git
> O comando git reset reverte mudanças movendo para trás no tempo (para um commit mais antigo) a referência do ramo. O git reset vai mover o ramo para trás como se o commit nunca tivesse existido.
* git reset HEAD~1
> git reset funciona bem somente em branches locais
#### Compartilhar mudanças
> Para reverter mudanças e conseguir compartilhar essas mudanças com os outros, precisamos usar o git revert
* git revert
#### Copiando uma série de commits
* git cherry-pick [nome dos commits]
* git cherry-pick c1 c2
#### Rebase interativo
> Mostrar quais commits estão prestes a serem copiados abaixo do alvo do rebase. Ele também mostra os hashes e as mensagens dos commits, o que é ótimo para ter noção do que é o que.
* git rebase -i HEAD~3
(Rebasing 3 commits)
> Dessa forma o git copia alguns commits exatamente da mesma forma que você os especificou.

## Comandos git mais usados
#### Criando uma nova branch com o git checkout
* git checkout -b <nome-da-branch> master

#### Atualizar e sobrescrever mudanças
* git pull
Caso você receba este seguinte erro:
> -> commit-test git:(master) $ git pull
> Updating db40e41..2958dc6
> error: Your local changes to the following files would be overwritten by merge:
>       README.md
> hint:  Please, commit your changes before merging.
> fatal: Exiting because of unfinished merge.
Utilize a seguinte sequência de comandos para sobrescrever as mudanças:
* git stash
* git pull
O git stash grava o estado atual do diretário durante um determinado período. Se você quiser recuperar as suas alterações, você pode usar o apply.
* git stash apply

#### Removendo arquivos não rastreados
> Quando você tiver arquivos e diretórios desnecessários na sua cópia local do repositório, e você quiser deletar esses asquivos ao invés de só usar o ignore (.gitignore), você pode usar o git clean para remover todos os arquivos que não estão rastreados pelo git.
1. Comece com um dry-run para ver o que vai ser deletado
  * git clean -n -d
2. Depois que tiver certeza, rode o comando git clean com a flag -f
  * git clean -f -d

#### Git unstage
Quando você estiver adicionando arquivos com o git add na sua árvore de trabalho no git, você esta adicionando os asquivos na área stage. Se você quiser parar de rastrear aquivos específicos da sua árvore de trabalho, você precisa removê-los dos seus arquivos em stage.
> Removendo arquivos do stage no index
Com este comando você mantém o arquivo mas remove ele do index
* git rm --cached <nome-do-arquivo>
> -> commit-test git:(master) $ git rm –cached unstageMe.js
rm unstageMe.js
Para remover todos os arquivos do stage:
* git reset

#### Desfazendo um Merge
Desfaça o merge mantendo o histórico de commits:
1. De checkout na branch master 
* git checkout master
2. Rode o git log e tenho o id do commit no merge
* git log --oneline
> commit-test git:(master) $ log –oneline
812d761 Merge pull request #524 from datreeio/DAT-1332-resolve-installation-id
b06dee0 feat: added installation event support
8471b2b fix: get organization details from repository object
3. Reverta o merge com o id do commit
* git revert -m 1 <merge-commit-id>
> commit-test git:(master) $ revert -m 1 812d761
Revert “Merge pull request #524 from datreeio/DAT-1332-resolve-installation-id”
[master 75b85db] Revert “Merge pull request #524 from datreeio/DAT-1332-resolve-installation-id”
1 file changed, 1 deletion(-)
4. Faça um commit do revert e faça o push para o repositório remoto.
> commit-test git:(master) $ git commit -m "revert merge #524"
  
> commit-test git:(master) $ git push

#### Removendo arquivos de um commit remoto
1. Remova os arquivos:
* git rm <file-A> <file-B> <file-C>`
2. Faça um commit das alterações:
* git commit -m "removing files"`
3. Faça o push das suas mudanças
* git push

#### Desfazendo um commit
- Mantendo as mudanças do commit que você deseja desfazer:
* git reset --soft HEAD^
- Destruindo as mudanças do commit que você deseja desfazer:
* git reset --hard HEAD^

#### Comparando diferenças entre branches
* git diff branch1..branch2
Compara arquivos entre as branches
* git diff branch1:file branch2:file

#### Renomeando uma branch após criá-la
1. De o checkout na branch que você precisa renomear
* git checkout <nome-antigo-da-branch>
2. Use este comendo para renomear o nome da branch localmente
* git branch -m <novo-nome>
3. Delete a branch antiga remotamente
* git push origin :<nome-antigo> <nome-novo>
4. Resete a upstream branch para o nome da nova branch
* git push origin -u <nova-branch>
  
