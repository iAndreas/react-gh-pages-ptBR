# Subindo um App React* no GitHub Pages

\* criado usando `create-react-app`

# Introdução
Este tutorial foi traduzido. [Clique aqui para ver a versão original em inglês](https://github.com/gitname/react-gh-pages).
Neste tutorial você vai aprender a criar uma aplicação React e subir ela no GitHub Pages.

Para criar o app React, Vamos utilizar [`create-react-app`](https://create-react-app.dev/), uma ferramenta utilizada para criar aplicações React do zero. Para subir a aplicação utilizaremos o [`gh-pages`](https://github.com/tschaub/gh-pages), um pacote npm feito para subir projetos no [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages), uma hospedagem web gratuita provida pelo GitHub.

Seguindo este tutorial você vai ter uma aplicação React simples hospedada no GitHub Pages — sendo possível customizar conforme sua demanda.

## Traduções

Este tutorial foi traduzido também para as seguintes linguagens:
- [Chinês Tradicional](https://github.com/gitname/react-gh-pages/issues/167#issuecomment-1925551338) (créditos: [@creaper9487](https://github.com/creaper9487))

# Tutorial

## Pré requisitos

1. [Node e npm](https://nodejs.org/en/download/) instalados. As versões utilizadas para fazer o tutorial foram:

    ```shell
    $ node --version
    v16.13.2

    $ npm --version
    8.1.2
    ```
    > Instalando o npm dois comandos são adicionados ao sistema —`npm` e `npx`— ambos serão usados ao decorrer do tutorial.

2. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) instalado. A versão utilizada para fazer o tutorial foi:

    ```shell
    $ git --version
    git version 2.29.1.windows.1
    ```

3. Uma conta no [GitHub](https://github.com/signup). :octocat:

## Procedimento

### 1. Crie um repositório **vazio** no GitHub

1. Entre na sua conta do GitHub.
2. Vá até a pagina [Criar um novo repositório](https://github.com/new).
3. Preencha o formulário da seguinte forma:
    - **Nome do repositório:** Pode botar como quiser\*.

        > \* Para um [site de projeto](https://pages.github.com/#project-site), você pode botar qualquer nome. Para um [site de usuário](https://pages.github.com/#user-site), o GitHub [obriga](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites) que o nome do repositório siga o seguinte formato: `{username}.github.io` (exemplo: `gitname.github.io`)
        
        > O nome que você escolher vai aparecer em alguns lugares: (a) na referência do repositório dentro do GitHub, (b) na URL do repositório e (c) na URL da aplicação.

        > Neste tutorial iremos subir a aplicação React como um site de projeto.

        Para o tutorial escolhemos: `react-gh-pages`
        
   - **Privacidade do repositório:** Selecionar _Public_ (ou _Private_\*).

        > \* Para usuários [GitHub Free](https://docs.github.com/en/get-started/learning-about-github/githubs-products#github-free-for-user-accounts), apenas repositórios _Public_ podem ser usados no Github Pages. Para usuários [GitHub Pro](https://docs.github.com/en/get-started/learning-about-github/githubs-products#github-pro) (e outros usuários pagos), tanto repositórios _Public_ quanto _Private_ podem ser usados no GitHub Pages.

        Para o tutorial escolhemos: _Public_

   - **Inicializar repositório:** Mantenha as checkboxes vazias.

        > Isto vai fazer o GitHub criar um repositório vazio, sem arquivos pré-prontos como `README.md`, `.gitignore`, e/ou `LICENSE`.
4. Clique em criar repositório.

Agora sua conta no GitHub possui um repositório vazio, com o nome e as configurações de privacidade que você especificou.

### 2. Criando um app React

1. Crie uma aplicação react com nome `my-app`:

    > Caso você queira utilizar um nome que não seja `my-app` (exemplo: `web-ui`), lembre-se de substituir todas as ocorrências de nome `my-app` deste tutorial com o nome escolhido (exemplo: `my-app` --> `web-ui`).
  
    ```shell
    $ npx create-react-app my-app
    ```

    > Este comando cria uma aplicação React escrita em JavaScript. Para criar uma escrita em [TypeScript](https://create-react-app.dev/docs/adding-typescript/#installation) você pode utilizar este comando:
    > ```shell
    > $ npx create-react-app my-app --template typescript
    > ```

    Este comando cria uma pasta chamada `my-app`, que vai conter o código fonte do nosso app React.

    > Além de conter o código fonte, esta pasta também será um repositório Git. Veremos mais sobre isso no passo 6.

    > #### Branch names: `master` vs. `main`
    > 
    > O repositório Git vai conter: (a) uma `branch`, nomeada como `master`, que é o padrão para uma instalação nova do Git; ou (b) o valor configurado nas configurações do seu Git, na variável `init.defaultBranch`, se o seu computador está rodando a versão 2.28 do Git ou anterior _e_ você [setou essa variável](https://github.blog/2020-07-27-highlights-from-git-2-28/#introducing-init-defaultbranch) na configuração do seu Git (exemplo: via `$ git config --global init.defaultBranch main`).
    >
    > Como não setei esta variável na minha configuração, a `branch` do meu repositório será `master`. Caso a `branch` do seu repositório tenha um nome diferente (você pode checar com o comando  `$ git branch`), como `main`, por exemplo; você tem que **substituir** todas as ocorrências do nome `master` neste tutorial com o nome da `branch` do seu repositório (exemplo: `master` → `main`).

2. Entrando na pasta nova:
  
    ```shell
    $ cd my-app
    ```

Neste ponto criamos a aplicação React no seu computador e você está na pasta com seu código fonte. Todos os outros comandos mostrados no tutorial deverão ser rodados nesta pasta.

### 3. Instalando o pacote npm `gh-pages`

1. Instale o pacote npm [`gh-pages`](https://github.com/tschaub/gh-pages), designando ele como uma [dependência de desenvolvimento](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file):
 
    ```shell
    $ npm install gh-pages --save-dev
    ```

Agora o pacote `gh-pages` esta instalado no seu computador e sua dependência foi documentada no arquivo `package.json` da sua aplicação React.

### 4. Adicione a propriedade `homepage` no arquivo `package.json`

1. Abra o arquivo `package.json` com um editor de texto (nano, vim...).
   
    ```shell
    $ vi package.json
    ```

    > Neste tutorial o editor de texto utilizado é o [vi](https://www.vim.org/). Mas você pode usar o editor de sua preferência; por exemplo, [Visual Studio Code](https://code.visualstudio.com/).

2. Adicione a propriedade `homepage` neste formato\*: `https://{username}.github.io/{repo-name}`

    > \* Para um [site de projeto](https://pages.github.com/#project-site), este é o formato. Para um [site de usuário](https://pages.github.com/#user-site), o formato é: `https://{username}.github.io`. Você pode ler mais sobre a propriedade `homepage` na [sessão "GitHub Pages"](https://create-react-app.dev/docs/deployment/#github-pages) da documentação do `create-react-app`.

    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://gitname.github.io/react-gh-pages",
      "private": true,
    ```
Agora o arquivo `package.json` contém a propriedade `homepage`.

### 5. Adicionar propriedades de deploy no objeto scripts do arquivo `package.json`

1. Abra o arquivo `package.json` em um editor de texto (caso ainda não esteja aberto).
   
    ```shell
    $ vi package.json
    ```

2. Adicione as propriedades `predeploy` e `deploy` no objeto `scripts`:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```

Agora o arquivo `package.json` possui os scripts necessários para o deploy.

### 6. Adicione a origem remota do seu repositório do GitHub

1. Adicione a "[origem remota](https://git-scm.com/docs/git-remote)" no repositório local.

    Você pode fazer isso adaptando o seguinte comando: 
    
    ```shell
    $ git remote add origin git@github.com:{username}/{repo-name}.git
    ```
    
    Para adaptá-lo, substitua `{username}` pelo seu usuário do GitHub e `{repo-name}` pelo nome do repositório criado no Passo 1.

    Para o tutorial utilizamos:

    ```shell
    $ git remote add origin git@github.com:gitname/react-gh-pages.git
    ```

    > Este comando mostra ao Git onde eu quero que ele envie as coisas sempre que eu — ou o pacote npm `gh-pages` agindo em meu nome — dermos o comando `$ git push` a partir do repositório local.

Agora o repositório local tem uma origem remota apontando para o repositório criado no Passo 1.

### 7. Envie o app React para o repositório no GitHub

1. Para dar o `push` da aplicação para o repositório no GitHub:

    ```shell
    $ npm run deploy
    ```

    > Este comando faz os scripts `predeploy` e `deploy` definidos no `package.json` rodarem.
    >
    > Por debaixo dos panos o script `predeploy` script vai criar uma versão distribuível do app React e armazenar essa versão na pasta `build`. Então, o script `deploy` envia o código desta pasta para um novo commit na `branc`  `gh-pages` do repositório no GitHub, criando esta `branch` caso ela não exista.

    > Por padrão o novo commit na `branch` `gh-pages` terá a mensagem de commit "Updates". Você pode [especificar a mensagem do commit](https://github.com/gitname/react-gh-pages/issues/80#issuecomment-1042449820) pela opção `-m` desta forma:
    > ```shell
    > $ npm run deploy -- -m "Subindo aplicação React para o GitHub Pages"
    > ```

Agora o repositório do GitHub possui uma `branch` com nome de `gh-pages`, que contém os arquivos com a versão distribuível do app React. Falta apenas configurar o GitHub Pages para subir a aplicação.

### 8. Configure o GitHub Pages

1. Acesse a página de configuração do **GitHub Pages**
   1. No seu navegador, acesse o repositório do GitHub
   1. Na parte de cima, clique em "Settings"
   1. No menu lateral, na seção "Code and automation", clique em "Pages"
1. Configure a tela "Build and deployment" desta forma: 
   1. **Source**: Deploy from a branch
   2. **Branch**: 
      - Branch: `gh-pages`
      - Folder: `/ (root)`
1. Clique no botão "Save"

**Está feito!** Sua aplicação React está rodando no GitHub Pages! :rocket:

Agora sua aplicação é acessível para todos que visitarem a URL do `homepage` que você configurou no Passo 4. Por exemplo, a aplicação React deste tutorial está disponível em: https://gitname.github.io/react-gh-pages.

### 9. (Opcional porém recomendado) Guarde o código fonte do app React no GitHub

Nos passos anteriores o pacote npm `gh-pages` fez o `push` da versão distribuível da aplicação para a `branch` nomeada `gh-pages` no repositório do GitHub. Porém, o _código fonte_ da aplicação ainda não está no GitHub.

Neste passo você vai aprender a guardar o código fonte da sua aplicação React no GitHub.

1. Faça o `commit` das alterações que você fez enquanto seguia este tutorial na `branch` `master` em seu repositório local; depois faça o `push` na `branch` `master` do repositório no GitHub.

    ```shell
    $ git add .
    $ git commit -m "Configure React app for deployment to GitHub Pages"
    $ git push origin master
    ```

    > Seu repositório no GitHub agora possui duas `branches`: `master` e `gh-pages`. A `branch` `master` contém o código fonte da aplicação, enquanto a `branch` `gh-pages` contém a versão distribuível do mesmo.

# Notas

- Agradecimento especial ao GitHub (como empresa) por tornar possível a hospedagem gratuita de aplicações por meio do GitHub Pages, e também ao [criador original](https://github.com/gitname) deste tutorial.
