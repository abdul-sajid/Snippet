# Snippet Template AdminLTE 3.x

AdminLTE3 adalah favorit admin template yang saya gunakan di tiap tiap project. alasan nya karena gratis dan banyak feature-feature yang menarik 😂, AdminLTE 3.x menggunakan framework bootstrap versi 4.6. Berikut adalah kumpulan snippet untuk template AdminLTE 3.x.

## Auto Active Sidebar

Auto active ini sangat bermanfaat sekali terutama pada menu sidebar yang dynamic, saya selalu menggunakan menu berbasis database mau project kecil / besar saya gunakan menu dari database. kalau pun tidak dynamic masih bisa digunakan.

```javascript
function activeSidebar() {
    /** add active class and stay opened when selected */
    var origin = window.location.origin;
    var pathname = window.location.pathname;
    var url = origin + pathname;

    // for sidebar menu entirely but not cover treeview
    $('ul.nav-sidebar a').filter(function() {
        return this.href == url;
    }).addClass('active');

    // for treeview
    $('ul.nav-treeview a').filter(function() {
        return this.href == url;
    }).parentsUntil(".nav-sidebar > .nav-treeview").addClass('menu-open').prev('a').addClass('active');
 }
```

## Dark Mode

AdminLTE 3 support dark mode di template bawaan nya sudah ada fitur dark mode, berikut adalah snippet fitur dark mode dengan local storage dan toggle untuk pergantian tema dark mode atau tema light mode.
Secara defautl fitur ini akan menyesuaikan dengan tema system operasi yang sedang digunakan.

### HTML Togle

Letakan kode berikut di bagian navbar tepatnya di dalam element class navbar-nav ml-auto

```html
<ul class="navbar-nav ml-auto">
    <!-- Right navbar links -->
    <li class="nav-item">
        <div class="nav-link">
            <div class="theme-switch">
                <input type="checkbox" class="checkbox" id="checkbox">
                <label for="checkbox" class="checkbox-label">
                    <i class="fas fa-moon"></i>
                    <i class="fas fa-sun"></i>
                    <span class="ball"></span>
                </label>
            </div>
        </div>
    </li>
</ul>
```

### CSS Togle

Letakan kode berikut di bagian css

```css
.checkbox {
    opacity: 0;
    position: absolute;
}

.checkbox-label {
    background-color: #fff;
    box-shadow: rgb(204, 219, 232) 3px 3px 6px 0px inset, rgba(255, 255, 255, 0.5) -3px -3px 6px 1px inset;
    width: 40px;
    height: 20px;
    border-radius: 50px;
    position: relative;
    padding: 5px;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;

}

body.dark-mode .checkbox-label {
    background-color: #111;
}

.theme-switch {
    margin: 0 auto;
}

.theme-switch .fa-moon {
    color: #fff;
}

.theme-switch .fa-sun {
    color: #f1c40f;
}

body.dark-mode .checkbox-label .ball {
    background-color: #454d55;
}

.checkbox-label .ball {
    background-color: #fff;
    width: 20px;
    height: 20px;
    position: absolute;
    left: 0px;
    top: 0px;
    border-radius: 50%;
    transition: transform 0.2s linear;
    box-shadow: rgba(0, 0, 0, 0.4) 0px 2px 4px, rgba(0, 0, 0, 0.3) 0px 7px 13px -3px, rgba(0, 0, 0, 0.2) 0px -3px 0px inset;
}

.checkbox:checked+.checkbox-label .ball {
    transform: translateX(20px);
}
```

### Javascript Togle

```javascript
var toggleSwitch = document.querySelector('.theme-switch input[type="checkbox"]');
  var currentTheme = localStorage.getItem('theme');
  var mainHeader = document.querySelector('.main-header');

  if (currentTheme) {
    if (currentTheme === 'dark') {
      if (!document.body.classList.contains('dark-mode')) {
        document.body.classList.add("dark-mode");
      }
      if (mainHeader.classList.contains('navbar-light')) {
        mainHeader.classList.add('navbar-dark');
        mainHeader.classList.remove('navbar-light');
        mainHeader.classList.remove('bg-white');
      }
      toggleSwitch.checked = true;
    }
  }

  function switchTheme(e) {
    if (e.target.checked) {
      if (!document.body.classList.contains('dark-mode')) {
        document.body.classList.add("dark-mode");
      }
      if (mainHeader.classList.contains('navbar-light')) {
        mainHeader.classList.add('navbar-dark');
        mainHeader.classList.remove('navbar-light');
        mainHeader.classList.remove('bg-white');
      }
      localStorage.setItem('theme', 'dark');
    } else {
      if (document.body.classList.contains('dark-mode')) {
        document.body.classList.remove("dark-mode");
      }
      if (mainHeader.classList.contains('navbar-dark')) {
        mainHeader.classList.add('navbar-light');
        mainHeader.classList.add('bg-white');
        mainHeader.classList.remove('navbar-dark');
      }
      localStorage.setItem('theme', 'light');
    }
  }

  toggleSwitch.addEventListener('change', switchTheme, false);
```

### Javascript Load Current Theme
Letakan kode berikut tepat di bawah `<body>`
```html
<script>
    var currentTheme = localStorage.getItem('theme');
    if (currentTheme)
        if (currentTheme === 'dark')
            if (!document.body.classList.contains('dark-mode')) document.body.classList.add("dark-mode");
</script>
```
