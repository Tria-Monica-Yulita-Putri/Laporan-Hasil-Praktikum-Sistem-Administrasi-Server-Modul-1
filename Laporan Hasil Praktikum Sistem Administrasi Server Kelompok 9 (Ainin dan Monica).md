## Laporan Hasil Praktikum Sistem Administrasi Server

1. Pertama-tama yaitu Rename ubuntu_php5.6 terlebih dahulu menjadi ubuntu_landing

   ```markdown
   sudo lxc-copy -R ubuntu_php5.6 name -N ubuntu_landing
   ```

![](C:\Users\TRIA YULITA\Downloads\SAS\1.jpeg)

![](C:\Users\TRIA YULITA\Downloads\SAS\2.jpeg)



* Setelah mengganti nama menjadi ubuntu_landing. Maka selanjutnya yaitu coba menjalankan ubuntu_landing atau Start ubuntu_landing

  ```markdown
  sudo lxc-start -n ubuntu_landing -d
  ```

  ```markdown
  sudo lxc-attach -n ubuntu_landing
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\3.jpeg)

  

* Setelah start ubuntu_landing, langkah selanjutnya yaitu mengganti ip di ubuntu_landing

  ```markdown
  nano /etc/network/interfaces 
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\4.jpeg)



* Setelah mengganti ip di ubuntu_landing, maka disini terlihat bahwa Reboot dan ip telah terganti

  ```markdown
  reboot
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\5.jpeg)

* Setelah reboot dan ip berganti dan ubuntu_landing berhasil. Maka, selanjutnya ping google untuk melihat apakah koneksi ntara komputer client dengan suatu komputer server yang terhubung dalam jaringan.

  ```markdown
  ping google.com
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\6.jpeg)



2. Step selanjutnya yaitu membuat dan mendownload debian_php_5.6

   ```markdown
   sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
   ```

![](C:\Users\TRIA YULITA\Downloads\SAS\7.jpeg)



* Setelah download dan membuat debian_php5.6, maka dapat dilihat disini, bahwa download debian_php5.6 berhasil

  ```markdown
  sudo lxc-ls -f (cek container)
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\8.jpeg)



* Setelah download debian_php5.6 berhasil, maka selanjutnya yaitu mencoba menjalankan debian_php5.6

  ```markdown
  sudo lxc-start -n debian_php5.6 -d
  ```

  ```markdown
  sudo lxc-attach -n debian_php5.6
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\9.jpeg)



3. Setelah mencoba menjalankan debian_php5.6 dan berhasil dijalankan. Maka, langkah selanjutnya yaitu install net-tools pada debian_php5.6

   ```markdown
   apt install nano net-tools curl -y
   ```

![](C:\Users\TRIA YULITA\Downloads\SAS\10.jpeg)



* Setelah install net-tools pada debian_php5.6 berhasil. Selanjutnya yaitu setting ip pada debian_php5.6

  ```markdown
  nano /etc/network/interfaces
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\11.jpeg)



* Setelah setting ip pada debian_php5.6 dan berhasil. Maka selanjutnya yaitu melihat ip yang  sudah di setting tersebut untuk melihat ip yang di punya oleh komputer. 

  ```markdown
  ifconfig
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\12.jpeg)



* Setelah mengetahui ip komputer. Langkah selanjutnya yaitu install nginx di debian_php5.6 

  ```markdown
  apt install nginx nginx-extras -y
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\13.jpeg)



* Setelah berhasil menginstall Nginx di debian_php5.6, selanjutnya yaitu  setting nginx

  ```markdown
  cd /etc/nginx/sites-available
  touch lxc_php5.6.dev
  nano lxc_php5.6.dev
  ```

  ![](C:\Users\TRIA YULITA\Downloads\WhatsApp Image 2021-10-24 at 19.04.07.jpeg)

  
  
  ```markdown
  cd ../sites-enabled
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev 
  nginx -t
  nginx -s reload
  ```

![](C:\Users\TRIA YULITA\Downloads\SAS\14.jpeg)

![](C:\Users\TRIA YULITA\Downloads\SAS\15.jpeg)



* Selanjutnya yaitu setting hosts 

  ```markdown
  nano /etc/hosts
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\16.jpeg)



* Setelah setting host. Maka selanjutnya yaitu setting index.html di debian_php5.6

  ```markdown
  lxc-attach -n debian_php5.6
  cd /var/www/html
  mkdir lxc_php5.6
  cp index.nginx-debian.html lxc_php5.6/index.html
  cd lxc_php5.6/
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\17.jpeg)

  

* Setelah setting index.html di debian_php5.6 berhasil. Selanjutnya yaitu mengisi file di dalam index.html

  ```markdown
  nano index.html
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\18.jpeg)

  

* Setelah mengisi file di dalam index.html, selanjutnya yaitu curl -I

  ```markdown
  curl -i http://lxc_php5.dev 
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\19.jpeg)

  

4. Langkah selanjutnya yaitu, masuk ke ubuntu_landing

   ```markdown
   sudo lxc-attach -n ubuntu_landing
   cd /etc/nginx/sites-available/
   ```

   ![](C:\Users\TRIA YULITA\Downloads\SAS\20.jpeg)



* Setelah berhasil masuk ke ubuntu_landing. Maka selanjutnya yaitu setting lxc_landing

  ```markdown
  nano lxc_php5.6.dev
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\21.jpeg)



* Setelah setting lxc_landing berhasil, maka selanjutnya yaitu setting hosts landing

  ```markdown
  cd ../sites-enabled
  rm lxc_php5.6.dev
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev
  nginx -t
  nginx -s reload
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\22.jpeg)



* Selanjutnya cek hosts landing yang sudah disetting

  ```markdown
  nano /etc/hosts
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\23.jpeg)

  

* Setelah cek host landing yang sudah disetting, selanjutnya yaitu masuk index.html

  ```markdown
  cd /var/www/html/
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\24.jpeg)



* Setelah masuk ke index.html, maka selanjutnya yaitu kita seeting file index landing

  ```markdown
  nano index.html
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\25.jpeg)



* Setelah berhasil setting di file index landing, maka selanjutnya ketik curl I lxc landing. Dimana untuk membuat setup nginx pada ubuntu_landing

  ```markdown
  curl -i http://lxc_landing.dev 
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\26.jpeg)



5. Langkah selanjutnya yaitu, Lxc ubuntu_landing harus auto start ketika vm dinyalakan, supaya menjaga website company profile tidak mengalami downtime

   ```markdown
   lxc-ls -f
   echo “lxc.start.auto =1” >> /var/lib/lxc/ubuntu_landing/config
   lxc-ls -f
   
   ```

   ![](C:\Users\TRIA YULITA\Downloads\SAS\29.jpeg)

   

6. Langkah selanjutnya yaitu, setup nginx pada vm.local dimana digunakan untuk mengatur proxy_pass

   ```markdown
   sudo nano /etc/hosts
   ```

   ![](C:\Users\TRIA YULITA\Downloads\SAS\28.jpeg)



* Selanjutnya yaitu, jalankan ubuntu_php7.4

  ```markdown
  sudo lxc-start -n ubuntu_php7.4
  sudo lxc-start -n ubuntu_php5.6
  lxc-ls -f
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\27.jpeg)



* Selanjutnya yaitu masuk ke vm lokal

  ```markdown
  cd /etc/nginx/sites-available/
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\30.jpeg)



* Setelah masuk ke vm lokal, maka selanjutnya yaitu kita setting vm lokal

  ```markdown
  sudo nano vm.local
  ```

  ![](C:\Users\TRIA YULITA\Downloads\SAS\31.jpeg)



* Setelah setting vm lokal. Maka, selanjutnya yaitu curl vm lokal

  ````markdown
  cd ../sites-enabled/
  sudo ln /etc/nginx/sites-available/vm.local
  sudo nginx -t
  sudo nginx -s reload
  curl -I http://vm.local
  ````

  ![](C:\Users\TRIA YULITA\Downloads\SAS\32.jpeg)

  

7. Langkah terakhir, yaitu mengakses tiga url :

*  [http://vm.local](http://vm.local/) akan diarahkan ke http://lxc_landing.dev

  ![](C:\Users\TRIA YULITA\Downloads\WhatsApp Image 2021-10-24 at 19.12.13.jpeg)

*  http://vm.local/blog akan diarahkan ke http://lxc_php7.dev

  ![](C:\Users\TRIA YULITA\Downloads\WhatsApp Image 2021-10-24 at 19.11.16.jpeg)

* http://vm.local/app akan diarahkan ke http://lxc_php5.dev

  ![](C:\Users\TRIA YULITA\Downloads\WhatsApp Image 2021-10-24 at 19.11.16 (1).jpeg)

  

8. Menyiapkan analisa untuk diserahkan ke CTO 

   * Mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?

     Jawab : 

     * Karena paket-paket untuk ubuntu 16.04 akan dihapus segera setelah diberitahukan, biasanya dalam waktu yang bersamaan rilis php akan dipublikasikan karena tidak mungkin menambah paket lagi. 
     * Karena paket untuk ubuntu 16.04 akan tersedia melalui PHP LTS oleh program berbayar Feexian. Ini merupakan opsi yang lebih murah daripada repositori pribadi yang diberitahukan sebelumnya. 

   * Kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?

     Jawab : 

     * Karena LXC merupakah sebuah teknologi virtualisasi yang ringan dan tentunya sudah menyediakan sebuah sistem virtualisasi perangkat lunak yang gratis untuk komputer dalam menjalankan GNU/Linux. Hal tersebut dilakukan melalui isolasi level kernel, dimana pengguna dalam menjalankan sebuah beberapa unit virtual (wadah) dapat dilakukan secara bersamaan pada host yang sama. LXC juga memiliki kelebihan dimana LXC sudah tersedia di kernel linux, jadi pengguna bisa dapat langsung menggunakannya tanpa harus membutuhkan sebuah kernel yang khusus. 

   * Apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?

     Jawab : 

      - Proxy server adalah sebuah program komputer yang dapat bekerja sebagai perantara jaringan. Proxy server biasanya digunakan untuk meningkatkan proteksi atau mengontrol dan memonitor seluruh aktivitas jaringan dalam mengakses internet.
     - Karena dalam pemanfaatan VM local, inerja server tidak jauh beda dengan server fisik. VM local dapat membuat server lebih dari satu hanya dengan menggunakan satu VM local. Dan dalam pembuatan virtual server, juga menerapkan teknologi proxy server dimana proxy server berguna untuk mengontrol dan memblokir sebuah aktivitas jaringan jikalau ada situs-situs terlarang. 

     

     

     

     
