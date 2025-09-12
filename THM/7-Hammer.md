## Info
- Platform: TryHackMe  
- Difficulty: Easy

---

## Enumeration

### Login Page
<img width="1919" height="830" alt="Screenshot_2025-09-10_06-46-58" src="https://github.com/user-attachments/assets/8673409d-5053-4627-9e26-32ae2c1dbcd6" />

- Discovered a standard login form.

<img width="1919" height="829" alt="Screenshot_2025-09-11_11-28-48" src="https://github.com/user-attachments/assets/736213f2-9c2d-4df7-8f82-fadfffdbfaa6" />

- In the page source, a developer note was found:
```html
<!-- Dev Note: Directory naming convention must be hmr_DIRECTORY_NAME -->
```
---

### Directory Fuzzing
<img width="1919" height="875" alt="Screenshot_2025-09-11_11-35-43" src="https://github.com/user-attachments/assets/44caa73c-6126-49ef-ae1c-23b4b2f0c782" />

Discovered:
- `/hmr_css`
- `/hmr_images`
- `/hmr_js`
- `/hmr_logs`

---

<img width="1919" height="828" alt="Screenshot_2025-09-11_11-36-39" src="https://github.com/user-attachments/assets/3be636bc-a961-4ffc-a6d2-11b9419ae858" />

- Navigated to /hmr_logs/ and found error.logs.

---

<img width="1919" height="821" alt="Screenshot_2025-09-11_11-38-39" src="https://github.com/user-attachments/assets/599acaef-1504-49f5-af66-13fd2be4d641" />

- Email address found in logs:tester@hammer.thm

---

## Exploitation
<img width="1919" height="825" alt="Screenshot_2025-09-11_11-45-32" src="https://github.com/user-attachments/assets/3a77a5c1-bd7a-4735-a71f-48b967390c1f" />

- On `reset_password.php`, the application requested a 4-digit recovery code.

---

Generated wordlist of all codes:

<img width="524" height="81" alt="Screenshot_2025-09-11_11-47-39" src="https://github.com/user-attachments/assets/0cdcea36-6c63-4469-8c05-d56cca8c0ae7" />

---

<img width="1919" height="859" alt="Screenshot_2025-09-11_12-36-47" src="https://github.com/user-attachments/assets/a6d492b0-70e4-40d8-912a-988d8f1e8208" />


- Brute-forced with ffuf, bypassing rate limits via X-Forwarded-For
- First flag obtained:
<img width="1918" height="828" alt="image" src="https://github.com/user-attachments/assets/f0a1f2c8-e585-4780-bb28-95658be1eb05" />

---

### Persistence via Expiry Date Manipulation
<img width="1919" height="476" alt="Screenshot_2025-09-11_12-39-19" src="https://github.com/user-attachments/assets/e66a3c9c-ae34-42d5-b6d1-a33853fa6b64" />

- After logging in, browser storage revealed the JWT token had an expiry field (exp). By manually editing the expiry date to a far future timestamp, the session persisted and bypassed automatic logout.

---

## Privilege Escalation
<img width="1919" height="875" alt="Screenshot_2025-09-11_12-41-06" src="https://github.com/user-attachments/assets/d4c37caa-1e5a-4111-83f8-b45492bd9295" />

- Retrieved the signing key directly from the server.

### Forging Admin Token (+ Persistence)
<img width="1919" height="756" alt="Screenshot_2025-09-11_13-05-24" src="https://github.com/user-attachments/assets/21f47d77-53e1-472b-9e22-0aa8253f07b5" />

- Modified payload to escalate role:
```bash
{
  "user_id": 1,
  "email": "tester@hammer.thm",
  "role": "admin"
}
```
Note: Used as `Authorization: Bearer <token>`.

---

### Command Execution
- As admin, accessed `/execute_command.php`.
- Final flag retrieved by reading `/home/ubuntu/flag.txt`:

<img width="1918" height="825" alt="image" src="https://github.com/user-attachments/assets/8a63aa0c-04fe-4f74-bfa7-145444b844cf" />

- Flag found: `[FLAG FOUND]`
