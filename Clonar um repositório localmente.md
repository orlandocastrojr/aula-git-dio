# Clonar um repositório localmente

Para clonar o repositório na branch `main` e configurar seu usuário localmente, você deve utilizar o terminal.

O comando para fazer isso é o , seguido pelas configurações locais do Git.

### Passo a Passo

1. Clone o repositório especificando a branch `main`:
   
   ```bash
   git clone -b main https://github.com
   ```

2. Acesse a pasta do repositório que acabou de ser criado:
   
   ```bash
   cd seu-repositorio
   ```

3. Configure seu usuário e e-mail como padrão apenas para este repositório (usando o comando sem a tag `--global`):
   
   ```bash
   git config user.name "Seu Nome"
   git config user.email "seu-email@email.com"
   ```

Se você preferir que esse usuário seja o padrão para todos os repositórios do seu computador, basta adicionar `--global` aos comandos acima (ex: `git config --global user.name "Seu Nome"`).

**Importante:** Mudar o `git config user.name` altera apenas o nome que aparece no histórico de commits, mas **não altera as credenciais de login** que o Windows usa para enviar o código.



## Acessar e autenticar usando chave SSH

Para acessar e autenticar usando a sua chave SSH, você precisa alterar a URL do seu repositório local de HTTPS para SSH e garantir que a sua chave pública esteja cadastrada na conta `orlandocastrojr` do GitHub.

O comando principal para mudar a autenticação do seu repositório para SSH é o `git remote set-url origin git@github.com:orlandocastrojr/M2_Semana_10.git`.

Aqui está o passo a passo para configurar e testar o acesso:

### 1. Alterar a URL do repositório para SSH

No seu terminal atual, execute o comando abaixo para mudar o protocolo de comunicação de HTTPS para SSH:

```bash
git remote set-url origin git@github.com:orlandocastrojr/M2_Semana_10.git
```

### 2. Verificar se a chave SSH está ativa no terminal

Como você está usando o ambiente do Git Bash/UCRT64, certifique-se de que o agente do SSH está rodando e que sua chave privada foi adicionada a ele:

```bash
# Inicia o agente SSH
eval $(ssh-agent -s)

# Adiciona a sua chave privada (altere para id_ed25519_pessoal, se for o caso)
ssh-add ~/.ssh/id_ed25519_estudos

# Isso retornará
Identity added: /c/Users/Dell/.ssh/id_ed25519_estudos (orlando.junior4@faculdadegran.edu.br)
```



### 3. Testar a conexão com o GitHub

Antes de tentar o push, verifique se o GitHub reconhece a sua chave e se ela está vinculada à conta correta:

```bash
ssh -T git@github.com
```

- Se a resposta for: `Hi orlandocastrojr! You've successfully authenticated...`, significa que deu certo.
- Se a resposta ainda mostrar o usuário antigo (`Hi orlandovcj!`), significa que o seu terminal está lendo a chave SSH antiga. Você precisará criar ou ajustar o arquivo `~/.ssh/config` para gerenciar as duas contas.

### 4. Fazer o Push

Se o teste do passo anterior exibiu o nome `orlandocastrojr`, basta rodar o comando final:

```bash
git push
```

O comando de teste retornou a mensagem de sucesso com o usuário orlandocastrojr, ou ele rejeitou a conexão / mostrou o usuário antigo? Se precisar, posso te ajudar a configurar um arquivo de configuração SSH para separar suas duas contas definitivamente.



## Como saber quais chaves SSH existem no Windows

No Windows, por padrão, o Git e o sistema operacional salvam todas as chaves SSH em uma pasta oculta chamada `.ssh`, que fica dentro do diretório do seu usuário do sistema (`C:\Usuários\SeuNome\.ssh`). [1, 2]

Como você já está utilizando o terminal do Git Bash (`UCRT64`), a forma mais fácil de listar suas chaves é diretamente por ele. [3]

### 1. Listar arquivos da pasta `.ssh` no terminal

Execute o seguinte comando para listar todos os arquivos desse diretório: [3]

```bash
ls -al ~/.ssh
```

### Como diferenciar as chaves?

As chaves SSH são geradas sempre em pares (uma privada e uma pública): [4]

- Sem extensão (Chave Privada): Os arquivos que não possuem extensão no nome (ex: `id_ed25519` ou `id_rsa`) são as suas chaves privadas. Elas funcionam como a sua "senha" e nunca devem ser compartilhadas com ninguém. [4]
- Com extensão `.pub` (Chave Pública): Os arquivos terminados em `.pub` (ex: `id_ed25519.pub` ou `id_rsa.pub`) são as suas chaves públicas. São essas que você copia e cola dentro das configurações do GitHub. [3, 5]

---

### 2. Verificar quais chaves estão ativas na memória (no Agente SSH)

Às vezes você tem chaves na pasta, mas o terminal não as carregou. Para ver quais chaves privadas o seu terminal está usando ativamente para tentar se autenticar no momento, use o comando: [6]

```bash
ssh-add -l
```

*(Se retornar "The agent has no identities", significa que nenhuma chave privada foi carregada na memória do terminal ainda).* [6]

---

### O que fazer com essa informação?

Se ao rodar o `ls -al ~/.ssh` você encontrar arquivos de chave: [3]

1. Abra o arquivo público (`.pub`) usando o comando `cat ~/.ssh/id_ed25519.pub` (substitua pelo nome da sua chave).
2. Copie o conteúdo gerado.
3. Vá até o site do GitHub na sua conta nova (`orlandocastrojr`), acesse Settings > SSH and GPG keys > New SSH Key e cole-a lá. [5, 7]

Se a pasta estiver vazia ou disser que o diretório não existe, significa que você não tem nenhuma chave gerada. Se for esse o caso, me avise que te passo o comando para criar uma do zero! [8]

[1] [https://stackoverflow.com](https://stackoverflow.com/questions/72788515/how-to-access-ssh-directory-in-windows)

[2] [https://www.youtube.com](https://www.youtube.com/watch?v=3umFtFyi2Lg)

[3] [https://docs.github.com](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)

[4] [https://www.freecodecamp.org](https://www.freecodecamp.org/portuguese/news/como-obter-e-configurar-suas-chaves-ssh-do-git-e-do-github/)

[5] [https://www.youtube.com](https://www.youtube.com/watch?v=B4p5P3UlD6I)

[6] [https://www.finalmarco.com](https://www.finalmarco.com/github-ssh-keys-setup-on-windows-10/)

[7] [https://medium.com](https://translate.google.com/translate?u=https://medium.com/@chancedev093/managing-multiple-ssh-keys-for-github-and-gitlab-7d77604f8773&hl=pt&sl=en&tl=pt&client=sge)

[8] [https://docs.github.com](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
