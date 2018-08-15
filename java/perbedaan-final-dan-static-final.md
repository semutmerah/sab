## Perbedaan Final Dan Static Final
Ada dua deklarasi final variabel yang sering kita temukan.

Deklarasi 1:
```
final dataType variableName = value;
```

Deklarasi 2:
```
static final dataType variableName = value;
```

Deklarasi pertama adalah salah satu instance variabel, dalam artian tiap instance objek memiliki variabel tersebut (dalam memory yang berbeda). Dengan demikian, deklarasi pertama juga memungkinkan untuk dimasukkan ke dalam constructor. Contohnya:
```
public class Test {
  private final int a;

  // constructor
  public Test() {
    this.a = 1;
  }
}
```

Deklarasi kedua merupakan static variabel. Tiap instance hanya akan menunjuk ke satu static variabel yang sama, sehingga menghemat memory. Static variabel dapat diakses tanpa harus menginisiasi objek terlebih dahulu. Contohnya:
```
NamaObject.namaStaticVariabel
```

Biasanya deklarasi kedua dipakai untuk kasus dimana data tidak akan pernah berubah sama sekali untuk semua instance. Juga digunakan dalam utility class dimana inisiasi object tidak diperlukan.
