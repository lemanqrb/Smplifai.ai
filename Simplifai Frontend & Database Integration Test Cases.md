# Simplifai Frontend Testing Report

---

## 1. Sign up with valid data

### Description
Valid məlumatlarla qeydiyyatdan keçmək.

### Steps
1. Simplifai frontend-də qeydiyyat səhifəsinə keçid etdim
2. Valid e-mail – “leman.qrb@gmail.com” daxil etdim
3. Valid name – “Ləman” daxil etdim
4. Valid password – “LDA0700fr@” daxil etdim
5. Password-u yenidən daxil etdim
6. SMPLIFAI's Terms of Use and Privacy Policy checkbox hissəsini qəbul etdim
7. “Create an account” buttonuna klik etdim

### Expected Result
İstifadəçi valid məlumatlarla uğurla qeydiyyatdan keçməlidir.

### Actual Result
E-mail təsdiqindən sonra istifadəçi əsas səhifəyə yönləndirildi.

### Database Check
```sql
Select * from profiles where first_name = 'Ləman';
```

Result:
```text
2026-04-14
id: a3c38e71-9784-4b8c-81af-9692a2aa8373
```

---

## 2. Sign up with invalid e-mail

### Description
Yanlış e-mail formatı ilə qeydiyyatdan keçmək.

### Steps
1. Simplifai frontend-də qeydiyyat səhifəsinə keçid etdim
2. Invalid e-mail – “leman123.qrbgmail.com” daxil etdim
3. Valid name – “Leman” daxil etdim
4. Valid password – “LDA0700fr@” daxil etdim
5. Password-u yenidən daxil etdim
6. SMPLIFAI's Terms of Use and Privacy Policy checkbox hissəsini qəbul etdim
7. “Create an account” buttonuna klik etdim

### Expected Result
Sistem yanlış e-mail formatını aşkarlamalı və qeydiyyat prosesini dayandırmalıdır.

### Actual Result
Sistem hesab yaratmadı və e-mail formatının yanlış olduğuna aid validation error mesajı göstərildi.

### Database Check
```sql
SELECT * FROM profiles 
WHERE first_name = 'Leman';
```

Result:
```text
No data is found in the database because the account was not created due to the invalid e-mail address format.

Test Date: 2026-05-09
```

---

## 3. Profildəki məlumatları dəyişdirmək

### Description
Adımı dəyişdirərək profilimi yenilədim.

### Steps
1. Simplifai frontend-də “Profile” bölməsinə keçid etdim
2. Adımı dəyişdirib, soyadımı olduğu kimi saxladım
3. Nömrəni olduğu kimi saxladım
4. “Send code” buttonuna klik etdim
5. E-maili olduğu kimi saxladım
6. “Save changes” buttonuna klik etdim

### Expected Result
Profil uğurla yenilənməlidir.

### Actual Result
“Profile updated successfully!” bildirisi ekranda göründü.

### Database Check
```sql
Select * from profiles where first_name = 'Lale';
```

Result:
```text
a3c38e71-9784-4b8c-81af-9692a2aa8373 id-də istifadəçi mövcuddur.
```

---

## 4. Log out from the system

### Description
İstifadəçinin sistemdən uğurla çıxış etməsini yoxlamaq.

### Steps
1. Simplifai frontend-də hesabıma daxil oldum
2. “Profile” bölməsinə keçid etdim
3. “Log out” buttonuna klik etdim

### Expected Result
İstifadəçi sistemdən uğurla çıxış etməli və login səhifəsinə yönləndirilməlidir.

### Actual Result
İstifadəçi sessiyası sonlandırıldı və istifadəçi login səhifəsinə yönləndirildi.

### Database Check
```sql
SELECT * FROM profiles 
WHERE first_name = 'Leman';
```

Result:
```text
User is not found in active data because the user successfully logged out from the system.

Test Date: 2026-05-09
```

---

## 5. “Sign in with Google” with valid data

### Description
Google vasitəsilə valid Google hesabı ilə sayta giriş etmək.

### Steps
1. Simplifai frontend-də login səhifəsinə keçid etdim
2. “Sign in with Google” buttonuna klik etdim
3. Valid Google hesabı – “lilithate601@gmail.com” seçdim
4. Valid phone number – “0559448073” daxil etdim
5. “Confirm” buttonuna klik etdim

### Expected Result
İstifadəçinin hesabı yaradılmalı və uğurla sayta daxil olmalıdır.

### Actual Result
İstifadəçinin hesabı yaradıldı və uğurla sayta daxil oldu.

### Database Check
```sql
Select * from profiles where first_name = 'Lilith';
```

Result:
```text
fb5d2633-580a-4683-9ed9-d42d23a84b43 id-yə sahib istifadəçi mövcuddur.
```

---

## 6. Log in with an invalid password

### Description
Yanlış şifrə ilə sistemə giriş etmək.

### Steps
1. Simplifai frontend-də login səhifəsinə keçid etdim
2. Valid e-mail – “moonloor22@gmail.com” daxil etdim
3. Invalid password – “1234679sd” daxil etdim
4. “Log in” buttonuna klik etdim

### Expected Result
Sistem “Invalid login credentials” error mesajı göstərməli və istifadəçi sistemə daxil olmamalıdır.

### Actual Result
“Invalid login credentials” error mesajı göstərildi və istifadəçi sistemə daxil ola bilmədi.

### Database Check
```sql
SELECT * FROM profiles
WHERE email = 'leman.qrb@gmail.com';
```

Result:
```text
User exists in the database, but login is not successful because the entered password is invalid.

Test Date: 2026-05-09
```

---

## 7. Yanlış format ilə profil məlumatlarını dəyişmək

### Description
Ad hissəsinə xüsusi simvollar daxil edərək profil məlumatlarını yeniləmək.

### Steps
1. Simplifai frontend-də “Profile” bölməsinə keçid etdim
2. Ad hissəsinə “#$%&*” daxil etdim
3. Nömrəni olduğu kimi saxladım
4. “Send code” buttonuna klik etdim
5. E-maili olduğu kimi saxladım
6. “Save changes” buttonuna klik etdim

### Expected Result
Error mesajı görünməlidir. Hərf yazılmalı olan hissəyə xüsusi simvollar daxil edilmişdir.

### Actual Result

```diff
- “Profile updated successfully!” bildirisi ekranda görsəndi.
```

### Database Check
```sql
Select * from profiles where first_name = '#$%&*';
```

Result:
```text
a3c38e71-9784-4b8c-81af-9692a2aa8373 id-sinə sahib istifadəçi mövcuddur.
```

---

## 8. Düzgün məlumatlarla “New Application” yaratmaq

### Description
Valid məlumatlarla “New Application” buttonundan istifadə edərək yeni tətbiq yaratmaq.

### Steps
1. Simplifai frontend-də Dashboard hissəsinə keçid etdim
2. “New Application” buttonuna klik etdim
3. E-mail və telefon nömrəmi daxil etdim
4. “Choose” buttonuna klik etdim
5. Şəkil yerləşdirdim
6. “Submit passport to review” buttonuna klik etdim
7. First name və last name hissələrini valid data ilə doldurdum
8. “Approve” buttonuna klik etdim

### Expected Result
Yeni tətbiq uğurla yaradılmalıdır.

### Actual Result
İstifadəçi valid məlumatlarla yeni tətbiq yaratdı və tətbiq uğurla dashboard/history bölməsində görüntüləndi.

### Database Check
```sql
Select * from applications where created_at = '2026-05-27 15:56:12.376057+00';
```

Result:
```text
6051ddcc-1afd-41a4-9db8-f587e3a4213e id-yə sahib yeni tətbiq mövcuddur.
```

---

## 9. Yanlış məlumat formatı ilə tətbiq yaratmaq

### Description
Yanlış məlumat formatı ilə “New Application” buttonundan istifadə edərək yeni tətbiq yaratmaq.

### Steps
1. Simplifai frontend-də Dashboard bölməsinə keçdim
2. “New Application” buttonuna klik etdim
3. E-mailimi düzgün məlumatlarla daxil etdim
4. Telefon nömrəmi rəqəmlər əvəzinə xüsusi simvollarla doldurdum
5. “Choose” buttonuna klik etdim
6. Şəkil yerləşdirdim
7. “Submit Documents” buttonuna klik etdim

### Expected Result
Error mesajı görünməlidir.

### Actual Result

```diff
- “Enrollment Agreement” application-u yaradıldı.
```

### Database Check
```sql
Select * from applications where phone = '+44@#$%^&*()';
```

Result:
```text
8c172506-d34f-4d5a-b2d3-eb9f613882db id-yə sahib yeni tətbiq mövcuddur.
```

---

## 10. History bölməsində PDF faylının düzgün yüklənməsinin yoxlanılması

### Description
History bölməsində PDF faylının düzgün şəkildə yüklənib-yüklənmədiyini yoxlamaq.

### Steps
1. Simplifai frontend-də History bölməsinə keçid etmək
2. “Application history”-dan hər hansısa bir application sənədinin yanında yerləşən PDF yükləmə işarəsinin üzərinə klik etmək

### Expected Result
PDF-in yükləndiyinə aid bildiriş gəlməlidir.

### Actual Result
Ekranda PDF-in yükləndiyini göstərən bildiriş görsəndi.
