# Lab 2 - 基本的なレンダリング

## Exercise 1: テキストバインディング

1. トップページを、TypeScript で定義したプロパティをレンダリングするように変更してみます。まず `src/views/Home.vue` を開き、 `<script>` タグ内を以下のように編集します（既存のコードは削除して構いません）。

    ```ts
    <script lang="ts">
    import Vue from "vue";

    export default Vue.extend({
      data() {
        return {
          msg: "Hello Vue.js!"
        };
      }
    });
    </script>
    ```

1. 次にHTML部分となるテンプレートを変更して、 TypeScript で実装した `msg` をレンダリングするように変更します（既存のマークアップは削除して構いません）。

    ```html
    <template>
      <div class="home">
        <h3>テキストバインディング</h3>
        <span>{{ msg }}</span>
      </div>
    </template>
    ```

    ブラウザに「Hello Vue!」と表示されていれば成功です。

1. 次に `Home.vue` のスタイルが左寄せになるように `<style>` タグを追加します。

    ```css
    <style scoped>
    .home {
      text-align: left;
    }
    </style>
    ```

## Exercise 2: リストレンダリング

1. まず、リスト要素の型を定義するインターフェース `Item` を定義しておきます。ここでは、便宜的にインターフェースの定義箇所を Home.vueのscriptタグ内にそのまま追加するようにしています。

    ```ts
    <script lang="ts">
    import Vue from "vue";

    // ここにインターフェースを追加
    declare interface Item {
      id: number;
      name: string;
    }

    // 以下省略
    </script>
    ```

1. scriptタグ内の `data()` 内に、リストを表現する配列 `items` を実装します。

    ```ts
    import Vue from "vue";

    // 途中省略

    export default Vue.extend({
      data() {
        return {
          msg: "Hello Vue.js!",
          items: [
            {
              id: 1,
              name: "キーボード"
            },
            {
              id: 2,
              name: "マウス"
            }
          ] as Item[]
        };
      }
    });
    ```

1. 続けて、TypeScript で実装した `items` をレンダリングするように `<template>` に以下を追加します。

    ```html
    <template>
      <div class="home">
        <!-- 途中省略 -->
        <h3>リストレンダリング</h3>
        <ul id="item-list">
          <li v-for="item in items" :key="item.id">
            {{item.name}}
          </li>
        </ul>
      </div>
    </template>
    ```

    ブラウザに Item のリストが2行表示されていれば成功です。

## Exercise 3: イベントハンドリング

1. クリックイベントに対応するイベントハンドラを `<script>` タグ内にメソッドとして実装します。

    ```ts
    data() {
      // 途中省略
    },
    // ここにメソッドを追加する
    methods: {
      onClick(): void {
        alert(this.msg);
      }
    }
    ```

1. テンプレートには `v-on` を使ったイベントに対応するをボタンを実装します。

    ```html
    <h3>イベントハンドリング</h3>
    <button v-on:click="onClick">実行</button>
    ```

    ボタンをクリックして「Hello Vue!」アラートが表示されれば成功です。

---
[Previous](lab01.md) | [Next](lab03.md)
