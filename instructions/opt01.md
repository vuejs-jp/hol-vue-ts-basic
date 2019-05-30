# Option 1 - API の接続

## Exercise 1: axios の導入

1. Vue.js のウェブアプリケーションで API からデータを取得するにはいくつかの方法がありますが、ここでは一般的な [axios](https://github.com/axios/axios) を導入していきます。axios は Vue CLI のプラグインとしてインストールすることができますので、以下のコマンドを実行します。

    ```bash
    vue add axios
    ```

1. axios のインストール後、プラグインの実行によって以下のファイルが追加、変更になっていることを確認して下さい。ここでは、特にコードの変更は不要です。

- `src/main.ts`: Vue インスタンスに axios を読み込む処理を追加
- `src/plugins/axios.js` : axios の各種設定と Vue にプラグインとして組み込むための処理を新規追加

## Exercise 2: Translator 画面の追加

1. API を利用する画面として、 `views` ディレクトリ配下に `Translator.vue` ファイルを新規に追加します。この時点ではファイルの中身は何も実装しなくて構いません。

1. フォーム画面に遷移できるように `router.ts` を以下のように編集します。

    ```ts
    // （途中省略）
    // 1. importに以下を追加します
    import Translator from './views/Translator.vue';

    Vue.use(Router);

    export default new Router({
      mode: 'history',
      base: process.env.BASE_URL,
      routes: [
        // （途中省略）
        // 2. routesに以下を追加します
        {
          path: '/translator',
          name: 'translator',
          component: Translator
        }
      ]
    });
    ```

1. 画面左のメニューにフォーム画面へのリンクが表示されるよう `App.vue` に以下を追加します。

    ```html
    <el-menu-item>
      <router-link to="/translator">Translator</router-link>
    </el-menu-item>
    ```

## Exercise 3: API を使ったフォームの実装

1. フォームに入力したデータを API に送信して結果を取得する処理を TypeScript 側に実装するため、 `Translator.vue` を開き、 `<script>` タグを以下のように実装します。なお、APIのプレフィックス `{YOUR-PREFIX}` はダミーテキストです。実際にAPIにアクセスするためには、ハンズオンスタッフに確認して、有効な文字列に置き換えて下さい。

    ```ts
    <script lang="ts">
    import Vue from "vue";
    import axios, { AxiosResponse } from "axios";

    // API 実行結果
    class TranslatorResult {
      detectedLanguage: string = "";
      translatedText: string = "";
      translatedLanguage: string = "";
    }

    // フォームデータ
    class TranslatorForm {
      inputText: string = "";
      translatorResult: TranslatorResult = new TranslatorResult();
    }

    // ビューモデル
    export default Vue.extend({
      data() {
        return {
          target: new TranslatorForm(),
          apiPrefix: "{YOUR-PREFIX}"
        };
      },
      methods: {
        // 翻訳ボタンクリック時のイベントハンドラ
        async onSubmit() {
          if (this.target.inputText) {
            const translatorResult = await this.invokeTranslator(
              this.target.inputText
            );
            this.target.translatorResult = translatorResult;
          }
        },
        // Azure Text Translator APIの実行
        async invokeTranslator(text: string): Promise<TranslatorResult> {
          const res: AxiosResponse = await axios.post(
            "https://" + this.apiPrefix + "-vue.azurewebsites.net/api/translate",
            {
              target: text
            }
          );
          return res.data;
        }
      }
    });
    </script>
    ```

1. 次に `<template>` タグを以下のようにマークアップし、テキストを入力して API を実行すると、翻訳結果が表示されるようなフォームを完成させます。

    ```html
    <template>
      <div class="translator">
        <h2>Translatorの実装</h2>
        <el-row :gutter="40">
          <el-col :span="12">
            <el-form ref="form" :model="target">
              <el-form-item label="翻訳するテキスト">
                <el-input
                  type="textarea"
                  rows="8"
                  v-model="target.inputText"
                  placeholder="翻訳するテキストを入力して下さい"
                />
              </el-form-item>
              <el-form-item>
                <el-button type="primary" @click="onSubmit">翻訳</el-button>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="12">
            <span>翻訳結果</span>
            <ul>
              <li>入力された言語: {{ target.translatorResult.detectedLanguage }}</li>
              <li>翻訳された言語: {{ target.translatorResult.translatedLanguage }}</li>
              <li>翻訳結果:
                <div>
                  {{ target.translatorResult.translatedText }}
                </div>
              </li>
            </ul>
          </el-col>
        </el-row>
      </div>
    </template>

    <style scoped>
    .translator {
      text-align: left;
    }
    </style>
    ```

    ブラウザで `http://localhost:8080/form` を表示し、フォームにデータを入力してボタンをクリックすると、画面右のプレビュー領域に翻訳結果が表示されることが確認できるはずです。なお、ここで呼んでいる翻訳APIは、 Microsoft Azure の [Translator Text API](https://azure.microsoft.com/ja-jp/services/cognitive-services/translator-text-api/) を利用しています。

---

[Previous](lab04.md) | [Next](opt02.md)
