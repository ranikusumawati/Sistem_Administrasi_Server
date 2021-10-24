1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema yang baru

   1.1 Menampikan Container sebelum dirubah 

   ```
   	  sudo lxc-ls -f
   ```
   
   ![1.1](C:\Users\USEER\Documents\Gambar\1.1.jpeg)

​		1.2 Kode ini untuk menyalin daripada mengubah nama container dari ubuntu_php5.6 menjadi    ubuntu_landing.

 		     sudo lxc-copy -R -n ubuntu_php5.6 -N ubuntu_landing

![1.2](C:\Users\USEER\Documents\Gambar\1.2.PNG)

​        1.3 Menampikan Container setelah dirubah	

```
sudo lxc-ls -f
```

​                ![1.3](C:\Users\USEER\Documents\Gambar\1.3.jpeg)

​        1.4 Start Ubuntu landing

```
sudo lxc-start ubuntu_landing
```

​               

![1.4](C:\Users\USEER\Documents\Gambar\1.4.PNG)

​        1.5 Masuk ke root ubuntu_landing container

```
 sudo lxc-attach ubuntu_landing
```

​			 

![1.5](C:\Users\USEER\Documents\Gambar\1.5.PNG)



​        1.6 Setting IP yang mengikuti skema baru

```
 nano /etc/network/interfaces
```

​                                            ![1.6](C:\Users\USEER\Documents\Gambar\1.6.PNG)



​        1.7 Restart container

```
    shutdown now

    sudo lxc-start ubuntu_landing
```

​				

![1.7](C:\Users\USEER\Documents\Gambar\1.7.PNG)

​        1.8 Setelah Restart lalu check IP apakh sudah berubah

```
 	lxc-attach ubuntu_landing

	ifconfig
```

​              

![1.8](C:\Users\USEER\Documents\Gambar\1.8.PNG)

​             Dan IP sudah berubah menjadi 10.0.3.103

Inilah step bagaimana merename ubuntu_php5.6 menjadi ubuntu_landing, serta merubah IP mengikuti skema yang baru.



2. Install lxc debian 9 dengan nama debian_php5.6

   2.1 Install lxc debian 9

   ```
   sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
   ```
   
   
   
   ![2.1](C:\Users\USEER\Documents\Gambar\2.1.PNG)
   
   

​       2.2 Cek container apakah sudah berhasil terinstall

```
	Sudo lxc-ls -f 
```

![2.2](C:\Users\USEER\Documents\Gambar\2.2.PNG)



​       2.3 Start debian_php 5.6

```
    Sudo lxc-start -n debian_php5.6 -d

    Sudo lxc-attach -n debian_php5.6
```

​				

![2.3](C:\Users\USEER\Documents\Gambar\2.3.PNG)



3. Setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

   3.1 Pertama cek apakah ubuntu_php5.6 berjalan, setelah itu install nginx

   ```
   sudo apt install nginx nginx-extras
   ```

   ![3.1](C:\Users\USEER\Documents\Gambar\3.1.PNG)

   3.2 Setelah itu install net tools

   ```
   apt install nano net-tools curl
   ```
   
   ​	  
   
   ![3.2](C:\Users\USEER\Documents\Gambar\3.2.PNG)

​       3.3 Lalu kita harus setting IP 

```
	nano /etc/network/interfaces
```

![3.3](C:\Users\USEER\Documents\Gambar\3.3.PNG)

​      3.4 Lalu restart kontainer

​             Pertama reboot, setelah itu buka ifconfig untuk mengecek apakah IP telah berubah atau tidak.

![3.4](C:\Users\USEER\Documents\Gambar\3.4.PNG)

​      3.5 Setting nginx

​			Setelah itu setting nginx ikuti kode dibawah ini:

![3.5](C:\Users\USEER\Documents\Gambar\3.5.PNG)

​      3.6 Mulai nano untuk konfigurasi

```
			nano lxc_php5.6.dev
```

![3.6](C:\Users\USEER\Documents\Gambar\3.6.PNG)

​      3.7 Setting hosts

```
             nano /etc/hosts
```

![3.7](C:\Users\USEER\Documents\Gambar\3.7.PNG)

```
nano index.html
```

​                            ![3.7.1](C:\Users\USEER\Documents\Gambar\3.7.1.PNG)

​     3.8 Setelah itu, kita membutuhkan untuk mengecek code di index.html

![3.8](C:\Users\USEER\Documents\Gambar\3.8.PNG)

​     3.9 Setelah itu curl -i

```
          curl -i http://lxc_php5.dev 
```

 ![3.9](C:\Users\USEER\Documents\Gambar\3.9.PNG)

Yang dapat kita simpulkan yaitu kita membutuhkan memasukkan cd lxc_php5.6 sebelum kita memasukkan nano index.html

4. Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc

   Langkahnya seperti nomer 3

   4.1 Ikuti Langkah-langkah dibawah ini :

   ![4.1.1](C:\Users\USEER\Documents\Gambar\4.1.1.PNG)
   
   ![4.1.2](C:\Users\USEER\Documents\Gambar\4.1.2.PNG)
   
   ![4.1.3](C:\Users\USEER\Documents\Gambar\4.1.3.PNG)
   
   ![4.1.4](C:\Users\USEER\Documents\Gambar\4.1.4.PNG)
   
   ![4.1.5](C:\Users\USEER\Documents\Gambar\4.1.5.PNG)
   
   ![4.1.6](C:\Users\USEER\Documents\Gambar\4.1.6.PNG)
   
   

   4. 2 Lalu kita membutuhkan untuk mengecek command curl

      ```
      			curl -i http://lxc_landing.dev
      ```

![4.2](C:\Users\USEER\Documents\Gambar\4.2.PNG)

5. LXC ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website company profile tidak mengalami *downtime*

   5.1 Masuk ke Super User atau Sudo su untuk masuk halaman config

```
    sudo su
    cd /var/lib/lxc/ubuntu_landing
    nano config
```

![5.1](C:\Users\USEER\Documents\Gambar\5.1.PNG)

​       5.2 Lalu tambahkan 

```
    lxc.start.auto = 1
```

![5.2](C:\Users\USEER\Documents\Gambar\5.2.PNG)

​       5.3 Keluar dari super user lalu reboot

```
	 reboot
```

![5.3](C:\Users\USEER\Documents\Gambar\5.3.PNG)

​        5.4 Lalu cek ubuntu_landing autostart telah berjalan atau tidak. jika autostart telah berjalan, autostart akan berubah dari '0' ke '1'

```
	sudo lxc-ls -f
```

![5.4](C:\Users\USEER\Documents\Gambar\5.4.PNG)

6. Setup nginx pada vm.local untuk mengatur *proxy_pass* dimana :

   6.1 Masuk pada nano

```
	sudo nano /etc/hosts
```

![6.1](C:\Users\USEER\Documents\Gambar\6.1.PNG)

​        6.2 Setelah itu kita harus install nginx, lalu mulai directory bagian yang available,lalu mulai nano vm.local dan edit nano vm.local

```
    sudo apt install nginx nginx-extras
    cd /etc/nginx/sites-available
    sudo touch vm.local
    sudo nano vm.local
```

![6.2](C:\Users\USEER\Documents\Gambar\6.2.PNG)

​      6.3 Setelah itu masuk pada directory bagian enabled, jika nginx gagal untuk di dimulai, jalankan sudo nginx-t untuk menemukannya jika ada kesalahan dengan konfigurasi file. Jika nginx error di beberapa konfigurasi file, ulangi dan tetap jalankan configurasi file sebelumnya.

```
    cd ../sites-enabled
    sudo nginx -t
    sudo nginx -s reload
```

​	  6.4 Mengakses [http://vm.local](http://vm.local/) akan diarahkan ke http://lxc_landing.dev

```
	curl -i http://vm.local/blog
```

![6.4](C:\Users\USEER\Documents\Gambar\6.4.PNG)

​      6.5 Mengakses http://vm.local/blog akan diarahkan ke http://lxc_php7.dev

```
	curl -i http://vm.local/
```

![6.5](C:\Users\USEER\Documents\Gambar\6.5.PNG)

​      6.6 Mengakses http://vm.local/app  akan diarahkan ke http://lxc_php5.dev

```
	curl -i http://vm.local/app
```

![6.6](C:\Users\USEER\Documents\Gambar\6.6.PNG)

7. Untuk kebutuhan presentasi mereka, browser di laptop mereka harus dapat mengakses ketiga url tersebut.

```
	http://vm.local/
```

![7.1](C:\Users\USEER\Documents\Gambar\7.1.PNG)

```
	http://vm.local/app
```

![image-20211024232004216](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024232004216.png)

```
	http://vm.local/blog
```

![7.3](C:\Users\USEER\Documents\Gambar\7.3.PNG)

### Analysis

1. Why we can't use ubuntu 16.04 for php5.6 needs, and we have to change the OS to debian 9?
2. Why we have to use LXC Virtualization for website scheme that will be developed?
3. What is a proxy server? Why we think of vm.local as a proxy server?

### Answer of the Analysis

1. Karena ubuntu 16.04 telah beralih ke PHP 7.0 dengan infrastruktur baru untuk paket PHP. Jadi, tidak, Anda tidak dapat menginstal php5 pada Ubuntu 16.04
2. LXC memberikan kemudahan dalam penerapan dan kinerja yang digunakan sangatlah ringan karena hanya memerlukan aplikasi pendukung yang diperlukan saja dalam pengoprasiannya
3. Server proxy adalah aplikasi server yang bertindak sebagai perantara antara klien yang meminta sumber daya dan server yang menyediakan sumber daya itu. Vm.local disebut sebagai server proxy karena vm local jembatan untuk menghubungkan internet