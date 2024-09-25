# Select2 Snippet

Berikut kumpulan select2 snippet yang biasa saya gunakan.

## Auto Focus Search On Click Select2

Untuk membuat Select2 secara otomatis mendapatkan fokus (`auto-focus`) ketika diklik, Anda bisa menggunakan event `select2:open` dan memanipulasi elemen input pencariannya.

Auto fucus ini diperlukan jika fitur search pada selec2 di aktifkan (default active).

### Javascript

```javascript
$(document).on('select2:open', () => {
    document.querySelector('.select2-search__field').focus();
});
```

## Get More Data On Selected Select2

Jika kamu ingin mendapatkan hasil tambahan dari Select2 saat sebuah item dipilih (`on select`), kamu bisa menggunakan event `select2:select` untuk mengambil data yang dipilih beserta properti-properti tambahan seperti `description` dan `code`.

Contoh implementasi di sisi JavaScript:

### Javascript

```javascript
$('#yourSelectElement').on('select2:select', function (e) {
    var data = e.params.data;

    // Akses data tambahan
    var id = data.id;
    var text = data.text;
    var description = data.description;  // Data tambahan
    var code = data.code;                // Data tambahan

    console.log("ID: " + id);
    console.log("Text: " + text);
    console.log("Description: " + description);
    console.log("Code: " + code);

    // Kamu bisa melakukan sesuatu dengan data tambahan di sini
});
```
