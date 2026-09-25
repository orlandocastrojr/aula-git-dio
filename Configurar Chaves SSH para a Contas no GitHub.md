## Configuração credenciais (chaves SSH) para acessar contas diferentes no Git

Esse erro acontece porque o Git no seu computador está configurado globalmente com as **credenciais (chaves SSH ou Token de Acesso)** de apenas uma das suas contas. Quando você tenta commitar ou buildar na outra conta, o GitHub rejeita o acesso por falta de permissão.

Para resolver isso de forma definitiva e conseguir usar as duas contas no mesmo computador, a melhor solução é configurar **chaves SSH diferentes** para cada conta.

Aqui está o passo a passo resumido do que você precisa fazer:

1. Criar chaves SSH para cada conta

Abra o seu terminal (ou Git Bash) e gere uma chave para cada e-mail (substitua pelos seus e-mails do GitHub):

bash

```
# Chave para a Conta 1 (Pessoal)
ssh-keygen -t ed25519 -C "seu_email_pessoal@example.com" -f ~/.ssh/id_ed25519_pessoal

# Chave para a Conta 2 (Trabalho/Secundária)
ssh-keygen -t ed25519 -C "seu_email_trabalho@example.com" -f ~/.ssh/id_ed25519_trabalho
```

Use o código com cuidado.

*(Quando o terminal pedir uma "passphrase", você pode apenas apertar Enter para deixar em branco).*

2. Adicionar as chaves nas suas contas do GitHub
- Copie o conteúdo de uma das chaves (ex: `cat ~/.ssh/id_ed25519_pessoal.pub`).

- Vá no GitHub da respectiva conta -> **Settings** -> **SSH and GPG keys** -> **New SSH Key**.

- Cole o conteúdo e salve. Repita o processo com a outra chave na outra conta.
3. Criar um arquivo de configuração SSH

Agora você precisa dizer ao Git quando usar cada chave. Crie ou edite o arquivo `config` dentro da pasta `~/.ssh/`:

bash

```
nano ~/.ssh/config
```

Use o código com cuidado.

Cole a seguinte estrutura dentro dele:

text

```
# Conta Pessoal (Padrão)Host github.com-pessoal    HostName github.com    User git    IdentityFile ~/.ssh/id_ed25519_pessoal# Conta de TrabalhoHost github.com-trabalho    HostName github.com    User git    IdentityFile ~/.ssh/id_ed25519_trabalho
```

Use o código com cuidado.

*(Para salvar no nano, aperte `Ctrl + O`, `Enter` e depois `Ctrl + X`).*

4. Clonar ou atualizar os repositórios

A partir de agora, ao clonar um repositório, você mudará levemente a URL para indicar qual conta quer usar.

- **Para clonar um repositório da conta de trabalho:**
  
  bash
  
  ```
  git clone git@github.com-trabalho:usuario_trabalho/nome-do-repositorio.git
  ```
  
  Use o código com cuidado.

- **Se o repositório já está no seu PC**, mude a URL dele usando o comando:
  
  bash
  
  ```
  git remote set-url origin git@github.com-trabalho:usuario_trabalho/nome-do-repositorio.git
  ```
  
  Use o código com cuidado.
5. Ajustar o nome e e-mail por repositório

Para garantir que os commits fiquem com o nome e e-mail certos em cada projeto, entre na pasta do repositório da sua conta secundária e configure o e-mail localmente (sem o `--global`):

bash

```
git config user.name "Seu Nome Trabalho"
git config user.email "seu_email_trabalho@example.com"
```

Use o código com cuidado.

Você prefere seguir essa configuração usando **chaves SSH** ou gostaria de saber como resolver isso usando o **GitHub Desktop / Gerenciador de Credenciais do Windows** se não quiser mexer no terminal?

Se você prefere evitar o terminal e as chaves SSH, o processo fica muito mais visual. Abaixo estão as duas principais alternativas para gerenciar suas duas contas.

---

Opção 1: Usando o GitHub Desktop (Mais Fácil)

O aplicativo oficial do **GitHub Desktop** permite clonar, fazer commits e dar push alternando entre contas de forma nativa e rápida.

1. **Baixe e instale** o GitHub Desktop (caso ainda não tenha).
2. Abra o aplicativo e vá em **File** (Arquivo) > **Options** (Opções) > **Accounts** (Contas).
3. Faça login com a sua **Conta 1**.
4. Para usar a **Conta 2**, você só precisa clicar em **Sign Out** da primeira e fazer o **Sign In** na segunda. O aplicativo lembra os repositórios de cada uma, exigindo apenas que você troque o login de acordo com o projeto que está mexendo.

Configurando o nome e e-mail corretos no app:

Para que seus commits não fiquem com a assinatura da conta errada:

1. Abra o repositório desejado no GitHub Desktop.
2. Vá em **Repository** (Repositório) > **Repository Settings** (Configurações do Repositório).
3. Na aba **Options**, você pode definir o nome e o e-mail específicos que serão usados **apenas para aquele projeto**, ignorando a configuração global do seu computador.

---

Opção 2: Gerenciador de Credenciais do Windows (Git Credential Manager)

Se você usa o **VS Code**, o **Git Bash** clássico ou outras IDEs, o Windows guarda a sua senha/token do GitHub de forma oculta. Quando você tenta usar a segunda conta, ele tenta enviar a senha salva da primeira.

Para limpar ou alternar essas credenciais manualmente:

1. No menu Iniciar do Windows, pesquise por **Gerenciador de Credenciais** (Credential Manager) e abra-o.
2. Clique em **Credenciais do Windows**.
3. Procure na lista por qualquer item que comece com `git:https://github.com`.
4. Clique na seta ao lado dele e depois em **Remover** (Remove).
5. **O que vai acontecer agora?** Na próxima vez que você tentar dar um `git push` ou `git clone` pelo terminal ou pelo VS Code, o Windows abrirá uma janela pop-up do GitHub perguntando os dados de acesso. Basta logar com a conta correspondente àquele projeto.

---

Tabela Comparativa: Qual escolher?

| Método                     | Vantagem                                                                       | Desvantagem                                                                              |
| -------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| **GitHub Desktop**         | Interface 100% visual, sem códigos. Troca de e-mail por projeto muito simples. | Requer deslogar e logar para mudar de conta no painel.                                   |
| **Gerenciador do Windows** | Ideal para quem usa o VS Code ou quer automatizar o login via pop-up.          | Você precisa "apagar" a credencial antiga sempre que o Windows insistir na conta errada. |

Qual dessas duas ferramentas você utiliza mais no seu dia a dia (**VS Code** ou **GitHub Desktop**)? Assim posso te guiar no passo a passo exato para o seu fluxo.
