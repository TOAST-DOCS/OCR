## AI Service > OCR > Overview

OCR provides a feature to recognize the text area of images and documents and extract the text for each area. 
It can be used by customers who need to create a database for recognized documents or implement document processing automation.

## General OCR

### Main Features

* **Recognition of text areas in image**
    * Recognizes the text areas (bounding boxes) in an image and provides the coordinates of the areas.
* **Confidence**
    * Detects text in the image and provides a confidence for it.
* **Analysis results download**
    * You can download the results extracted from an image file as a Text or JSON file.

### Input Image Guide

For more accurate image analysis, please refer to the guide below.

* File/image URL recommendations
    * File format: Supports analysis of images in .jpeg, .png format.
    * Maximum size: 5 MB for file content, 20 MB for image URL content
    * Recommended resolution: 1280x720
    * If you are analyzing a long image, you can use the ‘Segmentation Recognition feature’ to get more accurate analysis results.
        * Long images with a ‘horizontal to vertical’ or ‘vertical to horizontal’ aspect ratio greater than 1:2.5 can cause poor analysis performance.
        * If you need accurate recognition when the aspect ratio exceeds 1:2.5, you can use the ‘Segmentation Recognition feature’ to increase the accuracy of the analysis results.
            * When segmenting and recognizing images, the analysis may include text that is duplicated with some overlapping regions.
        * If the aspect ratio goes beyond about 1:10, analysis is not possible.
* Image recommendation
    * Please use an image taken in a condition where the subject has been laid out as straight as possible on a flat surface.
    * Use a full image with a rectangular shape.
    * It may be difficult to accurately extract the text when the text is unidentifiable due to light reflection or shade caused by camera flash, or the text size is small relative to the resolution.
    * The service supports result analysis for black-and-white and color images, but color images are recommended for accurate analysis.
    * General OCR provides analysis results only for Korean and English.

## Document OCR

### Business Registration Certificate Analysis

#### Main Features

* **Recognition of text areas in a business registration certificate**
    * Recognizes the text areas (bounding boxes) in a business registration certificate and provides the coordinates of the areas.

* **Extraction and analysis of key data in a business registration certificate**
    * Key data according to the classification of the business registration certificate (individual/corporate) is analyzed as a key/value pair, and provides a confidence for it.

* **Analysis results download**
    * You can download the results extracted from a business registration certificate image file as an Excel or JSON file.

#### Input Image Guide

For more accurate business registration analysis, please refer to the guide below.

* File recommendations
    * This service supports analysis of business registration certificate images in .pdf, .jpeg, .png format.
    * Maximum size: 5 MB
    * Recommended resolution: 1280 x 720 or higher
* For PDF, only the analysis results for a single page is provided. (In case of multiple pages, analysis results for the first page is provided.)
* Please use an image taken in a condition where the subject has been laid out as straight as possible on a flat surface.
* Use a full image with a rectangular shape.
* It might be difficult to extract the correct key/value if the text is difficult to read due to light reflection or shadows caused by the camera flash, etc.
* The service supports result analysis for black-and-white and color images, but color images are recommended for accurate analysis.
* The service provides analysis results for the business registration certificate in Korean only.

### Credit Card Analysis

#### Main Features

* **Recognition of text areas in a credit card**
    * Recognizes the text areas (bounding boxes) of card number and expiration date in a credit card image and provides the coordinates of the areas.

* **Extraction and analysis of key data in a credit card**
    * Provides card number and expiration date information in the credit card image, as well as confidence for the information.

* **Analysis results download**
    * You can download the results extracted from a credit card image file as a JSON file.

#### Input Image Guide

For more accurate credit card analysis, please refer to the guide below.

* File recommendations
    * File format: Supports analysis of images in .jpeg, .png format.
    * Maximum size: 5 MB
    * Recommended resolution: 760 x 480
* Please use an image taken in a condition where the subject has been laid out as straight as possible on a flat surface.
* Use a full image with a rectangular shape.
* It might be difficult to extract the correct key/value if the text is difficult to read due to light reflection or shadows caused by the camera flash, etc.
* The service supports result analysis for black-and-white and color images, but color images are recommended for accurate analysis.
* If the card is a vertical card, use an image with the card number and expiration date of the vertical card in the correct orientation for recognition.
* Credit card analysis image example

![Image Example](http://static.toastoven.net/prod_ocr/DocumentRecognizer_ex_img_en.png)

### Analyze ID Card

#### Main Features

* **Recognition of text areas in an ID card**
	* Recognizes the text areas (bounding boxes) in an ID card and provides the coordinates of the areas.

* **Extraction and analysis of key data in an ID card**
    * Key data according to the types of ID cards (resident registration certificate/driver license/passport) is analyzed as a key/value pair, and provides a confidence for it.

* Verify Authenticity
    * Verifies the authenticity of an ID card based on the result extracted from the image file.

* **Analysis results download**
	* You can download the results extracted from an ID card image file as a JSON file.

#### Input Image Guide

For more accurate ID card analysis, please refer to the guide below.

* File recommendations
    * File format: Supports analysis of images in .jpeg, .png format.
    * Maximum size: 5 MB
    * Recommended resolution: 760x480
* Image recommendation
    * Please use an image taken in a condition where the subject has been laid out as straight as possible on a flat surface.
    * Use a full image with a rectangular shape.
    * It might be difficult to extract the correct key/value if the text is difficult to read due to light reflection or shadows caused by the camera flash, etc.
    * The service supports result analysis for black-and-white and color images, but color images are recommended for accurate analysis.
    * The service provides analysis results for ID cards (resident registration certificate/driver license) in Korean only.
        * Passport can be analyzed for domestic and foreign passports, and for foreign passports, analysis results are provided only for MRZ (machine reading area).

## Document AI

### Main Features

* Extracts characters from images through OCR and provides question and answer services such as summarizing the content and extracting information based on the extracted information in conjunction with the LLM model.
* Extracts information in key-value form from images of structured documents such as business licenses, business cards, and more.
* Support for handwriting recognition enables analysis of handwritten images.

### Input Image Guide

For more accurate image analysis, please refer to the guide below.

* File Recommendations
    * File format: Supports analysis of images in .jpeg, .png format.
    * Maximum size: 5 MB
    * Recommended resolution: 1280 x 720 or higher

* Image Recommendations
    * Please use an image taken in a condition where the subject has been laid out as straight as possible on a flat surface.
    * Use a full image with a rectangular shape.
    * It might be difficult to extract text correctly if the text is difficult to read due to light reflection or shadows caused by the camera flash, etc, or if the character size is small relative to the resolution.
    * The service supports result analysis for black-and-white and color images, but color images are recommended for accurate analysis.
    * The text embedded in the image provides analysis results in Korean and English only.

### Cautions for using the service

* Answers generated by Document AI are extracted based on the embedded text within the images you upload.
* Due to the inherent nature of the generative AI (LLM) technology utilized in Document AI, inappropriate or inaccurate answers may be generated. Please double-check your answers to ensure they meet your intent before using them.

## Service Targets
* When you need to register documents (business registration certificate, credit card, and ID card) in the customer's system automatically
* When you need to implement document processing automation
* When you need to build an accounting/financial management automation solution
* when you need to quickly analyze key information from various images and get the information you need in a question-and-answer format,

## Privacy Policy
* While using the OCR service, the customer may collect personal and sensitive information of their users. Therefore, the customer of this service must inform a legal notice to their users as per the Personal Information Protection Act and acquire their consent regarding the matter. Also during this process, work consignment relation regarding the processing of personal information may arise between the customer and NHN Cloud. The customer who assumes the position of consignor may enter into a consignment contract with the consignee, NHN Cloud, separately in writing, and post a privacy policy notice by referencing the following:
    - Consignee: NHN Cloud Corp.
    - Consignment Description: Providing OCR service

## Agreement on technical/administrative level
* The customer must fully implement technical and administrative protection measures considering the sensitive nature of information collected/used while using the OCR service.
* To receive the information recognized by the OCR service, the customer must complete the encryption of the communication section before starting to use the OCR service.
* The original data that the customer requests for recognition to the OCR service must be stored in a secure location and must not be accessible through a URL that can be exposed externally.
* The customer must adopt the recommended transmission method (dedicated line, IPSecVPN, etc.) to provide secure recognition result data from the OCR service.
* The customer must comply with relevant laws such as the Personal Information Protection Act when storing/keeping/managing information recognized by the OCR service.
* The company may request evidence from the customer if it is necessary to verify that the customer prepared all of the technical and administrative measures set out above.
* We ask for the items above from the customer because the information collected/used by the customer through the OCR service is important information. <br>We process information within the scope entrusted as a consignee at the request of the customer, and the customer, as the subject of information processing, guarantees the implementation of the above items and bears all responsibilities for the information subject and regulatory agency arising from violation. 
