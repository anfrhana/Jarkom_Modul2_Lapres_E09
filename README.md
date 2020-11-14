# Jarkom_Modul2_Lapres_E09

## 1. Website utama dengan alamat http://semerue09.pw
membuat domain konfigurasi pada MALANG (DNS master) di /etc/bind/named.conf.local

<img width="377" alt="1" src="https://user-images.githubusercontent.com/61228737/99058594-04452e00-25d0-11eb-9168-00ea7a1ebf12.png">

copy file db.local pada path /etc/bind ke dalam folder /jarkom/semerue09.pw.

kemudian buka file yang telah di-copy dan isi menjadi seperti berikut:

<img width="386" alt="2" src="https://user-images.githubusercontent.com/61228737/99058773-3c4c7100-25d0-11eb-8a62-d3635d1b31d9.png">

restart bind9 dengan ```service bind9 restart```

coba ping pada GRESIK (klien) apakah sudah bekerja dengan baik

<img width="374" alt="3" src="https://user-images.githubusercontent.com/61228737/99059047-9b11ea80-25d0-11eb-82c8-1c6476b1aa1d.png">

## 2. Membuat alias http://www.semerue09.pw
tambahkan CNAME pada file /etc/bind/jarkom/semerue09.pw

<img width="376" alt="4" src="https://user-images.githubusercontent.com/61228737/99059274-efb56580-25d0-11eb-8ba5-f7857b544bc2.png">

restart bind9 dengan ```service bind9 restart```

coba ping untuk melihat apakah alias sudah bekerja dengan baik

<img width="382" alt="5" src="https://user-images.githubusercontent.com/61228737/99059364-11165180-25d1-11eb-95f1-bc5eedb142aa.png">

## 3. Membuat subdomain http://penanjakan.semerue09.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO
pada file /etc/bind/jarkom/semerue09.pw tambahkan sebagai berikut:

<img width="382" alt="6" src="https://user-images.githubusercontent.com/61228737/99059576-5cc8fb00-25d1-11eb-81f9-b4b62052ec5e.png">

restart bind9 dengan ```service bind9 restart```

coba ping untuk melihat apakah sudah bekerja dengan baik

<img width="380" alt="7" src="https://user-images.githubusercontent.com/61228737/99059680-7cf8ba00-25d1-11eb-8650-ba7d994d8f12.png">

## 4. Membuat reverse domain untuk domain utama
Tambahakan konfigurasi berikut di file /etc/bind/named.conf.local pada MALANG

<img width="374" alt="8" src="https://user-images.githubusercontent.com/61228737/99059978-e8db2280-25d1-11eb-9174-bf9fff0f6e86.png">

copy file db.local pada path /etc/bind/jarkom/71.151.10.in-addr.arpa

kemudian buka file yang telah di-copy dan isi menjadi seperti berikut:

<img width="385" alt="8 5" src="https://user-images.githubusercontent.com/61228737/99060412-95b59f80-25d2-11eb-90ce-bcdea260b9f6.png">

restart bind9 dengan ```service bind9 restart```

coba cek dengan ```host -t PTR 10.151.71.84``` pada klien

<img width="381" alt="9" src="https://user-images.githubusercontent.com/61228737/99060217-4a02f600-25d2-11eb-8149-9c3769834e25.png">

## 5. Membuat DNS server slave
edit file /etc/bind/named.conf.local pada MALANG (DNS master) sebagai berikut:

<img width="383" alt="10" src="https://user-images.githubusercontent.com/61228737/99061575-5d16c580-25d4-11eb-8097-e315d0ee843d.png">

buka file /etc/bind/named.conf.local pada MOJOKERTO (DNS slave) dan tambahkan syntax berikut:

<img width="380" alt="11" src="https://user-images.githubusercontent.com/61228737/99061720-8cc5cd80-25d4-11eb-9099-2d2a0a699700.png">

untuk melakukan testing, pada MALANG kita stop bind9 dengan syntax ```service bind9 stop```

lalu pada klien dicek apakah slave sudah bekerja dengan baik

<img width="380" alt="13" src="https://user-images.githubusercontent.com/61228737/99062068-fcd45380-25d4-11eb-90d7-0b4845eeb216.png">

## 6. Membuat subdomain dengan alamat http://gunung.semerue09.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO.
edit file /etc/bind/jarkom/semerue09.pw pada MALANG sebagai berikut:

<img width="373" alt="14" src="https://user-images.githubusercontent.com/61228737/99062314-66ecf880-25d5-11eb-9f05-25ee638ce662.png">

edit file /etc/bind/named.conf.options pada MALANG kemudian comment dnssec-validation auto dan tambahkan ```allow-query{ any; };```

<img width="375" alt="15" src="https://user-images.githubusercontent.com/61228737/99062475-a3b8ef80-25d5-11eb-8dd1-550019b44e4c.png">

edit file /etc/bind/named.conf.options juga pada MOJOKERTO kemudian comment dnssec-validation auto dan tambahkan ```allow-query{ any; };```

<img width="381" alt="16" src="https://user-images.githubusercontent.com/61228737/99062578-ca772600-25d5-11eb-8330-8c77f08544a9.png">

edit file /etc/bind/named.conf.local pada MOJOKERTO menjadi sebagai berikut:

<img width="381" alt="17" src="https://user-images.githubusercontent.com/61228737/99062835-2c379000-25d6-11eb-8458-1a09cc186977.png">

buat direktori dengan nama delegasi lalu copy db.local ke /etc/bind/delegasi/gunung.semerue09.pw

buka file yang telah di-copy lalu ubah menjadi seperti di bawah ini:

<img width="374" alt="18" src="https://user-images.githubusercontent.com/61228737/99063266-d8797680-25d6-11eb-8af6-7c85f4027418.png">

coba ping pada klien untuk mengecek apakah sudah benar

<img width="378" alt="19" src="https://user-images.githubusercontent.com/61228737/99063357-f8109f00-25d6-11eb-98c1-5064fb909fb2.png">

## 7. Membuat subdomain dengan nama http://naik.gunung.semerue09.pw, domain ini diarahkan ke IP Server PROBOLINGGO
pada file /etc/bind/delegasi/gunung.semerue09.pw ditambahkan sebagai berikut:

<img width="380" alt="20" src="https://user-images.githubusercontent.com/61228737/99063548-3f972b00-25d7-11eb-936c-691c6cb7a130.png">

coba ping pada klien untuk mengetahui apakah sudah bekerja dengan baik

<img width="375" alt="21" src="https://user-images.githubusercontent.com/61228737/99063639-5c336300-25d7-11eb-80aa-89b8ad89c12a.png">

## 8. mengatur web server domain http://semerue09.pw memiliki DocumentRoot pada /var/www/semerue09.pw
buat file /etc/apache2/sites-available/semerue09.pw.conf dengan meng-copy file  /etc/apache2/sites-available/000-default.conf dan edit menjadi sebagai berikut:

<img width="384" alt="22" src="https://user-images.githubusercontent.com/61228737/99063891-c6e49e80-25d7-11eb-8885-17277d6819f8.png">

setelah edit, jalankan ```a2ensite semerue09.pw.conf``` lalu ```service apache2 restart``` pada PROBOLINGGO (web server)

<img width="383" alt="23" src="https://user-images.githubusercontent.com/61228737/99064071-04e1c280-25d8-11eb-9305-4eeb6d99f440.png">

buka browser, cek hasilnya dengan mengunjungi semerue09.pw

<img width="960" alt="24" src="https://user-images.githubusercontent.com/61228737/99064168-23e05480-25d8-11eb-85aa-b8a85018aab5.png">

## 9. Diaktifkan mod rewrite agar alamat http://semerue09.pw/index.php/home menjadi http://semerue09.pw/home

aktifkan mod rewrite dengan ```a2enmod rewrite```

<img width="390" alt="25" src="https://user-images.githubusercontent.com/61228737/99064463-92bdad80-25d8-11eb-9a2c-4744aa5e7f40.png">

buat file /var/www/semerue09.pw/.htaccess sebagai berikut:

<img width="385" alt="26" src="https://user-images.githubusercontent.com/61228737/99064628-ca2c5a00-25d8-11eb-9b88-10b74564ee56.png">

cek pada browser, buka semerue09.pw/home apakah sudah benar

<img width="960" alt="27" src="https://user-images.githubusercontent.com/61228737/99064650-d1536800-25d8-11eb-9f5f-7646f8f94ff2.png">

## 10. Web http://penanjakan.semerue09.pw akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semerue09.pw
memiliki struktur folder sebagai berikut:
/var/www/penanjakan.semeruyyy.pw
                                 /public/javascripts
                                 /public/css
                                 /public/images
                                 /errors

buat file /etc/apache2/sites-available/penanjakan.semerue09.pw.conf dengan meng-copy file  /etc/apache2/sites-available/000-default.conf dan edit menjadi sebagai berikut:

<img width="382" alt="29" src="https://user-images.githubusercontent.com/61228737/99065151-87b74d00-25d9-11eb-91c7-0c414b3c6673.png">

jangan lupa aktifkan ```a2ensite penanjakan.semerue09.pw.conf``` dan ```service apache2 restart```

<img width="385" alt="30" src="https://user-images.githubusercontent.com/61228737/99065346-d95fd780-25d9-11eb-99f6-1044421ece38.png">

cek dengan membuka penanjakan.semerue09.pw pada browser

<img width="960" alt="31" src="https://user-images.githubusercontent.com/61228737/99065428-f5fc0f80-25d9-11eb-9fb6-264e3860007d.png">

## 11. Directory listing pada folder /public dibolehkan namun untuk folder yang berada di dalamnya tidak dibolehkan.
edit file /etc/apache2/sites-available/penanjakan.semerue09.pw.conf sebagai berikut:

<img width="385" alt="32" src="https://user-images.githubusercontent.com/61228737/99065698-5a1ed380-25da-11eb-8862-73d0dd8f7ac9.png">

coba kunjungi penanjakan.semerue09.pw/public/

<img width="960" alt="33" src="https://user-images.githubusercontent.com/61228737/99065734-6571ff00-25da-11eb-8e41-bc97e8eb56ab.png">

coba kunjungi penanjakan.semerue09.pw/public/javascripts/

<img width="960" alt="34" src="https://user-images.githubusercontent.com/61228737/99065727-6440d200-25da-11eb-85f5-c87e15df6df4.png">

## 12. Mengatasi HTTP Error code 404 dengan file custom /errors/404.html untuk mengganti error default 404 dari Apache
edit file /etc/apache2/sites-available/penanjakan.semerue09.pw.conf dengan menambahkan sebaris syntax sebagai berikut:

<img width="390" alt="35" src="https://user-images.githubusercontent.com/61228737/99066055-f47f1700-25da-11eb-899e-3b9e0212f1fb.png">

jangan lupa melakukan ```service apache2 restart```

coba kunjungi sebuah url yang tidak ada, contoh disini penanjakan.semerue09.pw/publics

<img width="960" alt="36" src="https://user-images.githubusercontent.com/61228737/99066063-f6e17100-25da-11eb-9615-a00ed3415f0c.png">

## 13. Url http://penanjakan.semerue09.pw/public/javascripts dibuatkan konfigurasi virtual host agar menjadi http://penanjakan.semerue09.pw/js
edit file /etc/apache2/sites-available/penanjakan.semerue09.pw.conf dengan menambahkan sebaris syntax sebagai berikut:

<img width="381" alt="37" src="https://user-images.githubusercontent.com/61228737/99066452-930b7800-25db-11eb-9de6-02612549624d.png">

jangan lupa melakukan ```service apache2 restart```

coba kunjungi penanjakan.semerue09.pw/js pada web browser apakah hasilnya sama dengan saat mengakses penanjakan.semerue09.pw/public/javascripts

<img width="960" alt="38" src="https://user-images.githubusercontent.com/61228737/99066459-94d53b80-25db-11eb-8b48-8ca15c84d631.png">

## 14. Web http://naik.gunung.semerue09.pw bisa diakses hanya dengan menggunakan port 8888
buat file /etc/apache2/sites-available/naik.gunung.semerue09.pw.conf dengan meng-copy file  /etc/apache2/sites-available/000-default.conf dan edit menjadi sebagai berikut:

<img width="388" alt="39" src="https://user-images.githubusercontent.com/61228737/99066897-50966b00-25dc-11eb-84ec-3620e3d00447.png">

edit pada file /etc/apache2/ports.conf tambahkan listen port 8888

<img width="378" alt="40" src="https://user-images.githubusercontent.com/61228737/99066902-52602e80-25dc-11eb-823d-81ebc0840050.png">

setelah edit, jalankan ```a2ensite naik.gunung.semerue09.pw.conf``` lalu ```service apache2 restart```

<img width="380" alt="41" src="https://user-images.githubusercontent.com/61228737/99066906-53915b80-25dc-11eb-95aa-fa67114b4b9b.png">

coba kunjungi naik.gunung.semerue09.pw:8888 untuk mengecek apakah sudah benar

<img width="960" alt="42" src="https://user-images.githubusercontent.com/61228737/99066911-555b1f00-25dc-11eb-8bc5-857ba3da8a9f.png">

## 15. Web http://naik.gunung.semerue09.pw diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung”
menggunakan fitur htpasswd, dengan syntax ```htpasswd -c /etc/apache2/.htpasswd semeru``` lalu akan diminta untuk mengisi password yang diinginkan untuk user semeru
bisa lakukan cek cengan syntax ```cat .htpasswd``` untuk melihat apakah user dan passwordnya sudah terekam

<img width="382" alt="43" src="https://user-images.githubusercontent.com/61228737/99067273-fea21500-25dc-11eb-8d2c-36be2a1db77e.png">

edit file /etc/apache2/sites-available/naik.gunung.semerue09.pw.conf sebagai berikut untuk menjalankan authentication

<img width="385" alt="44" src="https://user-images.githubusercontent.com/61228737/99067275-ffd34200-25dc-11eb-9f61-a20bf8f50470.png">

jangan lupa melakukan ```service apache2 restart```

coba kunjungi naik.gunung.semerue09.pw:8888 dan isikan login dengan benar

<img width="960" alt="46" src="https://user-images.githubusercontent.com/61228737/99067285-05c92300-25dd-11eb-86b0-3b6697fca229.png">


coba kunjungi naik.gunung.semerue09.pw:8888 pada browser dan tolak login

<img width="960" alt="45" src="https://user-images.githubusercontent.com/61228737/99067283-0497f600-25dd-11eb-8210-d2db5bf1d1bf.png">

## 16. IP PROBOLINGGO akan dialihkan secara otomatis ke http://semerue09.pw
sebelum diubah, begini tampilan jika mengunjungi IP PROBOLINGGO

<img width="960" alt="47" src="https://user-images.githubusercontent.com/61228737/99068058-62790d80-25de-11eb-9c0b-8de491d6a17c.png">

pada file /etc/apache2/sites-available/000-default.conf tambahkan syntax menjadi seperti di bawah ini

<img width="379" alt="48" src="https://user-images.githubusercontent.com/61228737/99068067-660c9480-25de-11eb-9a21-377899d0ac51.png">

jangan lupa melakukan ```service apache2 restart```

coba kunjungi IP PROBOLINGGO (10.151.71.84) pada browser dan cek apakah sudah langsung redirect ke semerue09.pw

<img width="960" alt="49" src="https://user-images.githubusercontent.com/61228737/99068068-673dc180-25de-11eb-95f1-5960a2abb50c.png">

## 17. Semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg
pada penanjakan.semerue09.pw/public/images/ terdapat 2 file gambar yang memiliki nama dengan substring "semeru", yaitu semeru.jpg dan bukansemeruaja.jpg
pada awal sebelum diubah, jika kita mengunjungi penanjakan.semerue09.pw/public/images/bukansemeruaja.jpg pada browser akan tampil seperti di bawah ini

<img width="960" alt="50" src="https://user-images.githubusercontent.com/61228737/99069856-bc2f0700-25e1-11eb-9936-447bc7194e11.png">

pastikan file /etc/apache2/sites-available/penanjakan.semerue09.pw.conf seperti di bawah ini

<img width="380" alt="51" src="https://user-images.githubusercontent.com/61228737/99069864-bf29f780-25e1-11eb-9758-353d372015b3.png">

jangan lupa melakukan ```service apache2 restart```

buat file .htaccess pada /var/www/penanjakan.semerue09.pw seperti di bawah ini

<img width="403" alt="52" src="https://user-images.githubusercontent.com/61228737/99069871-c0f3bb00-25e1-11eb-9c9c-96885fdeea42.png">


jika sudah, coba kunjungi lagi penanjakan.semerue09.pw/public/images/bukansemeruaja.jpg pada browser dan cek apakah sudah langsung diarahkan menuju semeru.jpg

<img width="960" alt="53" src="https://user-images.githubusercontent.com/61228737/99069873-c224e800-25e1-11eb-839a-cc59333b6960.png">
