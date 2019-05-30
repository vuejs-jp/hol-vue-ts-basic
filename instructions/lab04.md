# Lab 4 - フォームの作成

## Exercise 1: フォーム画面の追加

1. `views` ディレクトリ配下に `Form.vue` ファイルを新規に追加します。この時点ではファイルの中身は何も実装しなくて構いません。

1. フォーム画面に遷移できるように `router.ts` を以下のように編集します。

    ```ts
    // （途中省略）
    // 1. importに以下を追加します
    import Form from './views/Form.vue';

    Vue.use(Router);

    export default new Router({
      mode: 'history',
      base: process.env.BASE_URL,
      routes: [
        // （途中省略）
        // 2. routesに以下を追加します
        {
          path: '/form',
          name: 'form',
          component: Form
        }
      ]
    });
   ```

1. 画面左のメニューにフォーム画面へのリンクが表示されるよう `App.vue` に以下を追加します。

    ```html
    <el-menu-item>
      <router-link to="/form">Form</router-link>
    </el-menu-item>
    ```

## Exercise 2: Element の Form コンポーネント実装

1. フォームで登録されるデータを格納するオブジェクトを TypeScript 側に実装するため、 `Form.vue` を開き、 `<script>` タグを以下のように実装します。

    ```ts
    <script lang="ts">
    import Vue from "vue";

    // RequestFormクラスの定義
    class RequestForm {
      title: string = "";
      type: string = "";
      isProduction: boolean = false;
      desc: string = "";
    }

    // Form画面のビューモデル
    export default Vue.extend({
      data() {
        return {
          request: new RequestForm()
        };
      },
      methods: {
        onSubmit(): void {
          alert("登録しました");
          this.request = new RequestForm();
        }
      }
    });
    </script>
    ```

1. 次に [Element の Form コンポーネント](https://element.eleme.io/#/en-US/component/form) は 以下のように `<template>` タグをマークアップすることで簡単に高機能なフォームを作成することができます。

   ```html
   <template>
     <div class="form">
       <h2>フォームの実装</h2>

       <el-row :gutter="20">
         <el-col :span="12">
           <h3>フォーム</h3>

           <el-form ref="form" :model="request" label-width="120px">
             <el-form-item label="タイトル">
               <el-input v-model="request.title"></el-input>
             </el-form-item>

             <el-form-item label="種別">
               <el-select v-model="request.type" placeholder="選択して下さい">
                 <el-option label="課題" value="issue"></el-option>
                 <el-option label="バックログ" value="backlog"></el-option>
               </el-select>
             </el-form-item>

             <el-form-item label="本番環境">
               <el-switch v-model="request.isProduction"></el-switch>
             </el-form-item>

             <el-form-item label="内容">
               <el-input
                 type="textarea"
                 rows="3"
                 v-model="request.desc"
               ></el-input>
             </el-form-item>

             <el-form-item>
               <el-button type="primary" @click="onSubmit">登録</el-button>
             </el-form-item>
           </el-form>
         </el-col>

         <el-col :span="6" :offset="2">
           <h3>プレビュー</h3>
           <ul>
             <li>タイトル: {{ request.title }}</li>
             <li>種別: {{ request.type }}</li>
             <li>本番環境: {{ request.isProduction }}</li>
             <li>内容: {{ request.desc }}</li>
           </ul>
         </el-col>
       </el-row>
     </div>
   </template>

   <style scoped>
     .form {
       text-align: left;
     }
     .el-form {
       width: 100%;
     }
   </style>
   ```

   ブラウザで `http://localhost:8080/form` を表示し、フォームにデータを入力すると、画面右のプレビュー領域に入力結果がリアルタイムに反映されることが確認できるはずです。これは、テンプレートで Vue.js の `v-model` ディレクティブ がフォーム要素とのデータバインディングを実現しているためです。詳細は、 [フォーム入力バインディング — Vue.js](https://jp.vuejs.org/v2/guide/forms.html) を参照して下さい。

---

[Previous](lab03.md) | [Next](opt01.md)
