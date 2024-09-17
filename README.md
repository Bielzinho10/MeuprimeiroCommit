**GIT**

**Estados**
- Modificado (modified)
- Preparado (encenado/indice)
- Consolidado (comprometido)

**Ajuda**

*Geral*
- `git help`
- Comando especifico: `git help add`, `git help commit`, `git help <qualquer_comando_git>`

*Configuracao*
- Geral: As configuracoes do GIT sao armazenadas no arquivo `.gitconfig` localizado dentro do diretorio do usuario do Sistema Operacional (Ex.: Windows: C:\Users\Documents and Settings\Leonardo ou *nix /home/leonardo).

As configuracoes realizadas por meio dos comandos abaixo serao incluídas no arquivo citado acima.
- Definir usuario: `git config --global user.name "Leonardo Comelli"`
- Definir e-mail: `git config --global user.email leonardo@software-ltda.com.br`
- Editor de Setar: `git config --global core.editor vim`
- Definir ferramenta de mesclagem: `git config --global merge.tool vimdiff`
- Setar arquivos a serem ignorados: `git config --global core.excludesfile ~/.gitignore`
- Listar configuracoes: `git config --list`

*Ignorar Arquivos*
- Os nomes de arquivos/diretorios ou extensoes de arquivos listados no arquivo `.gitignore` nao serao adicionados em um repositorio. Existem dois arquivos `.gitignore`, sao eles:
  - Geral: normalmente armazenado no diretorio do usuario do Sistema Operacional. O arquivo que possui uma lista de arquivos/diretorios a serem ignorados por todos os repositorios devera ser declarado conforme citado acima. O arquivo nao precisa ter o nome de `.gitignore`.
  - Por repositorio: Deve ser armazenado no diretorio do repositorio e deve conter a lista dos arquivos/diretorios que devem ser ignorados apenas para o repositorio especifico.

**Repositório Local**

- Criar novo repositorio: `git init`
- Verifique o estado dos arquivos/diretorios: `git status`

*Adicionar arquivo/diretório (area preparada)*
- Adicionar um arquivo especifico: `git add meu_arquivo.txt`
- Adicionar um diretorio especifico: `git add meu_diretorio`
- Adicionar todos os arquivos/diretorios: `git add .`
- Adicione um arquivo que esta listado no `.gitignore` (geral ou do repositorio): `git add -f arquivo_no_gitignore.txt`

*Comitar arquivo/diretório*
- Comitar um arquivo: `git commit meu_arquivo.txt`
- Comitar varios arquivos: `git commit meu_arquivo.txt meu_outro_arquivo.txt`
- Comitar informando mensagem: `git commit meuarquivo.txt -m "minha mensagem de commit"`

*Remover arquivo/diretório*
- Remover arquivo: `git rm meu_arquivo.txt`
- Remover diretorio: `git rm -r diretorio`

*Visualizar historico*
- Exibir SQLite: `git log`
- Exibir historico com diff das duas ultimas alteracoes: `git log -p -2`
- Exibir resumo do historico (hash completo, autor, data, comentario e qtde de alteracoes (+/-)): `git log --stat`
- Exibir informacoes resumidas em uma linha (hash completo e comentario): `git log --pretty=oneline`
- Exibir historico com formatacao especifica (hash abreviada, autor, dados e comentario): `git log --pretty=format:"%h - %an, %ar : %s"`
  - `%h`: Abreviacao de hash
  - `%an`: Nome do autor
  - `%ar`: Dados
  - `%s`: Comentario
  - Verifique as demais opcoes de formatacao no Git Book

- Exibir historico de um arquivo especifico: `git log -- <caminho_do_arquivo>`
- Exibir historico de um arquivo especifico que contem uma determinada palavra: `git log --summary -S<palavra> [<caminho_do_arquivo>]`
- Exibir historico de alteracao de um arquivo: `git log --diff-filter=M -- <caminho_do_arquivo>`
  - O pode ser substituido por: Adicionado (A), Copiado (C), Apagado (D), Modificado (M), Renomeado (R), entre outros.
- Exibir historico de um autor especifico: `git log --author=usuario`
- Exibir revisao e autor da ultima modificacao de um bloco de linhas: `git blame -L 12,22 meu_arquivo.txt`

**Desfazendo operacoes**

*Desfazendo alteracao local (working directory)*
- Este comando deve ser utilizado enquanto o arquivo nao foi adicionado na staged area.
  - `git checkout -- meu_arquivo.txt`

*Desfazendo alteracao local (staging area)*
- Este comando deve ser utilizado quando o arquivo ja foi adicionado na staged area.
  - `git reset HEAD meu_arquivo.txt`
  - Se o resultado abaixo para as configuracoes, o comando reset nao alterou o diretorio de trabalho.
  - `Unstaged changes after reset: M meu_arquivo.txt`
  - A alteracao do diretorio pode ser realizada atraves do comando abaixo:
    - `git checkout meu_arquivo.txt`

**Repositório Remoto**

- Exibir os repositorios remotos: `git remote`, `git remote -v`
- Vincular Local com um Repositorio Remoto: `git remote add origin git@github.com:leocomelli/curso-git.git`
- Exibir informacoes dos repositorios remotos: `git remote show origin`
- Renomear um repositorio remoto: `git remote rename origin curso-git`
- Desvincular um repositorio remoto: `git remote rm curso-git`
- Enviar arquivos/diretorios para o repositorio remoto: O primeiro push de um repositorio deve conter o nome do repositorio remoto e o branch.
  - `git push -u origin master`
  - Os demais empurram nao precisam dessa informacao: `git push`
- Atualizar repositorio local de acordo com o repositorio remoto
  - Atualizar os arquivos no branch atual: `git pull`
  - Buscar as alteracoes, mas nao se aplica as filiais atuais: `git fetch`
- Clonar um repositorio remoto ja existente: `git clone git@github.com:leocomelli/curso-git.git`

**Etiquetas**

- Criando uma tag leve: `git tag vs-1.1`
- Criando uma tag anotada: `git tag -a vs-1.1 -m "Minha versao 1.1"`
- Criando uma tag assinada: Para criar uma tag assinada e necessaria uma chave privada (GNU Privacy Guard - GPG).
  - `git tag -s vs-1.1 -m "Minha tag assinada 1.1"`
- Criando tag a partir de um commit (hash): `git tag -a vs-1.2 9fceb02`
- Criando tags no repositorio remoto: `git push origin vs-1.2`
- Criando todas as tags locais no repositorio remoto: `git push origin --tags`

**Galhos**

- O master e o branch principal do GIT.
- O HEAD e um ponteiro especial que indica qual e a filial atual. Por padrao, o HEAD aponta para o branch principal, o master.

*Criando um novo branch*
- `git branch bug-123`

*Trocando para uma filial existente*
- `git checkout bug-123`
  - Neste caso, o ponteiro principal HEAD esta apontando para o branch chamado bug-123.

*Criar um novo ramo e trocar*
- `git checkout -b bug-456`

*Voltar para o diretor da filial (mestre)*
- `git checkout master`

*Resolver mesclagem entre os ramos*
- `git merge bug-123`
  - Para realizar o merge, e necessario nao estar no branch que devera receber as alteracoes. A mesclagem pode ser automatica ou manual. A mesclagem automatica sera feita em arquivos que nao sofreram alteracoes nas mesmas linhas, ja o manual de mesclagem sera feito em arquivos de textos que sofreram alteracoes nas mesmas linhas.

  - A mensagem abaixo do manual de mesclagem sera:
    - `Automerging meu_arquivo.txt`
    - `CONFLICT (content): Merge conflict in meu_arquivo.txt`
    - `Automatic merge failed; fix conflicts and then commit the result.`

*Apagando um branch*
- `git branch -d bug-123`

*Listar ramos*
- Listar ramos: `git branch`
- Listar filiais com informacoes dos ultimos commits: `git branch -v`
- Listar ramos que ja foram fundidos (merged) com o master: `git branch --merged`
- Listar ramos que nao foram fundidos (merged) com o master: `git branch --no-merged`

*Criando filiais no repositorio remoto*
- Criando uma filial remota com o mesmo nome: `git push origin bug-123`
- Criando uma agencia remota com nome diferente: `git push origin bug-123:new-branch`
- Baixar um branch remoto para edicao: `git checkout -b bug-123 origin/bug-123`
- Apagar branch remoto: `git push origin:bug-123`