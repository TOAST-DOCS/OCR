## AI Service > OCR > General OCR > API Guide


### General OCR API

#### Request

- You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI                                                               |
|---|-------------------------------------------------------------------|
| POST | https://ocr.api.nhncloudservice.com/v1.0/appkeys/{appKey}/general |

[Request Header]

| Name | Value | Description |
|---|---|---|
| Authorization | {secretKey} | Security key issued from the console |

[Request Body]

- Put binary data of the image file.

```
curl -X POST 'https://ocr.api.nhncloudservice.com/v1.0/appkeys/{appKey}/general' \
-F 'image=@sample.png' \
-H 'Authorization: ${secretKey}'
```

[Field]

| Name | Type | Description |
|---|---|---|
| image | multipart/form-data | Image file |

#### Response

[Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "fileType": "png",
        "listOfInferTextList": [
            {
                "value":"stella",
                "conf":0.99
            },
            {
                "value":"artois",
                "conf":0.98
            },
            {
                "value":"belgium"
                "conf":0.98
            }
        ],
        "listOfBoundingBoxList": [
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
        ],
        "resolution": "normal"
    }
}
```

[Header]

| Name | Type | Description |
|---|---|---|
| isSuccessful | Boolean | Analysis API success or not |
| resultCode | Integer | Result code |
| resultMessage | String | Result message (success on success, error content on failure) |

[Field]

| Name | Type | Description                                                |
|---|---|---------------------------------------------------|
| fileType | String | File extension (jpg, png)                                  |
| values | List | List of recognition results                                          |
| listOfInferTextList[0].value | String | Recognized content                                             |
| listOfInferTextList[0].conf | Double | Confidence score of the recognition result                                         |
| listOfBoundingBoxList | List | List of bounding box coordinates                         |
| listOfBoundingBoxList[0] | Object  | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 }       |
| resolution | String | normal: the resolution is the recommended resolution (HD 1280\*720px) or above, low: the resolution is below the recommended resolution |

* boxes[0]

  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)

