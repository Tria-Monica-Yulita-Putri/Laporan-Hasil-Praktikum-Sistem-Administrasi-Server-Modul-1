## Laporan Hasil Praktikum Sistem Administrasi Server Modul 1

1. Pertama-tama yaitu Rename ubuntu_php5.6 terlebih dahulu menjadi ubuntu_landing

   ```markdown
   sudo lxc-copy -R ubuntu_php5.6 name -N ubuntu_landing
   ```

      ![1](https://user-images.githubusercontent.com/92940432/138595377-26a324e9-ae4a-49c8-b506-fef11b2145b0.jpeg)

      ![2](https://user-images.githubusercontent.com/92940432/138595384-e3788638-67fc-454e-8368-175065bbdb88.jpeg)



* Setelah mengganti nama menjadi ubuntu_landing. Maka selanjutnya yaitu coba menjalankan ubuntu_landing atau Start ubuntu_landing

  ```markdown
  sudo lxc-start -n ubuntu_landing -d
  ```

  ```markdown
  sudo lxc-attach -n ubuntu_landing
  ```

     ![3](https://user-images.githubusercontent.com/92940432/138595451-06d34fd4-f5db-4e3c-ba09-3f8f6b3329d7.jpeg)

  

* Setelah start ubuntu_landing, langkah selanjutnya yaitu mengganti ip di ubuntu_landing

  ```markdown
  nano /etc/network/interfaces 
  ```

   ![4](https://user-images.githubusercontent.com/92940432/138595455-45990994-fbbf-441e-876a-27b2a6ef908b.jpeg)


* Setelah mengganti ip di ubuntu_landing, maka disini terlihat bahwa Reboot dan ip telah terganti

  ```markdown
  reboot
  ```

   ![5](https://user-images.githubusercontent.com/92940432/138595478-df70535d-80a1-4bb9-867e-eba9a8c448ef.jpeg)

* Setelah reboot dan ip berganti dan ubuntu_landing berhasil. Maka, selanjutnya ping google untuk melihat apakah koneksi ntara komputer client dengan suatu komputer server yang terhubung dalam jaringan.

  ```markdown
  ping google.com
  ```

   ![6](https://user-images.githubusercontent.com/92940432/138595482-a01ccb53-9298-4ddb-81f8-0b2ce24d1da2.jpeg)



2. Step selanjutnya yaitu membuat dan mendownload debian_php_5.6

   ```markdown
   sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
   ```

   ![7](https://user-images.githubusercontent.com/92940432/138595543-4db31c8c-148c-4376-8885-1f2ff559fe73.jpeg)



* Setelah download dan membuat debian_php5.6, maka dapat dilihat disini, bahwa download debian_php5.6 berhasil

  ```markdown
  sudo lxc-ls -f (cek container)
  ```

   ![8](https://user-images.githubusercontent.com/92940432/138595545-5d1656f0-f71d-4e61-9d2f-3e45596d6eb4.jpeg)



* Setelah download debian_php5.6 berhasil, maka selanjutnya yaitu mencoba menjalankan debian_php5.6

  ```markdown
  sudo lxc-start -n debian_php5.6 -d
  ```

  ```markdown
  sudo lxc-attach -n debian_php5.6
  ```

   ![9](https://user-images.githubusercontent.com/92940432/138595550-b2f35134-be4e-4785-8caa-60e20c2f91b6.jpeg)



3. Setelah mencoba menjalankan debian_php5.6 dan berhasil dijalankan. Maka, langkah selanjutnya yaitu install net-tools pada debian_php5.6

   ```markdown
   apt install nano net-tools curl -y
   ```

   ![10](https://user-images.githubusercontent.com/92940432/138595557-668a1bcb-24f0-40b6-96a4-90bf24eddd49.jpeg)


* Setelah install net-tools pada debian_php5.6 berhasil. Selanjutnya yaitu setting ip pada debian_php5.6

  ```markdown
  nano /etc/network/interfaces
  ```

   ![11](https://user-images.githubusercontent.com/92940432/138595601-1717c5b6-b79e-4b37-b3c9-778740e256a4.jpeg)



* Setelah setting ip pada debian_php5.6 dan berhasil. Maka selanjutnya yaitu melihat ip yang  sudah di setting tersebut untuk melihat ip yang di punya oleh komputer. 

  ```markdown
  ifconfig
  ```

   ![12](https://user-images.githubusercontent.com/92940432/138595606-020b4fb8-0842-4a21-9f83-461d7bd9139d.jpeg)



* Setelah mengetahui ip komputer. Langkah selanjutnya yaitu install nginx di debian_php5.6 

  ```markdown
  apt install nginx nginx-extras -y
  ```

   ![13](https://user-images.githubusercontent.com/92940432/138595615-590c72a9-6295-4c6f-94db-bdd8900d6c59.jpeg)



* Setelah berhasil menginstall Nginx di debian_php5.6, selanjutnya yaitu  setting nginx

  ```markdown
  cd /etc/nginx/sites-available
  touch lxc_php5.6.dev
  nano lxc_php5.6.dev
  ```

  ![33](https://user-images.githubusercontent.com/92940432/138595733-86ed253b-157a-4cf2-b0da-4746c59a3584.jpeg)

  
  ```markdown
  cd ../sites-enabled
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev 
  nginx -t
  nginx -s reload
  ```

   ![14](https://user-images.githubusercontent.com/92940432/138595621-24f01c8b-4252-4ef5-aa5a-73bcb64d02a3.jpeg)

   ![15](https://user-images.githubusercontent.com/92940432/138595626-10fb7b24-1760-40bf-8216-98b3bb193a5a.jpeg)


* Selanjutnya yaitu setting hosts 

  ```markdown
  nano /etc/hosts
  ```

   ![16](https://user-images.githubusercontent.com/92940432/138595783-b7a9d69d-c6a9-46a7-91be-e297f1628d2f.jpeg)



* Setelah setting host. Maka selanjutnya yaitu setting index.html di debian_php5.6

  ```markdown
  lxc-attach -n debian_php5.6
  cd /var/www/html
  mkdir lxc_php5.6
  cp index.nginx-debian.html lxc_php5.6/index.html
  cd lxc_php5.6/
  ```

   ![17](https://user-images.githubusercontent.com/92940432/138595790-85d9af5a-e4d4-4177-a733-e794b5883fcb.jpeg)

  

* Setelah setting index.html di debian_php5.6 berhasil. Selanjutnya yaitu mengisi file di dalam index.html

  ```markdown
  nano index.html
  ```

   ![18](https://user-images.githubusercontent.com/92940432/138595795-24223b6c-b74f-4c74-b61c-bb4442987798.jpeg)

  

* Setelah mengisi file di dalam index.html, selanjutnya yaitu curl -I

  ```markdown
  curl -i http://lxc_php5.dev 
  ```

   ![19](https://user-images.githubusercontent.com/92940432/138595803-8b5b0868-b5f8-4798-a4a7-1a147e23fc0f.jpeg)

  

4. Langkah selanjutnya yaitu, masuk ke ubuntu_landing

   ```markdown
   sudo lxc-attach -n ubuntu_landing
   cd /etc/nginx/sites-available/
   ```

    ![20](https://user-images.githubusercontent.com/92940432/138595808-b6be5f94-967f-4d5e-8f46-2ec87e1d3416.jpeg)



* Setelah berhasil masuk ke ubuntu_landing. Maka selanjutnya yaitu setting lxc_landing

  ```markdown
  nano lxc_php5.6.dev
  ```

   ![21](https://user-images.githubusercontent.com/92940432/138595878-ea343706-083c-4ad1-b28b-803ea6140693.jpeg)


* Setelah setting lxc_landing berhasil, maka selanjutnya yaitu setting hosts landing

  ```markdown
  cd ../sites-enabled
  rm lxc_php5.6.dev
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev
  nginx -t
  nginx -s reload
  ```

   ![22](https://user-images.githubusercontent.com/92940432/138595885-c6e61b96-7b06-4f9d-8772-2a5f3277df80.jpeg)



* Selanjutnya cek hosts landing yang sudah disetting

  ```markdown
  nano /etc/hosts
  ```

   ![23](https://user-images.githubusercontent.com/92940432/138595889-d037d6e6-be22-4c70-afc2-36d81be4fc13.jpeg)

  

* Setelah cek host landing yang sudah disetting, selanjutnya yaitu masuk index.html

  ```markdown
  cd /var/www/html/
  ```

   ![24](https://user-images.githubusercontent.com/92940432/138595882-35dce101-4b89-4b3a-a16a-fd66b4bd9d22.jpeg)



* Setelah masuk ke index.html, maka selanjutnya yaitu kita seeting file index landing

  ```markdown
  nano index.html
  ```

    ![25](https://user-images.githubusercontent.com/92940432/138595899-ae11bb90-080b-4f01-9126-33720118f897.jpeg)



* Setelah berhasil setting di file index landing, maka selanjutnya ketik curl I lxc landing. Dimana untuk membuat setup nginx pada ubuntu_landing

  ```markdown
  curl -i http://lxc_landing.dev 
  ```

    ![26](https://user-images.githubusercontent.com/92940432/138595971-8840f06f-7f76-470f-88a5-686c88930755.jpeg)



5. Langkah selanjutnya yaitu, Lxc ubuntu_landing harus auto start ketika vm dinyalakan, supaya menjaga website company profile tidak mengalami downtime

   ```markdown
   lxc-ls -f
   echo “lxc.start.auto =1” >> /var/lib/lxc/ubuntu_landing/config
   lxc-ls -f
   
   ```

    ![29](https://user-images.githubusercontent.com/92940432/138595980-433b240d-5e41-4d87-9850-337b382f069e.jpeg)

   

6. Langkah selanjutnya yaitu, setup nginx pada vm.local dimana digunakan untuk mengatur proxy_pass

   ```markdown
   sudo nano /etc/hosts
   ```

    ![28](https://user-images.githubusercontent.com/92940432/138595977-ce747c0b-b1df-461f-b82f-26489a8eafc7.jpeg)



* Selanjutnya yaitu, jalankan ubuntu_php7.4

  ```markdown
  sudo lxc-start -n ubuntu_php7.4
  sudo lxc-start -n ubuntu_php5.6
  lxc-ls -f
  ```

   ![27](https://user-images.githubusercontent.com/92940432/138595973-22b5f9b6-c637-4117-b9c8-c6a89316eaf5.jpeg)



* Selanjutnya yaitu masuk ke vm lokal

  ```markdown
  cd /etc/nginx/sites-available/
  ```

    ![30](https://user-images.githubusercontent.com/92940432/138595984-fb2e90ff-87e1-4c86-82db-8a317c84fed4.jpeg)



* Setelah masuk ke vm lokal, maka selanjutnya yaitu kita setting vm lokal

  ```markdown
  sudo nano vm.local
  ```

   ![31](https://user-images.githubusercontent.com/92940432/138596044-551461b0-c5bc-4be4-b664-84b3ea48c43c.jpeg)



* Setelah setting vm lokal. Maka, selanjutnya yaitu curl vm lokal

  ````markdown
  cd ../sites-enabled/
  sudo ln /etc/nginx/sites-available/vm.local
  sudo nginx -t
  sudo nginx -s reload
  curl -I http://vm.local
  ````

   ![32](https://user-images.githubusercontent.com/92940432/138596046-7f7d9817-e667-4413-a2d5-b90e963ababa.jpeg)

  

7. Langkah terakhir, yaitu mengakses tiga url :

*  [http://vm.local](http://vm.local/) akan diarahkan ke http://lxc_landing.dev

   ![34](https://user-images.githubusercontent.com/92940432/138596122-944f83db-f39d-4f45-8c3f-cec24f58e68e.jpeg)

*  http://vm.local/blog akan diarahkan ke http://lxc_php7.dev

   ![35](https://user-images.githubusercontent.com/92940432/138596128-5ccba9a3-68cc-4f93-be23-9f82041af44c.jpeg)

* http://vm.local/app akan diarahkan ke http://lxc_php5.dev

   ![36](https://user-images.githubusercontent.com/92940432/138596132-c7257d48-c4ae-41d5-ac86-97df6098bfb3.jpeg)

  

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

     

     

     

     
