## AI Service > OCR > Document AI > コンソール使用ガイド

コンソールに画像ファイルをアップロードし、文書の種類と質問を入力して回答を得ることができます。

## Document AI分析

### 分析のための文書タイプ選択

分析する画像の文書タイプを選択します。

* 選択しない(一般)
* 事業者登録証
* 名刺

### 分析のための画像アップロード

分析する画像をアップロードします。
画像は次の2つの方法でアップロードできます。
1. **画像アップロード**クリック
2. 画像をドラッグ＆ドロップ

### 質問の入力

質問を入力します。

### 分析

**分析**をクリックすると、分析結果が画面右側に表示されます。

![General OCR Image](http://static.toastoven.net/prod_ocr/DocumentAI_console_ko.png)

* **テキスト**：分析結果を表示します。
* **JSON**：分析結果をJSONコード形式で表示します。
    * **llmResponse**: LLM分析の回答
* **コピー**、**ダウンロード**：分析結果のコピー及びダウンロード(Text, JSON)機能を提供します。 
* JSON分析結果例
```json
{
  "llmResponse": "この文書は、意味のないテキストである'ローレンipsum'を使用して、文字はあるが読みにくい、可読性が落ちる文章を作成したようです。"
}
```

### 初期化

**初期化**をクリックすると、入力された画像、質問、回答結果がすべて初期化されます。
