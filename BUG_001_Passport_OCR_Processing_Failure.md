# 🐞 Bug Report

| Field | Details |
|-------|---------|
| **Bug ID** | **BUG_001** |
| **Title** | POST `/ocr/passport` returns **500 "Failed to process image"** when a valid passport image is uploaded |
| **Description** | When a valid passport image is uploaded to the **POST `/ocr/passport`** endpoint, the API fails to process the image and returns a **500 Internal Server Error** instead of extracting the passport information. |
| **Steps to Reproduce** | 1. Authorize using a valid **Bearer Token**.<br>2. Navigate to the **POST `/ocr/passport`** endpoint in Swagger.<br>3. Click **Try it out**.<br>4. Upload a valid passport image in the **Image** field.<br>5. Fill in any remaining required fields.<br>6. Click **Execute**. |
| **Expected Result** | The API should return **200 OK** and successfully extract the passport information (**"200 Extracted document details"**). |
| **Actual Result** | The API returned **500 Internal Server Error** with the message **"Failed to process image"**, and the passport information was not extracted. |
| **Priority** | High |
| **Severity** | High |
| **Status** | Open / Confirmed |
| **Date Reported** | 26.05.2026 |
| **Reported By** | Ləman Qurbanova |
| **Attachments** | *(Add the Swagger response screenshot or error response here if available.)* |
