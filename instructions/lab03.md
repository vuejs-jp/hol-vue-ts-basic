# Lab 3 - テーブルの作成

## Exercise 1: Element の導入

1. Vue.js で利用できる UI ライブラリとして提供されている [Element](https://element.eleme.io/) を導入します。Element は Vue CLI のプラグインとしてインストールすることができますので、以下のコマンドを実行します。

   ```bash
   vue add element
   ```

1. CLI のプロンプトでは以下のように設定します。

   ```bash
   ? How do you want to import Element? : Fully import
   ? Do you wish to overwrite Element's SCSS variables? : No
   ? Choose the locale you want to load: ja
   ```

1. Element のインストール後、全体のレイアウトを調整するために `App.vue` を以下のように書き換えて下さい。( `<script>` タグは不要です)

   ```html
   <template>
     <div id="app">
       <el-container>
         <el-aside>
           <el-menu id="nav">
             <el-menu-item>
               <router-link to="/">Home</router-link>
             </el-menu-item>
             <el-menu-item>
               <router-link to="/about">About</router-link>
             </el-menu-item>
           </el-menu>
         </el-aside>
         <el-main>
           <router-view />
         </el-main>
       </el-container>
     </div>
   </template>

   <style>
     #app {
       font-family: 'Avenir', Helvetica, Arial, sans-serif;
       -webkit-font-smoothing: antialiased;
       -moz-osx-font-smoothing: grayscale;
       text-align: center;
       color: #2c3e50;
       margin-top: 60px;
     }
   </style>
   ```

## Exercise 2: テーブル画面の追加

1. `views` ディレクトリ配下に `Table.vue` ファイルを新規に追加します。この時点ではファイルの中身は何も実装しなくて構いません。

1. 次に、 [Vue Router](https://router.vuejs.org/ja/) の機能を使って、テーブル画面に遷移できるように `router.ts` を以下のように編集します。

   ```ts
   // （途中省略）
   // 1. importに以下を追加します
   import Table from './views/Table.vue';

   Vue.use(Router);

   export default new Router({
     mode: 'history',
     base: process.env.BASE_URL,
     routes: [
       // （途中省略）
       // 2. routesに以下を追加します
       {
         path: '/table',
         name: 'table',
         component: Table
       }
     ]
   });
   ```

1. 画面左のメニューにテーブル画面へのリンクが表示されるよう `App.vue` に以下を追加します。

   ```html
   <el-menu-item>
     <router-link to="/table">Table</router-link>
   </el-menu-item>
   ```

   この時点では、コンソールに `[Vue warn]: Failed to mount component: template or render function not defined.` の警告が出ますがそのまま進めます。

## Exercise 3: Element の Table コンポーネント を使ったテーブルの実装

1. テーブルのデータとなるオブジェクトを TypeScript 側に実装するため、 `Table.vue` を開き、 `<script>` タグを以下のように実装します。

   ```ts
   <script lang="ts">
   import Vue from "vue";

   // NoteBook型の定義
   declare interface NoteBook {
     id: number;
     brand: string;
     name: string;
     isUsed: boolean;
   }

   // Table画面のビューモデル
   export default Vue.extend({
     data() {
       return {
         noteBooks: [
           {
             id: 1001,
             brand: "Microsoft",
             name: "Surface Go",
             isUsed: false
           },
           {
             id: 1002,
             brand: "Apple",
             name: "MacBook Air",
             isUsed: true
           }
         ] as NoteBook[]
       };
     }
   });
   </script>
   ```

1. 次に [Element の Table コンポーネント](https://element.eleme.io/#/en-US/component/table) は 以下のように `<template>` タグをマークアップすることで簡単に高機能なテーブルを作成することができます。

   ```html
   <template>
     <div class="table">
       <el-table
         :data="noteBooks"
         :default-sort="{prop: 'id', order: 'ascending'}"
       >
         <el-table-column prop="id" label="ID" sortable> </el-table-column>
         <el-table-column prop="brand" label="メーカー"> </el-table-column>
         <el-table-column prop="name" label="機種名"> </el-table-column>
         <el-table-column prop="isUsed" label="利用中">
           <template slot-scope="scope">
             <i class="el-icon-check" v-if="scope.row.isUsed"></i>
           </template>
         </el-table-column>
       </el-table>
     </div>
   </template>

   <style scoped>
     .table {
       text-align: left;
     }
   </style>
   ```

   ブラウザで `http://localhost:8080/table` を表示し、ソート機能付きのテーブルがレンダリングされていれば成功です。

---

[Previous](lab02.md) | [Next](lab04.md)
