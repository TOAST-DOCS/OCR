## AI Service > OCR > Vehicle Plate OCR > 오류 코드

| resultCode | resultKey | resultMessage                                                                |
|---|---|------------------------------------------------------------------------------|
| 0 | SUCCESS | SUCCESS                                                                      |
| -1 | FAIL | Unknown error.                                                               |
| 400 | BAD_REQUEST | Bad Request                                                                  |
| 401 | UNAUTHORIZED | Unauthorized                                                                 |
| 403 | FORBIDDEN | Forbidden                                                                    |
| 404 | NOT_FOUND | Not Found                                                                    |
| 405 | METHOD_NOT_ALLOWED | Method Not Allowed                                                           |
| 415 | UNSUPPORTED_MEDIA_TYPE | Unsupported Media Type                                                       |
| 4000001 | INVALID_PARAMETER | Invalid parameter.                                                           |
| 4000003 | INVALID_FILE_TYPE | Invalid file type.                                                           |
| 4000004 | UPLOADED_FILE_IS_EMPTY | Uploaded file is empty.                                                      |
| 4000201 | VEHICLE_PLATE_NOT_FOUND | Vehicle plate not found in the image.                                        |
| 4010001 | INVALID_APPKEY_SECRETKEY | Invalid appKey or secretKey.                                                 |
| 4010002 | INVALID_UUID | Invalid uuid.                                                                |
| 4010003 | NOT_ALLOWED_USER | Not allowed user.                                                            |
| 4010004 | INVALID_PROJECT | Invalid project.                                                             |
| 4010005 | UNAUTHORIZED_ROLE | Unauthorized role.                                                           |
| 4131000 | MAX_UPLOAD_SIZE_EXCEEDED | Request size is larger than permissible limit. the permissible limit is 5mb. |
| 5000001 | INTERNAL_API_FAIL | Internal Api fail.                                                           |
| 5000002 | ERROR_PARSING_FAIL | Error parsing fail.                                                          |
| 5000003 | DATABASE_FAIL | Database server error.                                                       |
| 5000004 | RESOURCE_DELETE_FAIL | All or some resource delete fail.                                            |
| 5000005 | FILE_READ_FAIL | File read fail.                                                              |
| 5004001 | OCR_VEHICLE_PLATE_API_FAIL | Vehicle Plate OCR Api fail.                                                  |
| 5004002 | OCR_VEHICLE_PLATE_API_RETURN_EMPTY | Vehicle Plate OCR Api returned empty body.                                   |
| 5004003 | OCR_VEHICLE_PLATE_RECOGNITION_FAIL | Vehicle Plate OCR failed to recognize the vehicle plate.                     |