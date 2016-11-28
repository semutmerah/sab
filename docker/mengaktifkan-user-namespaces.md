## Mengaktifkan user namespaces

User namespaces adalah fitur sekuriti baru sejak docker versi 1.10. Dengan user namespaces ini, maka container yang berjalan dengan user root akan secara otomatis diberikan user non-root pada sisi host. Hal ini tentu memberikan isolasi yang lebih baik antara container dengan host. Namun, secara default user namespaces ini tidaklah aktif. Berikut adalah cara untuk mengaktifkan user namespaces (asumsi menggunakan ubuntu min versi 16.04 yang menggunakan systemctl):

1. Edit unit file pada service docker
  ```
  $ sudo systemctl edit --full docker.service
  ```

2. tambahkan --userns-remap=default pada baris _ExecStart=/usr/bin/dockerd -H fd://_, simpan ubahan
  ```
  ExecStart=/usr/bin/dockerd --userns-remap=default -H fd://
  ```

3. Reload systemctl
  ```
  $ sudo systemctl daemon-reload
  ```

4. Restart docker
  ```
  $ sudo systemctl restart docker
  ```

Voila!

Untuk mengetestnya, cobalah running sebuah image dan mount volume /etc/ ke container, lalu cobalah membuat file baru pada volume tersebut. Seharusnya eksekusi membuat file baru akan gagal karena telah menerapkan user namespaces.
