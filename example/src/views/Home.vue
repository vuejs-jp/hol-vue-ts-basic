<template>
  <div class="home">
    <h2>Vue.js の基本的な使い方</h2>
    <hr>

    <!-- step1 -->
    <h3>テキストバインディング</h3>
    <p>{{ msg }}</p>

    <!-- step2 -->
    <h3>リストレンダリング</h3>
    <ul id="item-list">
      <li
        v-for="item in items"
        :key="item.id"
      >{{item.name}}</li>
    </ul>

    <!-- step3 -->
    <h3>イベントハンドリング</h3>
    <button v-on:click="onClick">実行</button>

    <!-- step4 -->
    <h3>算出プロパティ</h3>
    <p>{{ computedMsg }}</p>

    <!-- step5 -->
    <h3>条件付きレンダリング</h3>
    <button v-on:click="showDetail">表示</button>
    <div v-if="detail">
      詳細が表示されました。
    </div>

    <h3>クラスとスタイルのバインディング</h3>
    <button v-on:click="raiseError">エラー</button>
    <div v-bind:class="{ 'text-danger': hasError }">
      システムからのメッセージ
    </div>

  </div>
</template>

<script lang="ts">
import Vue from "vue";

// Itemの定義
declare interface Item {
  id: number;
  name: string;
}

// Home画面のビューモデル
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
      ] as Item[],
      detail: false,
      hasError: false
    };
  },
  methods: {
    // イベントハンドラ
    onClick(): void {
      alert(this.msg);
    },
    // 条件付きレンダリングの制御用イベントハンドラ
    showDetail(): void {
      this.detail = true;
    },
    // クラスとスタイルのバインディング制御用イベントハンドラ
    raiseError(): void {
      this.hasError = true;
    }
  },
  // 算出プロパティ
  computed: {
    computedMsg(): string {
      return this.msg.replace(/!/g, "") + " + TypeScript!";
    }
  }
});
</script>

<style scoped>
.home {
  text-align: left;
}

.text-danger {
  color: darkred;
}
</style>
