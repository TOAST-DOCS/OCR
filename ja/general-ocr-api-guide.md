## AI Service > OCR > General OCR > APIガイド


### General OCR API

#### リクエスト

- {appKey}と{secretKey}はコンソール上部の**URL & Appkey**メニューで確認できます。

[URI]

| メソッド | URI                                                               |
|---|-------------------------------------------------------------------|
| POST | https://ocr.api.nhncloudservice.com/v1.0/appkeys/{appKey}/general |

[リクエストヘッダ]

| 名前 | 値 | 説明 |
|---|---|---|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |

[リクエスト本文]

- 画像ファイルのBinary Dataを入れます。

```
curl -X POST 'https://ocr.api.nhncloudservice.com/v1.0/appkeys/{appKey}/general' \
-F 'image=@sample.png' \
-H 'Authorization: ${secretKey}'
```

[フィールド]

| 名前 | タイプ | 説明 |
|---|---|---|
| image | multipart/form–data | 画像ファイル |

#### レスポンス

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "fileType": "png",
        "listOfInferTexts": [
            {
                "inferTexts": [
                    {
                        "value":"stella",
                        "conf":0.99
                    },
                    {
                        "value":"artois",
                        "conf":0.98
                    },
                ],
                "inferTexts": [
                    {
                        "value":"belgium",
                        "conf":0.99
                    }
                ]
            }
        ],
        "listOfBoundingBoxes": [
            {
                "boundingBoxes": [
                    {
                        "x1": 32,
                        "y1": 23,
                        "x2": 65,
                        "y2": 23,
                        "x3": 65,
                        "y3": 35,
                        "x4": 32,
                        "y4": 35
                    }
                ]
            }
        ],
        "resolution": "normal"
    }
}
```

[ヘッダ]

| 名前 | タイプ | 説明 |
|---|---|---|
| isSuccessful | Boolean | 分析APIの成否 |
| resultCode | Integer | 結果コード |
| resultMessage | String | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]

| 名前                                         | タイプ | 説明                                              |
|--------------------------------------------|---|---------------------------------------------------|
| fileType                                   | String | ファイル拡張子(jpg、png)                                  |
| values                                     | List | 認識結果リスト                                        |
| listOfInferTexts[0].inferTexts[0].value | String | 認識内容                                           |
| listOfInferTexts[0].inferTexts[0].conf  | Double | 認識結果の信頼度                                       |
| listOfBoundingBoxes                        | List | 認識領域(Bounding box)座標リスト                       |
| listOfBoundingBoxes[0].boundingBoxes[0]    | Object  | 認識領域の座標{ x1, y1, x2, y2, x3, y3, x4, y4 }       |
| resolution                                 | String | 推奨解像度(HD 1280*720px)以上の場合はnormal、推奨解像度未満はlow |

* boxes[0]

  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)
