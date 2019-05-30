<template>
  <div class="translator">
    <h2>Translatorの実装</h2>
    <el-row :gutter="40">
      <el-col :span="12">
        <el-form
          ref="form"
          :model="target"
        >
          <el-form-item label="翻訳するテキスト">
            <el-input
              type="textarea"
              rows="8"
              v-model="target.inputText"
              placeholder="翻訳するテキストを入力して下さい"
            />
          </el-form-item>
          <el-form-item>
            <el-button
              type="primary"
              @click="onSubmit"
            >翻訳</el-button>
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

<script lang="ts">
import Vue from "vue";
import axios, { AxiosResponse } from "axios";

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
</script>
