# Bug Report

| Sahə | Sahə adı |
|---|---|
| Bug ID | Bug_1 |
| Title | POST /ocr/passport sorğusunda şəkil yükləndikdə “Failed to process” xətası qaytarılır |
| Description | POST /ocr/passport sorğusunda "image" hissəsinə şəkil əlavə etdikdə API passport şəklini emal etmək əvəzinə "Failed to process" cavabı qaytarır. |
| Steps | 1. Bearer token ilə authorize olun <br> 2. POST `/ocr/passport` sorğusuna keçid edib “Try it out” düyməsinə klik et <br> 3. “Image” bölməsinə şəkil file-ı yerləşdir <br> 4. Qalan bölmələri uyğun olaraq doldur <br> 5. “Execute” düyməsinə klik et |
| Expected Result | Status Code `200` çıxmalı və sorğu uğurla yerinə yetirilməli idi, “200 Extracted document details” |
| Actual Result | Status Code `500` çıxdı və sorğu uğursuz alındı, “500 Failed to process Image” |
| Prioritet | High |
| Severity | High |
| Status | Açıq / Təsdiqlənmiş |
| Tapılan Vaxt | 26.05.2026 |
| Aşkar Edən Şəxs | Ləman Qurbanova |
| Əlavələr |  |
