# Lab 0 - 開発環境の準備

## Requirement

- Node.js: 8.11.0 以上必須、できれば 10.15.x 以上を推奨します

## Exercise 1: Visual Studio Code の準備

1. 自分のマシンで Visual Studio Code を起動します。もし、バージョンが古い場合はできるだけ最新に更新してください。インストールされていない場合は、 [公式サイト](https://code.visualstudio.com/) からインストールしてください。

1. Visual Studio Code の機能拡張 [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur) を導入します。Vetur を導入することで、 `.vue` ファイルでシンタックスハイライトが有効になります。

## Exercise 2: Vue CLI の導入

1. Vue CLI を導入します。インストール方法の詳細は [Installation | Vue CLI](https://cli.vuejs.org/guide/installation.html) に従ってください。

   ```bash
   npm install -g @vue/cli
   ```

1. 以下のコマンドで Vue CLI が利用できることを確認します。このハンズオンでは、Vue CLI 3.x の利用を前提としています。

   ```bash
   vue --version
   ```

---

[Next](lab01.md)
