# Mendapatkan current screen activity via ADB

- Koneksikan device dengan komputer/laptop, pastikan developer mode dengan usb debug nya aktif
- Jalankan perintah berikut:
  ```
  adb shell dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'
  ```
