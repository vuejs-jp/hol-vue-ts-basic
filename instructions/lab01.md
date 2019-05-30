# Lab 1 - プロジェクトの作成

## Exercise 1: Vue CLI でのプロジェクト新規作成

1. ターミナルやコマンドプロンプトで、プロジェクトを作成するディレクトリに移動します。 `˜/src` 以下に作成する場合は以下のように実行します（ディレクトリの場所は任意です）。

    ```bash
    cd ˜/src
    ```

1. Vue CLI でプロジェクトを新規作成します。まず、以下のコマンドを実行します（コマンド実行後はそのまま待機しておいてください）。以下ではプロジェクト名を `vue-lab` としています（プロジェクト名は任意です）。

    ```bash
    vue create vue-lab
    ```

1. 実行後のプロンプト `Please pick a preset` では、以下のように `Manually select features` を選択します。

    ```bash
    ? Please pick a preset:
      default (babel, eslint)
    ❯ Manually select features
    ```

1. 次のプロンプト `Check the features needed for your project` では、以下のよう `TypeScript` と `Router` を選択します。

    ```bash
    ? Check the features needed for your project:
    ◯ Babel
   ❯◉ TypeScript
    ◯ Progressive Web App (PWA) Support
    ◉ Router
    ◯ Vuex
    ◯ CSS Pre-processors
    ◯ Linter / Formatter
    ◯ Unit Testing
    ◯ E2E Testing
    ```

1. **（重要）** 次のプロンプト `Use class-style component syntax?` では、 `n` を選択してください。

    このハンズオンでは、 TypeScript では開発に、クラススタイルではなく、 `Vue.Extend` を使った記法を採用しています。主な理由は、[[Abandoned] Class API proposal: Update: the Class API proposal is being dropped.](https://github.com/vuejs/rfcs/pull/17#issuecomment-494242121) によるためです。

1. 次以降のプロンプトでは以下の設定になるように選択してください。

    ```bash
    ? Use Babel alongside TypeScript for auto-detected polyfills? No
    ? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
    ? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? In dedicated config files
    ? Save this as a preset for future projects? No
    ? Pick the package manager to use when installing dependencies:
     Use Yarn
    ❯ Use NPM
    ```

    Yarn に慣れている方は `Use Yarn` を選択しても構いません（このハンズオンでは、npm を前提に説明を進めますので、適宜読み替えてください）

## Exercise 2: プロジェクトの起動

1. `vue create` の処理が完了したら、カレントディレクトリを Vue CLI で生成したディレクトリに移動し（この例では `vue-lab`）、以下のコマンドを実行してプロジェクトを起動します。

    ```bash
    cd vue-lab
    npm run serve
    ```

1. `npm run serve` の実行が完了したら、ブラウザで `http://localhost:8080/` にアクセスします。

1. ブラウザに 「Welcome to Your Vue.js + TypeScript App」 等と表示されていれば、無事にプロジェクトの作成が成功しています。

`vue create` コマンドの詳細は [Creating a Project \| Vue CLI](https://cli.vuejs.org/guide/creating-a-project.html) を確認してください。

---

[Previous](lab00.md) | [Next](lab02.md)
