## AI Service > OCR > Vehicle Plate OCR > Console User Guide

You can upload license plate images and get analysis results through the console.

## License Plate Analysis


### Upload an Image for Analysis

Upload a license plate image for analysis.

- Images can be uploaded in the following two methods:
    1. Click the **Upload Image** button
    2. Drag and drop the image

### Analysis

After uploading the image, click the **Analyze** button and the analysis results will appear on the right side of the screen.

![Vehicle Plate Registration](http://static.toastoven.net/prod_carplate_ocr/VehiclePlateOCR_console_en.png)

* [Text (Key Value)] Displays the analyzed license plate contents in Key/Value format.
* [JSON] Displays the analysis results in JSON format.
    * [success] Analysis success/failure
    * [fileType] File extension (jpg, png)
    * [values] Analysis result
        * [value] Recognized license plate content
        * [conf] Confidence score of an analysis result
    * [resolution] normal: the resolution is the recommended resolution (HD 1280*720px) or above, low: the resolution is below the recommended resolution
    * [boxes] Coordinate values of the recognized area on the image ({x1, y1, x2, y2, x3, y3, x4, y4} format for each box)

        ![bbox](http://static.toastoven.net/prod_document_ocr/bbox.png)

* Provides a feature to copy and download (in JSON) analysis results.