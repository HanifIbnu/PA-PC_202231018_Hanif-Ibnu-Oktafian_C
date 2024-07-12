# PA-PC_202231018_Hanif-Ibnu-Oktafian_C

### Penjelasan Program

1. **Impor Library**:
```python
import cv2 as cv
import numpy as np
import matplotlib.pyplot as plt
```
Mengimpor pustaka yang diperlukan:
- `cv2` dari OpenCV untuk operasi citra.
- `numpy` untuk manipulasi array.
- `matplotlib.pyplot` untuk menampilkan gambar.
  
2. **Memproses Gambar**:
```python
# Membaca gambar
img = cv.imread('FotoDiri.jpeg')
```
Membaca gambar dari file `FotoDiri.jpeg` dan menyimpannya dalam variabel `img`.

3. **Fungsi untuk Menampilkan Gambar**:
```python
# Mendapatkan ukuran gambar
rows, cols = img.shape[:2]
```
Mendapatkan ukuran gambar (jumlah baris dan kolom) dari citra yang dibaca.

4. **Gambar Asli**:
```python
# Gambar asli
img_asli = img.copy()
```
Membuat salinan dari gambar asli untuk ditampilkan nanti.

5. **Mengubah Ukuran Gambar**:
```python
# Resize (memperkecil lebar menjadi setengah)
height, width = img.shape[:2]
resized = cv.resize(img, (width // 2, height), interpolation=cv.INTER_CUBIC)
```
Mengubah ukuran gambar dengan memperkecil lebar menjadi setengah dari ukuran aslinya, sementara tinggi tetap sama. Metode interpolasi yang digunakan adalah `INTER_CUBIC` yang memberikan kualitas hasil yang lebih baik.

6. **Translasi Gambar**:
```python
# Translasi (menggeser gambar 100 piksel ke kanan dan 100 piksel ke bawah)
M_translate = np.float32([[1, 0, 100], [0, 1, 100]])
translated = cv.warpAffine(img, M_translate, (cols, rows))
```
Mentranslasi (menggeser) gambar sebesar 100 piksel ke kanan dan 100 piksel ke bawah. Matriks translasi `M_translate` digunakan bersama dengan fungsi `warpAffine` untuk menerapkan pergeseran tersebut.

7. **Rotasi Gambar**:
```python
# Rotate (memotong diagonal)
(tinggi, lebar) = img.shape[:2]
pusat = (lebar // 2, tinggi // 2)
M_rotate = cv.getRotationMatrix2D(pusat, 45, 1.0)
rotated = cv.warpAffine(img, M_rotate, (lebar, tinggi))
```
Memutar gambar sebesar 45 derajat searah jarum jam. Pusat rotasi adalah pusat gambar (`pusat`). Matriks rotasi `M_rotate` digunakan bersama dengan fungsi `warpAffine` untuk menerapkan rotasi.

8. **Memotong Gambar**:
```python
# Crop (memotong gambar)
cropped = img[50:300, 50:300]
```
Memotong gambar dari koordinat (50, 50) hingga (300, 300), menghasilkan gambar yang lebih kecil.

9. **Rotasi Gambar**:
```python
# Flip (membalik gambar)
flipped = cv.flip(img, 1)
```
Membalik gambar secara horizontal. Parameter `1` menunjukkan pembalikan pada sumbu y (horizontal).

10. **Menampilkan Semua Gambar Setelah Pemrosesan Gambar**
```python
# Menampilkan semua gambar dalam layout 2x3
fig, axs = plt.subplots(2, 3, figsize=(15, 10))
```
Membuat layout tampilan 2 baris x 3 kolom menggunakan Matplotlib untuk menampilkan gambar-gambar yang telah dimodifikasi.

```python
# Gambar asli
axs[0, 0].imshow(cv.cvtColor(img_asli, cv.COLOR_BGR2RGB))
axs[0, 0].set_title('Citra Asli')
axs[0, 0].axis('on')
```
Menampilkan gambar asli pada posisi [0, 0] (baris pertama, kolom pertama) dalam layout. Fungsi `cv.cvtColor` digunakan untuk mengubah format warna dari BGR ke RGB (format yang digunakan Matplotlib).

```python
# Gambar setelah diputar
axs[0, 1].imshow(cv.cvtColor(rotated, cv.COLOR_BGR2RGB))
axs[0, 1].set_title('After Rotated')
axs[0, 1].axis('on')
```
Menampilkan gambar setelah diputar pada posisi [0, 1] (baris pertama, kolom kedua) dalam layout.

```python
# Gambar setelah diubah ukuran
axs[0, 2].imshow(cv.cvtColor(resized, cv.COLOR_BGR2RGB))
axs[0, 2].set_title('After Resized')
axs[0, 2].axis('on')
```
Menampilkan gambar setelah diubah ukuran pada posisi [0, 2] (baris pertama, kolom ketiga) dalam layout.

```python
# Gambar setelah dipotong
axs[1, 0].imshow(cv.cvtColor(cropped, cv.COLOR_BGR2RGB))
axs[1, 0].set_title('After Cropped')
axs[1, 0].axis('on')
```
Menampilkan gambar setelah dipotong pada posisi [1, 0] (baris kedua, kolom pertama) dalam layout.

```python
# Gambar setelah dibalik
axs[1, 1].imshow(cv.cvtColor(flipped, cv.COLOR_BGR2RGB))
axs[1, 1].set_title('After Flipped')
axs[1, 1].axis('on')
```
Menampilkan gambar setelah dibalik pada posisi [1, 1] (baris kedua, kolom kedua) dalam layout.

```python
# Gambar setelah ditranslasi
axs[1, 2].imshow(cv.cvtColor(translated, cv.COLOR_BGR2RGB))
axs[1, 2].set_title('After Translated')
axs[1, 2].axis('on')
```
Menampilkan gambar setelah ditranslasi pada posisi [1, 2] (baris kedua, kolom ketiga) dalam layout.

```python
plt.show()
```
Menampilkan semua gambar dalam layout 2x3 menggunakan Matplotlib.


### Pemrosesan Gambar: Teori dan Aplikasinya

Pemrosesan gambar adalah bidang yang luas dalam ilmu komputer dan teknik yang melibatkan manipulasi dan analisis gambar digital untuk mendapatkan informasi atau menghasilkan gambar yang lebih baik. Teknik-teknik dasar dalam pemrosesan gambar meliputi rotasi, perubahan ukuran, pemotongan, pembalikan, dan translasi gambar, yang masing-masing memiliki aplikasi dan teori yang mendasarinya.

**Rotasi gambar** adalah transformasi geometris yang memutar gambar di sekitar titik tertentu, biasanya pusat gambar, dengan sudut tertentu. Proses ini memerlukan matriks rotasi yang menggabungkan sudut rotasi dan pusat rotasi untuk menentukan posisi baru setiap piksel dalam gambar. Rotasi digunakan dalam berbagai aplikasi seperti perbaikan orientasi gambar, pembuatan efek artistik, dan augmentasi data dalam pelatihan model machine learning. Misalnya, dalam pengenalan karakter tulisan tangan, rotasi gambar membantu model untuk mengenali karakter dari berbagai orientasi.

**Perubahan ukuran gambar** adalah teknik untuk mengubah dimensi gambar, baik dengan memperbesar atau memperkecil. Proses ini melibatkan interpolasi piksel untuk menyesuaikan gambar ke dimensi baru tanpa mengurangi kualitasnya secara signifikan. Metode umum yang digunakan termasuk interpolasi bilinear dan bikubik. Perubahan ukuran sangat penting dalam berbagai aplikasi, seperti penyesuaian gambar untuk web, persiapan data untuk analisis, dan kompresi gambar untuk pengiriman yang lebih cepat melalui jaringan.

**Pemotongan gambar** adalah proses mengekstraksi bagian tertentu dari gambar dengan menentukan koordinat area yang ingin dipertahankan. Teknik ini berguna untuk fokus pada objek atau area tertentu dalam gambar dan menghilangkan bagian yang tidak relevan. Pemotongan digunakan dalam fotografi digital untuk menghilangkan gangguan latar belakang, dalam aplikasi medis untuk fokus pada area tertentu dari hasil scan, dan dalam sistem pengenalan wajah untuk mengekstraksi wajah dari gambar yang lebih besar.

**Pembalikan gambar**, baik secara horizontal maupun vertikal, adalah teknik sederhana namun efektif yang membalikkan arah piksel dalam gambar. Pembalikan horizontal mengubah sisi kiri menjadi kanan dan sebaliknya, sedangkan pembalikan vertikal mengubah sisi atas menjadi bawah. Teknik ini sering digunakan dalam augmentasi data untuk pelatihan model machine learning, terutama dalam visi komputer, untuk meningkatkan variasi data pelatihan tanpa menambah gambar baru secara eksplisit. Pembalikan juga digunakan dalam aplikasi fotografi untuk efek cermin.

**Translasi gambar** adalah teknik untuk menggeser posisi gambar dalam bidang koordinat tanpa mengubah orientasi atau skala. Translasi dilakukan dengan menggunakan matriks translasi yang menentukan seberapa jauh dan ke arah mana gambar harus digeser. Teknik ini digunakan dalam aplikasi navigasi robot, pengenalan objek, dan augmentasi data. Dalam visi komputer, translasi membantu model belajar mengenali objek yang mungkin tidak selalu berada di pusat gambar.

Dalam praktiknya, teknik-teknik ini sering dikombinasikan untuk mencapai tujuan tertentu. Misalnya, dalam pengenalan objek, gambar mungkin dipotong, diubah ukurannya, dan kemudian diputar untuk memastikan model dapat mengenali objek dari berbagai perspektif. Buku “Digital Image Processing” oleh Gonzalez dan Woods memberikan landasan teori yang mendalam tentang teknik-teknik ini, sedangkan jurnal-jurnal ilmiah seperti “A Comprehensive Review of Image Enhancement Techniques” oleh Smith dan Liu mengulas aplikasi praktis dan metode terbaru dalam pemrosesan gambar. Selain itu, penelitian dalam deep learning, seperti yang dibahas dalam “UNet++: A Nested U-Net Architecture for Medical Image Segmentation,” menunjukkan bagaimana teknik augmentasi data, termasuk rotasi dan pembalikan, diterapkan untuk meningkatkan performa model dalam tugas-tugas segmentasi gambar medis. Pemrosesan gambar merupakan bidang yang terus berkembang dengan aplikasi luas, mulai dari analisis citra medis hingga sistem pengenalan wajah, dan terus berkontribusi pada kemajuan teknologi modern.
