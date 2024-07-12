# PA-PC_202231018_Hanif-Ibnu-Oktafian_C

### Penjelasan Program

1. **Impor Library**:
   ```python
   import cv2
   import matplotlib.pyplot as plt
   import numpy as np
   ```

   - `cv2`: Library OpenCV untuk pemrosesan gambar.
   - `matplotlib.pyplot`: Library Matplotlib untuk menampilkan gambar.
   - `numpy`: Library untuk operasi numerik.

2. **Memproses Gambar**:
   ```python
   gambar = cv2.imread('FotoDiri.jpeg')
   ```

   - Membaca gambar dari file `FotoDiri.jpeg` menggunakan OpenCV.

3. **Fungsi untuk Menampilkan Gambar**:
   ```python
   def tampilkan_gambar(gambar_list, judul_list):
       plt.figure(figsize=(15, 10))
       for i in range(len(gambar_list)):
           plt.subplot(2, 3, i+1)
           plt.imshow(cv2.cvtColor(gambar_list[i], cv2.COLOR_BGR2RGB))
           plt.title(judul_list[i])
           plt.axis('off')
       plt.show()
   ```

   - Fungsi ini menerima daftar gambar (`gambar_list`) dan daftar judul (`judul_list`).
   - Menggunakan Matplotlib untuk menampilkan gambar dalam grid 2x3.
   - Mengonversi gambar dari format BGR (OpenCV) ke RGB (Matplotlib) untuk tampilan yang benar.

4. **Gambar Asli**:
   ```python
   asli = gambar.copy()
   ```

   - Menyimpan salinan dari gambar asli.

5. **Rotasi Gambar**:
   ```python
   (tinggi, lebar) = gambar.shape[:2]
   pusat = (lebar // 2, tinggi // 2)
   M = cv2.getRotationMatrix2D(pusat, 45, 1.0)
   diputar = cv2.warpAffine(gambar, M, (lebar, tinggi))
   ```

   - Mendapatkan dimensi gambar (`tinggi` dan `lebar`).
   - Menentukan pusat rotasi.
   - Membuat matriks rotasi untuk memutar gambar sebesar 45 derajat.
   - Menerapkan rotasi menggunakan `cv2.warpAffine`.

6. **Mengubah Ukuran Gambar**:
   ```python
   tinggi_baru = int(tinggi * 1.5)  # Tinggi naik 50%
   lebar_baru = lebar  # Lebar tetap sama
   diubah_ukuran = cv2.resize(gambar, (lebar_baru, tinggi_baru))
   ```

   - Menghitung dimensi baru untuk gambar dengan meningkatkan tinggi sebesar 50% dan mempertahankan lebar asli.
   - Mengubah ukuran gambar menggunakan `cv2.resize`.

7. **Memotong Gambar**:
   ```python
   dipotong = gambar[50:200, 50:200]
   ```

   - Memotong bagian dari gambar dari koordinat (50,50) hingga (200,200).

8. **Membalik Gambar**:
   ```python
   dibalik = cv2.flip(gambar, 1)
   ```

   - Membalik gambar secara horizontal menggunakan `cv2.flip`.

9. **Translasi Gambar**:
   ```python
   M = np.float32([[1, 0, 50], [0, 1, 100]])
   ditranslasi = cv2.warpAffine(gambar, M, (lebar, tinggi))
   ```

   - Membuat matriks translasi untuk menggeser gambar 50 piksel ke kanan dan 100 piksel ke bawah.
   - Menerapkan translasi menggunakan `cv2.warpAffine`.

10. **Menampilkan Semua Gambar**:
    ```python
    gambar_list = [asli, diputar, diubah_ukuran, dipotong, dibalik, ditranslasi]
    judul_list = ['Citra Asli', 'After Rotated', 'After Resized', 'After Cropped', 'After Flipped', 'After Translated']
    tampilkan_gambar(gambar_list, judul_list)
    ```

    - Membuat daftar gambar dan judul.
    - Memanggil fungsi `tampilkan_gambar` untuk menampilkan semua gambar dalam grid.
   
    
### Pemrosesan Gambar: Teori dan Aplikasinya

Pemrosesan gambar adalah bidang yang luas dalam ilmu komputer dan teknik yang melibatkan manipulasi dan analisis gambar digital untuk mendapatkan informasi atau menghasilkan gambar yang lebih baik. Teknik-teknik dasar dalam pemrosesan gambar meliputi rotasi, perubahan ukuran, pemotongan, pembalikan, dan translasi gambar, yang masing-masing memiliki aplikasi dan teori yang mendasarinya.

**Rotasi gambar** adalah transformasi geometris yang memutar gambar di sekitar titik tertentu, biasanya pusat gambar, dengan sudut tertentu. Proses ini memerlukan matriks rotasi yang menggabungkan sudut rotasi dan pusat rotasi untuk menentukan posisi baru setiap piksel dalam gambar. Rotasi digunakan dalam berbagai aplikasi seperti perbaikan orientasi gambar, pembuatan efek artistik, dan augmentasi data dalam pelatihan model machine learning. Misalnya, dalam pengenalan karakter tulisan tangan, rotasi gambar membantu model untuk mengenali karakter dari berbagai orientasi.

**Perubahan ukuran gambar** adalah teknik untuk mengubah dimensi gambar, baik dengan memperbesar atau memperkecil. Proses ini melibatkan interpolasi piksel untuk menyesuaikan gambar ke dimensi baru tanpa mengurangi kualitasnya secara signifikan. Metode umum yang digunakan termasuk interpolasi bilinear dan bikubik. Perubahan ukuran sangat penting dalam berbagai aplikasi, seperti penyesuaian gambar untuk web, persiapan data untuk analisis, dan kompresi gambar untuk pengiriman yang lebih cepat melalui jaringan.

**Pemotongan gambar** adalah proses mengekstraksi bagian tertentu dari gambar dengan menentukan koordinat area yang ingin dipertahankan. Teknik ini berguna untuk fokus pada objek atau area tertentu dalam gambar dan menghilangkan bagian yang tidak relevan. Pemotongan digunakan dalam fotografi digital untuk menghilangkan gangguan latar belakang, dalam aplikasi medis untuk fokus pada area tertentu dari hasil scan, dan dalam sistem pengenalan wajah untuk mengekstraksi wajah dari gambar yang lebih besar.

**Pembalikan gambar**, baik secara horizontal maupun vertikal, adalah teknik sederhana namun efektif yang membalikkan arah piksel dalam gambar. Pembalikan horizontal mengubah sisi kiri menjadi kanan dan sebaliknya, sedangkan pembalikan vertikal mengubah sisi atas menjadi bawah. Teknik ini sering digunakan dalam augmentasi data untuk pelatihan model machine learning, terutama dalam visi komputer, untuk meningkatkan variasi data pelatihan tanpa menambah gambar baru secara eksplisit. Pembalikan juga digunakan dalam aplikasi fotografi untuk efek cermin.

**Translasi gambar** adalah teknik untuk menggeser posisi gambar dalam bidang koordinat tanpa mengubah orientasi atau skala. Translasi dilakukan dengan menggunakan matriks translasi yang menentukan seberapa jauh dan ke arah mana gambar harus digeser. Teknik ini digunakan dalam aplikasi navigasi robot, pengenalan objek, dan augmentasi data. Dalam visi komputer, translasi membantu model belajar mengenali objek yang mungkin tidak selalu berada di pusat gambar.

Dalam praktiknya, teknik-teknik ini sering dikombinasikan untuk mencapai tujuan tertentu. Misalnya, dalam pengenalan objek, gambar mungkin dipotong, diubah ukurannya, dan kemudian diputar untuk memastikan model dapat mengenali objek dari berbagai perspektif. Buku “Digital Image Processing” oleh Gonzalez dan Woods memberikan landasan teori yang mendalam tentang teknik-teknik ini, sedangkan jurnal-jurnal ilmiah seperti “A Comprehensive Review of Image Enhancement Techniques” oleh Smith dan Liu mengulas aplikasi praktis dan metode terbaru dalam pemrosesan gambar. Selain itu, penelitian dalam deep learning, seperti yang dibahas dalam “UNet++: A Nested U-Net Architecture for Medical Image Segmentation,” menunjukkan bagaimana teknik augmentasi data, termasuk rotasi dan pembalikan, diterapkan untuk meningkatkan performa model dalam tugas-tugas segmentasi gambar medis. Pemrosesan gambar merupakan bidang yang terus berkembang dengan aplikasi luas, mulai dari analisis citra medis hingga sistem pengenalan wajah, dan terus berkontribusi pada kemajuan teknologi modern.
