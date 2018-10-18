# Nested virtualization di docker

Nested virtualization adalah konsep di mana sebuah environment virtual berjalan di dalam sebuah environment yang juga tervirtualisasi. Hypervisor atau VM yang berjalan di tingkat paling bawah bisa dikategorikan sebagai level 0, atau L0 hypervisor. Jika ditambahkan hypervisor lagi di atasnya, maka bisa dikategorikan sebagai L1 hypervisor, naik keatas nya akan menghasilkan L2 hypervisor, dan seterusnya.

Secara bagan, bisa digambarkan sebagai berikut:

```

    OS Installed by L1      <-- L1 Guest
       Hypervisor
-------------------------
     Hypervisor / VM        <-- L1 Hypervisor
-------------------------
    OS Installed by L0      <-- L0 Guest
        Hypervisor
-------------------------
     Hypervisor / VM        <-- L0 Hypervisor
-------------------------
Windows or MacOS or Linux   <-- Host
-------------------------
        PC or Mac           <-- Hardware
```

## Kapan nested virtualization diperlukan di docker?

Kita bisa ambil satu use case: **menjalankan android emulator x86 di dalam docker**.

Jika digambarkan dengan bagan, maka seperti inilah bagan saat ini yang memungkinkan untuk berjalannya android emulator x86 di docker:

```

     Android (x86)          <-- L1 Guest
-------------------------
     KVM / Hyper-V
   bypassing from L0        <-- L1 Hypervisor      
-------------------------
    Ubuntu / Windows        <-- L0 Guest
   container by Docker
-------------------------
        Docker              <-- L0 Hypervisor
-------------------------
    Linux or Windows        <-- Host
-------------------------
          PC                <-- Hardware
```

## Tunggu - tunggu, kenapa di bagan hanya disebut Linux dan Windows sebagai host? Bagaimana dengan MacOS?

Pertanyaan bagus. Limitasi ini sendiri terjadi karena implementasi docker yang berbeda terhadap setiap OS host. Pada Host Linux, docker memanfaatkan KVM sebagai mesin Hypervisor. Pada Ubuntu 18.04 dan minimal Processor yang support x86 virtualization (Intel VT-x / AMD-V), KVM secara otomatis sudah support nested virtualization. Untuk mengeceknya, bisa dengan menjalankan perintah berikut pada bash terminal host :

```
$ cat /sys/module/kvm_intel/parameters/nested
```
Jika aktif, maka anda akan melihat output ```Y``` atau ```1```

Saat ini, sudah banyak juga projek open source dengan misi menjalankan android emulator x86 di docker, dengan limitasi Linux sebagai host Docker. Salah satunya adalah projek ini: https://github.com/butomo1989/docker-android

Sedangkan pada Host Windows, docker memanfaatkan Hyper-V yang merupakan Hypervisor native Windows sebagai basis. Merujuk pada blog windows di sini : https://blogs.msdn.microsoft.com/visualstudio/2018/05/08/hyper-v-android-emulator-support/ , Hyper-V juga telah support nested virtualization dan memungkinkan untuk menjalankan android emulator x86 pada docker dengan host Windows.

Sedangkan pada MacOS, saat ini Docker berjalan dengan memanfaatkan [Hyperkit](https://github.com/moby/hyperkit). Kekurangan Hyperkit sendiri adalah sampai saat ini belum support nested virtualization, yang dikuatkan oleh issue yang tercatat di repository hyperkit [di sini](https://github.com/moby/hyperkit/issues/127).

Lalu apakah ada alternatif lain untuk MacOS? Saat ini ada 2 opsi yang diketahui (1 baru sekedar teori):
 1. Memilih emulator armeabi sebagai pilihan. Namun, sebagai yang kita ketahui emulator dengan komputasi armeabi berjalan sangat-sangat lambat bila dibandingkan dengan komputasi x86.
 2. (belum coba, baru teori) Menjalankan Ubuntu OS di VirtualBox, dengan mengaktifkan KVM di opsi paravirtualization nya VirtualBox. Lalu install docker di dalamnya. Dari sini lanjut menjalankan android emulator x86 docker image di dalamnya.