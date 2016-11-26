## fatal: could not read Username for 'https://github.com': terminal prompts disabled

Jika mendapati error seperti ini, berikut adalah langkah yang harus dilakukan:
1. Setup osxkeychain credential helper, bisa merujuk [di sini](https://help.github.com/articles/caching-your-github-password-in-git/)
2. Jika menggunakan 2FA, generate personal akses token [di sini](https://github.com/settings/tokens)
3. git clone private repo yang mengalami kendala, masukkan username github dan token/password
4. Remove repo hasil clone di local, dan coba kembali menjalankan perintah ketika mendapati error di atas.
