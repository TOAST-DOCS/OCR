## AI Service > OCR > Vehicle Plate OCR > コンソール使用ガイド

コンソールを通して車両ナンバープレートの画像をアップロードし、分析結果を得ることができます。

## 車両ナンバープレート分析


### 分析のための写真のアップロード

分析する車両ナンバープレートの画像をアップロードします。

- 画像は次の2つの方法でアップロードできます。
    1. **画像アップロード**ボタンをクリック
    2. 画像をドラッグ＆ドロップ

### 分析

写真をアップロードした後、**分析**ボタンをクリックすると分析結果が画面の右側に表示されます。

![Vehicle Plate Registration](http://static.toastoven.net/prod_ocr/VehiclePlateOCR_console_ja.png)

* [テキスト(Key Value)]分析された車両ナンバープレートの内容をKey/Value形式で表示します。
* [JSON]分析した結果をJSON形式で表示します。
    * [success]分析成功/失敗
    * [fileType]ファイル拡張子(jpg、png)
    * [values]分析結果
        * [value]認識した車両ナンバープレートの内容
        * [conf]分析結果の信頼度
    * [resolution]推奨解像度(HD 1280*720px)以上の場合はnormal、推奨解像度未満はlow
    * [boxes]認識領域の画像上の座標値(box別{x1, y1, x2, y2, x3, y3, x4, y4}の形式)
    
        ![bbox](http://static.toastoven.net/prod_ocr/bbox.png)
    
* 分析結果のコピーおよびダウンロード(JSON)機能を提供します。 
