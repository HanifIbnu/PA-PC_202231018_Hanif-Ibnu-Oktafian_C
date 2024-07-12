# PA-PC_202231018_Hanif-Ibnu-Oktafian_C
import cv2
import matplotlib.pyplot as plt
import numpy as np

# Memproses Gambar
gambar = cv2.imread('FotoDiri.jpeg')

# Untuk Menampilkan Gambar
def tampilkan_gambar(gambar_list, judul_list):
    plt.figure(figsize=(15, 10))
    for i in range(len(gambar_list)):
        plt.subplot(2, 3, i+1)
        plt.imshow(cv2.cvtColor(gambar_list[i], cv2.COLOR_BGR2RGB))
        plt.title(judul_list[i])
        plt.axis('off')
    plt.show()

# Gambar Asli
asli = gambar.copy()

# Gambar Setelah Diputar
(tinggi, lebar) = gambar.shape[:2]
pusat = (lebar // 2, tinggi // 2)
M = cv2.getRotationMatrix2D(pusat, 45, 1.0)
diputar = cv2.warpAffine(gambar, M, (lebar, tinggi))

# Gambar Setelah Diubah Ukuran
tinggi_baru = int(tinggi * 1.5)  # Tinggi naik 50%
lebar_baru = lebar  # Lebar tetap sama
diubah_ukuran = cv2.resize(gambar, (lebar_baru, tinggi_baru))

# Gambar Setelah Dipotong
dipotong = gambar[50:200, 50:200]

# Gambar Setelah Dibalik
dibalik = cv2.flip(gambar, 1)

# Gambar Setelah Ditranslasi
M = np.float32([[1, 0, 50], [0, 1, 100]])
ditranslasi = cv2.warpAffine(gambar, M, (lebar, tinggi))

# Menampilkan semua gambar
gambar_list = [asli, diputar, diubah_ukuran, dipotong, dibalik, ditranslasi]
judul_list = ['Citra Asli', 'After Rotated', 'After Resized', 'After Cropped', 'After Flipped', 'After Translated']
tampilkan_gambar(gambar_list, judul_list)
