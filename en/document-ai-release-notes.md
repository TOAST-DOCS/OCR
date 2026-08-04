## AI Service > OCR > Document AI > Release Notes

### August 11, 2026

- API endpoint domain changed
  - The new endpoint `https://api-ocr.nhncloudservice.com` has been added.
  - The existing endpoint `https://ocr.api.nhncloudservice.com` will be supported until July 31, 2027.
  - Please switch to the new endpoint. For more information, refer to the [API Guide](./document-ai-api-guide-v1.1.md).
- Maximum request file size increased
  - The maximum request file size has been increased from 5 MB to 20 MB.

### March 10, 2026

- API v1.1 released
  - Added API using User Access Key token authentication.
  - For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

### November 12, 2024

- Release of Document AI
  - Document AI extracts characters from images through OCR and provides questions and answers such as summarizing the content and extracting information based on the extracted informati on in conjunction with the LLM model.