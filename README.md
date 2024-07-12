# PA-PC_202231056_RAHMI-NUR-HIDAYAH_C
## UAS PENGOLAHAN CITRA DIGITAL C
### SIGMENTASI DAUN

#### Tahap Pengerjaan Proyek :
Di sini, gambar yang akan saya oleh adalah hasil jepretan saya sendiri dan telah saya simpan dalam folder yang sama dengan file Python saya. Berikut adalah langkah-langkah pengolahannya :
##### Import CV
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
Untuk melakukan pemrosesan dan visualisasi gambar, saya menggunakan pustaka OpenCV, NumPy, dan Matplotlib dalam bahasa pemrograman Python. Pertama-tama, pustaka-pustaka tersebut diimpor dengan perintah import cv2, import numpy as np, dan import matplotlib.pyplot as plt, di mana cv2 digunakan untuk operasi pemrosesan gambar, np digunakan untuk operasi numerik, dan plt digunakan untuk visualisasi data. 
##### Mengimpor Gambar
```bash
image = cv2.imread('nanas.png')
```
Disini saya menggunakan gambar 'nanas.png' sebagai objek dalam pemrosesan menggunakan pustaka OpenCV. Gambar ini dibaca menggunakan fungsi cv2.imread('nanas.png'). 
##### Konversi Gambar dari Format BRG ke HSV
```bash
hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
```
Di sini, saya mengubah format warna gambar menggunakan OpenCV dari BGR ke HSV (Hue, Saturation, Value). Dalam format HSV, 'Hue' mencerminkan warna asli, 'Saturation' mengatur kecerahan warna, dan 'Value' mengendalikan intensitas cahaya dalam gambar. 
##### Mendefinisikan Batas Bawah dan Batas Atas untuk Warna Kuning (NANAS)
```bash
lower_yellow = np.array([0, 50, 100], dtype="uint8")
upper_yellow = np.array([30, 255, 255], dtype="uint8")
```
Disini, saya menentukan rentang warna kuning untuk buah nanasnya dalam format HSV menggunakan NumPy. Variabel lower_yellow dan upper_yellow adalah array NumPy yang kita gunakan untuk menetapkan batas bawah dan atas dari rentang warna kuning yang ingin kita identifikasi dalam gambar. Pada lower_yellow, nilai [0, 50, 100] menunjukkan nilai minimum untuk setiap komponen HSV: Hue (0-30), Saturation (50-255), dan Value (100-255). Sedangkan pada upper_yellow, nilai [30, 255, 255] menunjukkan nilai maksimum untuk setiap komponen HSV: Hue (0-30), Saturation (50-255), dan Value (100-255).
##### Mendefinisikan Batas Bawah dan Batas Atas untuk Warna Hijau (DAUN)
```bash
lower_green = np.array([31, 60, 5], dtype="uint8")
upper_green = np.array([150, 255, 255], dtype="uint8")
```
Di sini, saya mendefinisikan rentang warna hijau dalam format HSV (Hue, Saturation, Value). Variabel lower_green dan upper_green adalah array NumPy yang digunakan untuk menetapkan batas bawah dan atas dari rentang warna hijau yang ingin diidentifikasi dalam gambar. Pada variabel lower_green, nilai [31, 60, 5] menunjukkan nilai minimum untuk setiap komponen HSV: Hue (31-150), Saturation (60-255), dan Value (5-255). Sedangkan pada variabel upper_green, nilai [150, 255, 255] menunjukkan nilai maksimum untuk setiap komponen HSV: Hue (31-150), Saturation (60-255), dan Value (5-255).
##### Membuat Masker untuk Pixel Kuning dan Hijau
```bash
mask_pineapple = cv2.inRange(hsv_image, lower_yellow, upper_yellow)
mask_leaves = cv2.inRange(hsv_image, lower_green, upper_green)
```
Untuk membuat masker warna dalam format HSV (Hue, Saturation, Value) menggunakan pustaka OpenCV disini
Pertama, saya menggunakan `cv2.inRange(hsv_image, lower_yellow, upper_yellow)`untuk membuat masker yang memisahkan bagian gambar yang berada dalam rentang warna kuning yang telah ditentukan oleh `lower_yellow` dan `upper_yellow`. Masker ini akan menghasilkan citra biner di mana piksel yang berada dalam rentang warna kuning akan memiliki nilai 255 (putih), sedangkan piksel di luar rentang tersebut akan memiliki nilai 0 (hitam).
Kedua, saya menggunakan `cv2.inRange(hsv_image, lower_green, upper_green)` untuk membuat masker yang memisahkan bagian gambar yang berada dalam rentang warna hijau yang ditentukan oleh `lower_green` dan `upper_green`. Masker ini juga menghasilkan citra biner di mana piksel yang berada dalam rentang warna hijau akan memiliki nilai 255 (putih), dan piksel di luar rentang tersebut akan memiliki nilai 0 (hitam). Dengan menggunakan masker-masker ini, saya dapat mengidentifikasi dengan tepat bagian-bagian tertentu dari gambar yang memiliki warna kuning (misalnya, buah nanas) dan warna hijau (misalnya, daun).
##### Melakukan Oprasi Bitwise
```bash
segmented_pineapple = cv2.bitwise_and(image, image, mask=mask_pineapple)
segmented_leaves = cv2.bitwise_and(image, image, mask=mask_leaves)
```
Disini saya akan melakukan segmentasi  bagian-bagian tertentu dari gambar menggunakan masker yang telah dibuat sebelumnya dalam format HSV (Hue, Saturation, Value).
pada bagian kode pertama, `cv2.bitwise_and(image, image, mask=mask_pineapple)` itu digunakan untuk menerapkan operasi bitwise AND antara gambar asli (`image`) dan masker `mask_pineapple` yang telah dibuat sebelumnya. Hasil dari operasi ini adalah gambar yang hanya menampilkan bagian dari gambar asli yang sesuai dengan masker `mask_pineapple`, yaitu bagian-bagian yang berada dalam rentang warna kuning. Kedua, `cv2.bitwise_and(image, image, mask=mask_leaves)` digunakan untuk melakukan hal yang sama dengan masker `mask_leaves`, yaitu menghasilkan gambar yang hanya menampilkan bagian dari gambar asli yang sesuai dengan masker `mask_leaves`, yaitu bagian-bagian yang berada dalam rentang warna hijau.
##### Membuat Masker yang menunjukkan bagian buah Nanas tetapi tidak termasuk bagian daun-daunnya
```bash
mask_pineapple_no_leaves = cv2.bitwise_not(mask_leaves)
mask_pineapple_no_leaves = cv2.bitwise_and(mask_pineapple, mask_pineapple_no_leaves)
```
untuk membuat masker yang menunjukkan bagian buah nanas tetapi tidak termasuk daun-daunya, saya menggunakan operasi bitwise NOT dan bitwise AND dalam pustaka OpenCV. 
Pertama, saya menggunakan kode cv2.bitwise_not(mask_leaves) untuk menghasilkan masker yang merupakan kebalikan dari mask_leaves. Dengan kata lain, piksel yang awalnya bernilai 0 (hitam) dalam mask_leaves akan menjadi 255 (putih), dan sebaliknya. Ini artinya, masker ini menunjukkan bagian-bagian gambar yang bukan daun (misalnya, buah nanas). Kemudian, cv2.bitwise_and(mask_pineapple, mask_pineapple_no_leaves) mengaplikasikan operasi bitwise AND antara mask_pineapple (masker buah nanas) dan mask_pineapple_no_leaves (masker yang bukan daun). Hasil dari operasi ini adalah masker yang menunjukkan hanya bagian-bagian gambar yang termasuk dalam rentang warna kuning (buah nanas) dan bukan bagian dari daun-daunnya.
#### Menampilkan Output
```bash
fig, axs = plt.subplots(2, 2, figsize=(12, 10))

axs[0, 0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axs[0, 0].set_title('Nanas Asli')

axs[0, 1].imshow(mask_pineapple_no_leaves, cmap='gray')
axs[0, 1].set_title('Mask Nanas (Tanpa Daun)')

axs[1, 0].imshow(cv2.cvtColor(segmented_pineapple, cv2.COLOR_BGR2RGB))
axs[1, 0].set_title('Segmentasi Nanas')

axs[1, 1].imshow(cv2.cvtColor(segmented_leaves, cv2.COLOR_BGR2RGB))
axs[1, 1].set_title('Segmentasi Daun')

plt.show()
```
Pertama, kita menampilkan gambar "Nanas Asli", yaitu gambar mentah yang saya proses. Lalu ada, Subplot "Mask Nanas (Tanpa Daun)" ini akan menampilkan bagian gambar yang hanya berisi buah nanas, tanpa daun, yang ditandai dengan warna kuning. Kemudian, "Segmentasi Nanas" menampilkan bagian dari gambar yang telah berhasil diisolasi berdasarkan masker kuning tersebut. Lalu, subplot terakhir, "Segmentasi Daun", menampilkan bagian gambar yang berisi daun yang juga berhasil diidentifikasi.

Teori Pendukung :
1. **Konversi Warna (BGR ke HSV)**: Konversi warna dari BGR (Blue, Green, Red) ke HSV (Hue, Saturation, Value) memungkinkan pengenalan warna yang lebih intuitif dalam citra. HSV memisahkan komponen warna berdasarkan nuansa, kecerahan, dan intensitas, yang membantu dalam identifikasi objek berdasarkan warna aslinya.

2. **Penggunaan Masker (cv2.inRange)**: Masking adalah teknik di mana hanya piksel dalam rentang warna tertentu yang dipertahankan dalam citra, sedangkan piksel di luar rentang tersebut diabaikan. Fungsi `cv2.inRange` digunakan untuk membuat masker biner di mana piksel dalam rentang warna tertentu ditandai sebagai putih (255) dan yang lainnya sebagai hitam (0).

3. **Operasi Bitwise**: Operasi bitwise (AND, NOT) digunakan untuk menggabungkan atau memodifikasi masker. `cv2.bitwise_and` digunakan untuk menerapkan operasi AND antara dua gambar atau antara gambar dan masker, sementara `cv2.bitwise_not` digunakan untuk menghasilkan kebalikan dari sebuah masker.

4. **Segmentasi Gambar**: Segmentasi adalah proses membagi gambar menjadi bagian-bagian yang berbeda berdasarkan kriteria tertentu, seperti warna. Dalam konteks ini, segmentasi dilakukan untuk memisahkan buah nanas dan daun berdasarkan masker yang telah dibuat.

5. **Visualisasi dengan Matplotlib**: Matplotlib digunakan untuk visualisasi hasil pengolahan gambar dalam format yang mudah dipahami. Ini membantu dalam menampilkan gambar asli, masker, dan hasil segmentasi dengan jelas.
