## Sistem pakar
* Sistem pakar Generik untuk menghasilkan aturan dan membuat hubungan antara entri dan basis pengetahuan.
* Diimplementasikan menggunakan Forward Chaining dan Backward chaining.
* Harus memasukkan file json dengan format baik yang sesuai dengan contoh di folder `` data```
* Klausul harus terkait dengan basis Pengetahuan atau tidak akan masuk akal saat dijalankan.
* Parser dibuat untuk mengurai file json dan membuat objek saat runtime.

### Deskripsi
* Rule adalah string yang bisa dibandingkan.
* Pengetahuan terbentuk dari beberapa aturan
* Basis Pengetahuan terdiri dari berbagai pengetahuan
* Klausul adalah sekumpulan pertanyaan
* Klausa memiliki 3 atribut klausa, negatif, positif
* Untuk setiap klausa, basis pengetahuan dicari, persen lebih tinggi dari Pencocokan Min dikeluarkan
* Konstanta dapat diubah dari `` `` utils / constants.py```
* Lihat contoh `` data / ''

### Proses berpikir
* Format file Json yang dapat dengan jelas menentukan struktur yang akan diurai.
* Membaca file json dan membangun Basis Pengetahuan dan Basis Klausa.
* Input pengguna untuk setiap klausul diubah ke Basis Pengetahuan.
* Kedua basis Pengetahuan dibandingkan dan persentase maksimal yang cocok dikeluarkan.
* Mungkin ada beberapa pertandingan, kami dapat menampilkan detail dengan persentase.
* Jawaban akhirnya adalah Benar atau Salah.

   
* Sintaks basis pengetahuannya
```json
{
  "target": [
    {
      "name": "Kidney disease",
      "rules": {
        "1": "head aches",
        "2": "vomiting",
        "3": "body ache",
        "4": "no sleep"
      }
    },
    {
      "name": "Some target",
      "rules": {
        "1": "rule1",
        "2": "rule2"
      }
    }
  ]
}
```


* Sintak basis Clause
```json
{
  "1": {
    "question": "State your symptoms?",
    "answer": {
      "positive": "Yes, you are positive for ",
      "negative": "We don't see any signs of "
    }
  },
  "2": {
    "question": "question/statement",
    "answer": {
      "positive": "positive statement with potential to add target at end",
      "negative": "negative statement, target will be added at end"
    }
  }
}
```

----------------------------------
### contoh
* Backward Chaining
```console
Chankya >>> Tell me some features of this bird?
You >>> high flight, strong legs, yellow legs
[DEBUG] Target :: Falcons, Eagles --->  Matched :: 33.33333333333333

[INFO] I am not sure if this is the bird Falcons, Eagles
[INFO] Hope that you are satisfied with your answers !
```

* Forward Chaining
```console
Chankya >>> Tell me some features of this bird?
You >>> high flight, strong legs, yellow legs
[DEBUG] Target :: Falcons, Eagles --->  Matched :: 33.33333333333333
[DEBUG] Target :: Peacock --->  Matched :: 0.0
[DEBUG] Target :: Hen --->  Matched :: 0.0
[DEBUG] Target :: Albatrosses --->  Matched :: 0.0
[DEBUG] Target :: Paradise birds --->  Matched :: 0.0
[DEBUG] Target :: Crows --->  Matched :: 0.0
[DEBUG] Target :: Cuckoos --->  Matched :: 0.0
[DEBUG] Target :: Ducks, Geese and Swans --->  Matched :: 0.0

[INFO] I am not sure if this is the bird Falcons, Eagles
[INFO] Hope that you are satisfied with your answers !
```

-TERIMA KASIH-
