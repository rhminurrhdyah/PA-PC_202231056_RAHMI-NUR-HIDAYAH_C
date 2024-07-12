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
