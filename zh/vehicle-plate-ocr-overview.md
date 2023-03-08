## AI Service > OCR > Vehicle Plate OCR > Overview

Vehicle Plate OCR uses optical character recognition (OCR) technology to recognize text areas on a license plate and extract text in each region.
It provides a high level of accuracy for the results of text area recognition and text extraction per area, and provides OCR technology optimized for businesses that require license plate recognition.

## Main Features

* **Recognition of text areas in a license plate**
    * Recognizes the bounding boxes on the rectangular license plate attached to the front and rear of the vehicle.

* Detection of text on a license plate
    * Detects text in the recognized text area and provides a confidence for it.

* **Analysis results download**
    * You can download the results extracted from a license plate file as a JSON file.

## Input Image Guide

For more accurate license plate analysis, please refer to the guide below.

* File recommendations
    * File format: Supports analysis of images in .jpeg, .png format.
    * Maximum size: 5 MB
    * Recommended resolution: 1280 x 720 or higher

* Image recommendations
    * An image where the license plate is facing the front and the bonnet of the car is included is recommended.
    * An environment in which only one vehicle can be photographed in one image is recommended.
        * If there are multiple license plates, the analysis result for one license plate is provided.
    * The analysis result is provided for regular license plates (excluding special purpose vehicles).
    * The recognition rate may decrease if there is a strong light reflection from the camera flash.
    * If the license plate is damaged or it is difficult to recognize the plate normally due to foreign matter, the recognition rate may decrease.
    * The service provides analysis results for a license plate in Korean only.

* Example of a license plate analysis image

![Image Example](http://static.toastoven.net/prod_carplate_ocr/VehiclePlateOCR_ex_img_en.png)

## Service Targets
* When you need to build a parking management system that manages vehicle entry and exit
* When you need to build a vehicle traffic control system
* When you need to build a traffic enforcement system for illegal parking, overloaded vehicles, and illegal license plates
* When you need to create a DB of vehicle license plates
* When you require car information analysis

## Privacy Policy
* While using the OCR service, the customer may collect personal and sensitive information of their users. Therefore, the customer of this service must inform a legal notice to their users as per the Personal Information Protection Act and acquire their consent regarding the matter. Also during this process, work consignment relation regarding the processing of personal information may arise between the customer and NHN Cloud. The customer who assumes the position of consignor may enter into a consignment contract with the consignee, NHN Cloud, separately in writing, and post a privacy policy notice by referencing the following:
    - Consignee: NHN Cloud Corp.
    - Consignment Description: Providing OCR service