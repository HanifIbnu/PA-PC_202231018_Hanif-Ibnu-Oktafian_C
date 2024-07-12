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

