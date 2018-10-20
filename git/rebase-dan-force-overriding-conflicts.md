# Rebase dan Force Overriding Conflicts

Use case:

- Kita punya branch bernama ```wip``` yang merupakan pisahan dari branch ```master```.
- Branch ```master``` saat ini memiliki banyak commitan baru yang masuk sejak kita membuat branch ```wip```.
- Kita mau update kondisi branch kita ke posisi terakhir dari branch ```master``` dengan teknik rebase. Namun ternyata, ada conflict saat proses rebase.
- Kita ingin secara otomatis solving conflict dengan memenangkan kondisi terakhir dari branch kita, tanpa harus manual solving conflict di editor.

Langkah:

1. checkout ke branch ```master```.
2. pull dari ```origin/master``` ke ```master``` lokal kita.
3. checkout kembali ke branch ```wip```.
4. pastikan tidak ada kerjaan yang belum di commit di branch ```wip```. Jika ada, bisa stash terlebih dahulu jika belum selesai atau commit dahulu jika memang sudah selesai.
5. Jalankan perintah berikut : ```$ git rebase -Xtheirs master -f```. Ini akan memenangkan commitan di sisi kita jika terjadi conflict.
6. Jika ingin memenagkan sisi master ketika ada conflict ketika rebase, maka perintahnya adalah : ```$ git rebase -Xours master -f```. 