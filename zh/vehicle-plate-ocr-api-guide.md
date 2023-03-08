## AI Service > OCR > Vehicle Plate OCR > API Guide

### License Plate Analysis API

#### Request

- You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI |
|---|---|
| POST | https://ocr.api.nhncloudservice.com/v1.0/appkeys/{appKey}/vehicle-plate |

[Request Header]

| Name | Value | Description |
|---|---|---|
| Authorization | {secretKey} | Security key issued from the console |

[Request Body]

- Put binary data of the image file.

```
curl -X POST 'https://ocr.api.nhncloudservice.com/v1.0/appkeys/{appKey}/vehicle-plate' \
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
        "values": [
            {
                "value":"123가4567",
                "conf":0.93
            }
        ],
        "boxes": [
            {
                "x1": 340,
                "y1": 3231,
                "x2": 523,
                "y2": 3231,
                "x3": 523,
                "y3": 3297,
                "x4": 340,
                "y4": 3297
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

| Name | Type | Description |
|---|---|---|
| fileType | String | File extension (jpg, png) |
| values | List | List of recognition results |
| values[0].value | String | Recognized content |
| values[0].conf | Double | Confidence score of the recognition result |
| resolution | String | normal: the resolution is the recommended resolution (HD 1280*720px) or above, low: the resolution is below the recommended resolution |
| boxes | List | List of bounding box coordinates |
| boxes[0] | Object  | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 } |

* boxes[0]

    ![Bounding box](http://static.toastoven.net/prod_document_ocr/bbox.png)

