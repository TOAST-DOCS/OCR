## AI Service > OCR > Document AI > Console User Guide

You can upload an image file to the console, enter a document type and a question to get answers.

## Document AI Analysis

### Select document types for analysis

Select the document type of the image you want to analyze.

* Not selected (General)
* Business registration certificate
* Business card

### Upload an Image for Analysis

Upload an image to analyze.<br>
Images can be uploaded in the following two methods:
1. Click **Upload Image**
2. Drag and drop the image

### Enter a Question

Enter a question.

### Analysis

When you click **Analysis**, the results of your analysis appear on the right side of the screen.

![General OCR Image](http://static.toastoven.net/prod_ocr/DocumentAI_console_ko.png)

* **Text**: Displays the results of the analysis.
* **JSON**: Displays the results of your analysis in JSON code format.
    * **llmResponse**: LLM Analysis Response
* **Copy**, **Download**: Provides the feature to copy and download analytics results (Text, JSON). 
* JSON Analysis Results
```json
{
  "llmResponse": "It appears that this document uses 'loren ipsum', which is meaningless text, to create a sentence that has letters but is difficult and illegible to read."
}
```

### Initialize

Click **Reset** to reset any images, questions, and answers you entered.
