Para subir um projeto local do seu notebook para o GitHub, você deve criar um repositório vazio na plataforma e conectá-lo ao Git no seu terminal. [[1](https://docs.github.com/pt/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github), [2](https://cursos.alura.com.br/forum/topico-duvida-criando-repositorio-remoto-a-partir-do-git-local-360151)]

Passo 1: Criar o repositório no GitHub

1. Acesse o [GitHub](https://github.com/) e faça login na sua conta.
2. Clique no ícone **"+"** no canto superior direito e selecione **"New repository"** (Novo repositório).
3. Dê um nome ao seu repositório (sem espaços ou acentos).
4. Escolha se ele será **Público** ou **Privado**.
5. **Não** marque a opção de adicionar arquivo README, `.gitignore` ou licença (para evitar conflitos com o projeto que já está no seu notebook).
6. Clique no botão verde **"Create repository"**.
7. Na página seguinte, copie a **URL do repositório** (exemplo: `https://github.com`). [[1](https://www.youtube.com/watch?v=07n8FF_hrTM&t=37), [2](https://www.youtube.com/shorts/Q9tRyy6RjwI), [3](https://www.youtube.com/watch?v=s54N3QuLdKc), [4](https://www.youtube.com/watch?v=iR6-3AT1WfE), [5](https://cursos.alura.com.br/forum/topico-duvida-criando-repositorio-remoto-a-partir-do-git-local-360151), [6](https://docs.github.com/pt/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)]

---

Passo 2: Configurar o Git no seu notebook

Abra o terminal (ou Git Bash, no Windows) e siga os comandos abaixo: [[1](https://docs.github.com/pt/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)]

1. **Navegue até a pasta do seu projeto:**
   
   bash
   
   ```
   cd /caminho/para/seu/projeto
   ```
   
   Use o código com cuidado.

2. **Inicialize o repositório Git localmente:**
   
   bash
   
   ```
   git init
   ```
   
   Use o código com cuidado.
   
   *(Isso cria a pasta oculta `.git` no seu projeto)*.

3. **Adicione todos os arquivos do projeto ao controle de versão:**
   
   bash
   
   ```
   git add .
   ```
   
   Use o código com cuidado.

4. **Faça o primeiro commit:**
   
   bash
   
   ```
   git commit -m "Primeiro commit: envio do projeto inicial"
   ```
   
   Use o código com cuidado.

5. **Defina a branch principal como `main`:**
   
   bash
   
   ```
   git branch -M main
   ```
   
   Use o código com cuidado.

6. **Conecte o repositório local ao GitHub (substitua pela URL que você copiou):**
   
   bash
   
   ```
   git remote add origin https://github.com
   ```
   
   Use o código com cuidado.

7. **Envie os arquivos para o GitHub:** [[1](https://www.youtube.com/watch?v=y2bAb8zpEFI&t=24), [2](https://www.dio.me/articles/criar-repositorio-e-versionar-codigo-com-git-e-github-6ee65a344def)]
   
   bash
   
   ```
   git push -u origin main
   ```
   
   Use o código com cuidado.

Pronto! Seus arquivos já estarão disponíveis na sua conta do GitHub. [[1](https://www.youtube.com/watch?v=UvmgcBv9BtQ&t=67), [2](https://docs.github.com/pt/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)]

Veja um passo a passo em vídeo de como criar e conectar o repositório:

Se você encontrou algum **erro no terminal** (como problemas de autenticação ou conflito de branches) ou se quiser ajuda para criar um arquivo **`.gitignore`**, me avise aqui!
