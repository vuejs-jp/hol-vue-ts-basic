# Option 2 - さまざまなレンダリング

## Exercise 1: 算出プロパティ

1. 何らかの計算結果をプロパティとして扱うことができる [算出プロパティ](https://jp.vuejs.org/v2/guide/computed.html) を実装します。まず `<script>` タグ内に `computed` オブジェクト内のメソッドとして実装します。ここでは、 `msg` プロパティを拡張して `+ TypeScript!` という文字列を結合されるようにしています。

    ```ts
    // 算出プロパティを実装
    computed: {
      computedMsg(): string {
        return this.msg.replace(/!/g, "") + " + TypeScript!";
      }
    }
    ```

1. テンプレート側には TypeScript の getter として定義したメソッド名を、 `data` 内のプロパティと同じように mustache 記法で記述します。

    ```html
    <h3>算出プロパティ</h3>
    <p>{{ computedMsg }}</p>
    ```

    ブラウザに「Hello Vue + TypeScript!」と表示されていれば成功です。

## Exercise 2: 条件付きレンダリング

1. ブロックを条件に応じて描画したい場合に使用する [条件付きレンダリング](https://jp.vuejs.org/v2/guide/conditional.html) を実装します。まず ビューモデルの `data()` 内に、表示を判定するためのフラグとしてのプロパティ `detail` を定義し、`methods` オブジェクト内に、フラグを `true` にするためのメソッドを追加します。

    ```ts
    data() {
      return {
        // （途中省略）
        // 1. プロパティを追加します
        detail: false
      }
    },
    methods: {
      // （途中省略）
      // 2. 条件付きレンダリングの制御用イベントハンドラを追加します
      showDetail(): void {
        this.detail = true;
      }
    }
    ```

1. テンプレート側には `v-if` ディレクティブを使ったブロックとフラグを `true` にするためのボタンをマークアップします。

    ```html
    <h3>条件付きレンダリング</h3>
    <button v-on:click="showDetail">表示</button>
    <div v-if="detail">
      詳細が表示されました。
    </div>
    ```

    「表示」ボタンをクリックして、「詳細が表示されました。」がレンダリングされれば成功です。

## Exercise 3: クラスとスタイルのバインディング

1. HTMLクラスやインラインスタイルを操作するための [クラスとスタイルのバインディング](https://jp.vuejs.org/v2/guide/class-and-style.html) を実装します。まず、ビューモデルの `data()` 内に、表示を判定するためのフラグとしてのプロパティ `hasError` を定義し、`methods` オブジェクト内に、HTMLクラスを制御するためのメソッドも実装します。

    ```ts
    data() {
      return {
        // （途中省略）
        // 1. プロパティを追加します
        hasError: false
      }
    },
    methods: {
      // （途中省略）
      // 2. クラスとスタイルのバインディング制御用イベントハンドラを追加します
      showDetail(): void {
        this.hasError = true;
      }
    }
    ```

1. テンプレート側には `v-bind:class` ディレクティブに HTMLクラスを制御するオブジェクトをマークアップします。

    ```html
    <button v-on:click="raiseError">エラー</button>
    <div v-bind:class="{ 'text-danger': hasError }">
      システムからのメッセージ
    </div>
    ```

1. HTMLクラスのスタイルが適用された際に、テキストの色が変化するように `<style>` タグ内のCSSを定義します。

    ```css
    .text-danger {
      color: darkred;
    }
    ```

    「エラー」ボタンをクリックすると、「システムからのメッセージ」が赤色のテキストに変化すれば成功です。

---
[Previous](opt01.md)
