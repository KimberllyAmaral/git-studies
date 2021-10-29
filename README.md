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


