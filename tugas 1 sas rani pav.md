# Laporan Praktikum 1

## Kelompok 3


**1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema yang baru**
	a. Menampikan Container sebelum dirubah
		```
      		sudo lxc-ls -f
      		```
![1 fix](C:\Users\USEER\Downloads\1 fix.jpeg)
	1.2 Kode ini untuk menyalin daripada mengubah nama container dari ubuntu_php5.6 menjadi ubuntu_landing.

 		sudo lxc-copy -R -n ubuntu_php5.6 -N ubuntu_landing

![image-20211024190208627](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024190208627.png)

	1.3 Menampikan Container setelah dirubah	

		sudo lxc-ls -f

![1.1f](C:\Users\USEER\Downloads\1.1f.jpeg)



​        1.4 Start Ubuntu landing

		sudo lxc-start ubuntu_landing

![](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024190344879.png)

​        1.5 Masuk ke root ubuntu_landing container

​			  sudo lxc-attach ubuntu_landing

![image-20211024190514738](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024190514738.png)

​        1.6 Setting IP yang mengikuti skema baru

​               nano /etc/network/interfaces

![image-20211024191256525](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024191256525.png)

​        1.7 Restart container

​				shutdown now

​				sudo lxc-start ubuntu_landing

![image-20211024191906084](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024191906084.png)

​        1.8 Setelah Restart lalu check IP apakh sudah berubah

​               lxc-attach ubuntu_landing

​               ifconfig

![image-20211024192907362](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024192907362.png)

​             Dan IP sudah berubah menjadi 10.0.3.103

Inilah step bagaimana merename ubuntu_php5.6 menjadi ubuntu_landing, serta merubah IP mengikuti skema yang baru.



2. Install lxc debian 9 dengan nama debian_php5.6

   2.1 Install lxc debian 9

   sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org

   ![image-20211024193638291](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024193638291.png)

​       2.2 Cek container apakah sudah berhasil terinstall

​       Sudo lxc-ls -f 

![image-20211024200042885](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024200042885.png)

​       2.3 Start debian_php 5.6

​				Sudo lxc-start -n debian_php5.6 -d

​			    Sudo lxc-attach -n debian_php5.6

![image-20211024201325655](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024201325655.png)



3. Setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

   3.1 Pertama cek apakah ubuntu_php5.6 berjalan, setelah itu install nginx

   ​	  sudo apt install nginx nginx-extras

   ![image-20211024200944627](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024200944627.png)

   3.2 Setelah itu install net tools

   ​	  apt install nano net-tools curl

   ![image-20211024202229659](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024202229659.png)

​       3.3 Lalu kita harus setting IP 

​			 nano /etc/network/interfaces

![image-20211024202637080](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024202637080.png)

​      3.4 Lalu restart kontainer

​             Pertama reboot, setelah itu buka ifconfig untuk mengecek apakah IP telah berubah atau tidak.

![image-20211024202741756](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024202741756.png)

​      3.5 Setting nginx

​			Setelah itu setting nginx ikuti kode dibawah ini:

![image-20211024203721823](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024203721823.png)

​      3.6 Mulai nano untuk konfigurasi

```
			nano lxc_php5.6.dev
```

![image-20211024204608264](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024204608264.png)

​      3.7 Setting hosts

```
             nano /etc/hosts
```

​     ![image-20211024204452250](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024204452250.png)

```
nano index.html
```

​           ![image-20211024205019655](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024205019655.png)

​     3.8 Setelah itu, kita membutuhkan untuk mengecek code di index.html

![image-20211024205215486](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024205215486.png)

​     3.9 Setelah itu curl -i

```
          curl -i http://lxc_php5.dev 
```

  ![image-20211024210429614](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024210429614.png)

Yang dapat kita simpulkan yaitu kita membutuhkan memasukkan cd lxc_php5.6 sebelum kita memasukkan nano index.html

4. Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc

   Langkahnya seperti nomer 3

   4.1 Ikuti Langkah-langkah dibawah ini :

   ![image-20211024213855650](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024213855650.png)

![image-20211024213956223](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024213956223.png)

![image-20211024214300936](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024214300936.png)

![image-20211024214353558](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024214353558.png)

![image-20211024214432926](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024214432926.png)

![image-20211024214457380](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024214457380.png)

   4. 2 Lalu kita membutuhkan untuk mengecek command curl

      ```
      			curl -i http://lxc_landing.dev
      ```

![image-20211024214621591](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024214621591.png)

5. LXC ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website company profile tidak mengalami *downtime*

   5.1 Masuk ke Super User atau Sudo su untuk masuk halaman config

```
    sudo su
    cd /var/lib/lxc/ubuntu_landing
    nano config
```

![image-20211024215223823](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024215223823.png)

​       5.2 Lalu tambahkan 

```
    lxc.start.auto = 1
```

![image-20211024215316449](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024215316449.png)

​       5.3 Keluar dari super user lalu reboot

```
	 reboot
```

![image-20211024215626321](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024215626321.png)

​        5.4 Lalu cek ubuntu_landing autostart telah berjalan atau tidak. jika autostart telah berjalan, autostart akan berubah dari '0' ke '1'

```
	sudo lxc-ls -f
```

![image-20211024215822864](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024215822864.png)

6. Setup nginx pada vm.local untuk mengatur *proxy_pass* dimana :

   6.1 Masuk pada nano

```
	sudo nano /etc/hosts
```

![image-20211024220135827](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024220135827.png)

​        6.2 Setelah itu kita harus install nginx, lalu mulai directory bagian yang available,lalu mulai nano vm.local dan edit nano vm.local

```
    sudo apt install nginx nginx-extras
    cd /etc/nginx/sites-available
    sudo touch vm.local
    sudo nano vm.local
```

![image-20211024220624494](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024220624494.png)

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

![image-20211024221944292](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024221944292.png)

​      6.5 Mengakses http://vm.local/blog akan diarahkan ke http://lxc_php7.dev

```
	curl -i http://vm.local/
```

![image-20211024222031497](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024222031497.png)

​      6.7 Mengakses http://vm.local/app  akan diarahkan ke http://lxc_php5.dev

```
	curl -i http://vm.local/app
```

![image-20211024222008751](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024222008751.png)

7. Untuk kebutuhan presentasi mereka, browser di laptop mereka harus dapat mengakses ketiga url tersebut.

```
	http://vm.local/
```

![image-20211024222222224](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024222222224.png)

```
	http://vm.local/app
```

![image-20211024222259232](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024222259232.png)

```
	http://vm.local/blog
```

![image-20211024222334095](C:\Users\USEER\AppData\Roaming\Typora\typora-user-images\image-20211024222334095.png)

### Analysis

1. Why we can't use ubuntu 16.04 for php5.6 needs, and we have to change the OS to debian 9?
2. Why we have to use LXC Virtualization for website scheme that will be developed?
3. What is a proxy server? Why we think of vm.local as a proxy server?

### Answer of the Analysis

1. Karena ubuntu 16.04 telah beralih ke PHP 7.0 dengan infrastruktur baru untuk paket PHP. Jadi, tidak, Anda tidak dapat menginstal php5 pada Ubuntu 16.04
2. LXC memberikan kemudahan dalam penerapan dan kinerja yang digunakan sangatlah ringan karena hanya memerlukan aplikasi pendukung yang diperlukan saja dalam pengoprasiannya
3. Server proxy adalah aplikasi server yang bertindak sebagai perantara antara klien yang meminta sumber daya dan server yang menyediakan sumber daya itu. Vm.local disebut sebagai server proxy karena vm local jembatan untuk menghubungkan internet
