# Fix Too Many Authentication Failures

Jika mendapat error seperti ini:

```
$ Received disconnect from host: 22:2 Too many authentication failures for your_user
```

Ini biasanya terjaddi karena system anda memiliki lima atau lebih DSA/RSA identity file tersimpan di folder ~/.ssh anda.
Cara mengakalinya adalah memaksa untuk login tanpa menggunakan DSA/RSA, dengan command di bawah ini:

```
$ ssh -o PubkeyAuthentication=no root@host
```
