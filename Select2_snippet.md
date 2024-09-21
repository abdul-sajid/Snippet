# Select2 Snippet

Berikut kumpulan select2 snippet yang biasa saya gunakan.

## Auto Focus Search On Click Select2

Untuk membuat Select2 secara otomatis mendapatkan fokus (auto-focus) ketika diklik, Anda bisa menggunakan event select2:open dan memanipulasi elemen input pencariannya.

Auto fucus ini diperlukan jika fitur search pada selec2 di aktifkan (default active).

### VanilaJS

```javascript
selectElement.addEventListener('select2:open', function() {
    // Tunggu sampai elemen pencarian Select2 muncul, lalu fokuskan
    const searchInput = document.querySelector('.select2-search__field');
    if (searchInput) {
        searchInput.focus();
    }
});
```

### jQuery

```javascript
$(document).on('select2:open', () => {
    $('.select2-search__field').focus();
});
```
