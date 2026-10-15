# O Básico do Git

O **Git** é um sistema de controle de versão distribuído (DVCS). Em termos práticos para quem trabalha com dados, relatórios e código, ele funciona como uma "máquina do tempo" com árvore de decisões: registra cada alteração feita nos arquivos, permite navegar entre versões passadas e possibilita que várias pessoas trabalhem no mesmo projeto sem sobrescrever o trabalho umas das outras.

### Entendimento do Conceito: Três Níveis de Profundidade

- **Explicação Simples (O Básico):** Imagine um relatório em Excel ou script Python que antes você salvava como `analise_v1.py`, `analise_final.py`, `analise_final_MESMO.py`. O Git elimina isso. Você mantém um único arquivo `analise.py` e o Git tira "fotos" (snapshots) do projeto a cada marco concluído, com data, autor e descrição do que mudou.

- **Explicação Técnica (Intermediário):** O Git é distribuído porque cada colaborador possui uma cópia integral do histórico no seu próprio computador local (no diretório oculto `.git`). Ele não armazena diferenças linha a linha de forma isolada, mas sim **snapshots** do estado de todos os arquivos. Se um arquivo não mudou, o Git apenas cria um ponteiro para a versão idêntica anterior.

- **Visão Avançada (Arquitetura e Grafos):** Estruturalmente, o Git opera como um **Grafo Acíclico Dirigido (DAG)** de objetos imutáveis identificados por hashes criptográficos SHA-1 (ou SHA-256). Cada commit aponta para uma árvore de diretórios (`tree`), que aponta para arquivos (`blobs`) e para o(s) commit(s) pai(s). Branches são apenas ponteiros móveis leves (arquivos de texto simples de 41 bytes) que apontam para nós desse grafo.

### Os Três Estados do Git Local

Antes de gravar qualquer alteração no histórico, o arquivo passa por três áreas:

1. **Working Directory (Área de Trabalho):** Onde você edita seus arquivos, scripts SQL ou notebooks.

2. **Staging Area / Index (Área de Preparação):** Onde você seleciona exatamente quais arquivos modificados farão parte da próxima "foto".

3. **Local Repository (Repositório Local):** Onde os commits ficam gravados em definitivo no histórico local.

### Passo a Passo: Fluxo de Trabalho Prático

Bash

```
# 1. Inicializa o repositório na pasta do projeto
git init

# 2. Verifica o estado dos arquivos (modificados, não rastreados)
git status

# 3. Move o arquivo da Working Area para a Staging Area
git add script_extracao.py
# (Ou 'git add .' para adicionar todos os arquivos da pasta)

# 4. Grava o snapshot no histórico local com uma mensagem explicativa
git commit -m "feat: adiciona script de extracao de vendas da API"

# 5. Conecta o repositório local a um servidor remoto (ex: GitHub, GitLab)
git remote add origin https://github.com/usuario/projeto-bi.git

# 6. Envia as alterações locais para a branch principal no servidor remoto
git push -u origin main
```

### Conceitos Avançados no Dia a Dia de Dados

- **Branches (Ramificações):** Permitem isolar o desenvolvimento de uma nova análise ou feature sem afetar o código em produção.

  Bash

```
git checkout -b feature/novo-kpi-churn  # Cria e muda para a nova branch
```

- **Merge vs. Rebase:**

- `git merge`: Une duas branches criando um commit de mesclagem explícito, preservando o histórico cronológico exato.

- `git rebase`: Reescreve o histórico, reaplicando seus commits no topo da branch de destino para manter um histórico linear e limpo.

- **Merge Conflicts:** Ocorrem quando duas pessoas alteram a mesma linha do mesmo arquivo. O Git interrompe o processo e exige que você decida manualmente qual versão manter antes de concluir o commit.

- **Stash (`git stash`):** Guarda temporariamente modificações inacabadas da sua área de trabalho para você poder alternar de branch sem precisar commitar código quebrado.

### Erros Comuns (Especiais para Ciência e Análise de Dados)

1. **Subir bases de dados pesadas ou confidenciais:** Arquivos `.csv`, `.parquet`, planilhas de clientes ou credenciais (`.env`) nunca devem ir para o Git. Use um arquivo `.gitignore` na raiz do projeto listando pastas como `data/`, arquivos `.csv` e senhas.

2. **Mensagens de commit genéricas:** Mensagens como "ajustes", "corrigido" ou "update" tornam auditorias de versão inúteis. Prefira padrões como Conventional Commits: `fix: corrige calculo da margem liquida`.

3. **Diferenças em Jupyter Notebooks (`.ipynb`):** Notebooks salvam saídas de células e metadados em JSON complexo, gerando conflitos gigantescos no Git. Boa prática: limpe as saídas das células antes de commitar ou use ferramentas como `jupytext` ou `nbstripout`.

### Como Validar seu Repositório

Para verificar se o seu fluxo está íntegro e acompanhar o histórico:

- Execute `git status` com frequência: garanta que sua árvore de trabalho está limpa (`working tree clean`).

- Execute `git log --oneline --graph --all` para visualizar o grafo das branches e entender a cronologia das entregas.
