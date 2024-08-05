Eksekusi perintah ini lewat powershell

```
while ($true) { sleep 1; try { (ps -ea silent *nama_process*).processoraffinity = 1023; echo "Set affinity!"; break } catch { echo "Waiting..." } }
```

Cara hitung affinity:
- 1 core = 1
- 2 core = 1 + 2 = 3
- 3 core = 1 + 2 + 4 = 7
- 4 core = 1 + 2 + 4 + 8 = 15
- dst
