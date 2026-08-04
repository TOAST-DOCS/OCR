## AI Service > OCR > Document AI > リリースノート

### 2026. 08. 11.

- APIエンドポイントドメイン変更
  - 新規エンドポイント`https://api-ocr.nhncloudservice.com`が追加されました。
  - 既存エンドポイント`https://ocr.api.nhncloudservice.com`は2027年7月31日までサポートされた後、サポートが終了します。
  - 新規エンドポイントへ切り替えてください。詳細は[APIガイド](./document-ai-api-guide-v1.1.md)を参照してください。
- リクエストファイル最大容量拡大
  - リクエストファイルの最大容量が5MBから20MBに拡大されました。

### 2026. 03. 10.

- API v1.1リリース
  - User Access Keyトークン認証を使用するAPIが追加されました。
  - User Access Keyトークンの発行及び使用に関する詳細は、[User Access Keyトークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。

### 2024. 11. 12.

* Document AIサービスリリース
    * OCRを通じて画像から文字を抽出し、抽出した情報を基にLLMモデルと連動して内容の要約、情報抽出などの質疑応答を提供するサービスです。
