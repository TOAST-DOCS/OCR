## AI Service > OCR > Vehicle Plate OCR > 콘솔 사용 가이드

콘솔을 통해 차량 번호판 이미지를 올리고 분석 결과를 얻을 수 있습니다.

## 차량 번호판 분석


### 분석을 위한 사진 업로드

분석할 차량 번호판 이미지를 업로드합니다.

- 이미지는 다음 2가지 방법으로 업로드할 수 있습니다.
    1. **이미지 업로드** 버튼 클릭
    2. 이미지 드래그 앤드 드롭

### 분석

사진을 업로드한 후 **분석** 버튼을 클릭하면 분석 결과가 화면 오른쪽에 나타납니다.

![Vehicle Plate Registration](http://static.toastoven.net/prod_ocr/VehiclePlateOCR_console_ko.png)

* [텍스트(Key Value)] 분석된 차량 번호판의 내용을 Key/Value 형태로 표시합니다.
* [JSON] 분석한 결과를 JSON 형태로 표시합니다.
    * [success] 분석 성공/실패 여부
    * [fileType] 파일 확장자(jpg, png)
    * [values] 분석 결과
        * [value] 인식한 차량 번호판 내용
        * [conf] 분석 결과에 대한 신뢰도
    * [resolution] 권장 해상도(HD 1280*720px) 이상이면 normal, 권장 해상도 미만은 low
    * [boxes] 인식 영역에 대한 이미지 상의 좌표값(box 별 {x1, y1, x2, y2, x3, y3, x4, y4} 형태)
    
        ![bbox](http://static.toastoven.net/prod_ocr/bbox.png)
    
* 분석 결과 복사 및 다운로드(JSON) 기능을 제공합니다. 