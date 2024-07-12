# PA-PC_202231031_RAFI-DIO-ADIBTA_C
import cv2
import matplotlib.pyplot as plt
import numpy as np
import skimage
from skimage.feature import graycomatrix,graycoprops

PENJELASAN:
**1.import cv2**
Perintah ini mengimpor library OpenCV.OpenCV mendukung berbagai operasi pengolahan citra seperti pemfilteran, deteksi tepi, deteksi objek, transformasi geometris,
**2.import Matplotlib.pyplot as plt**
Perintah ini mengimpor modul pyplot dari library Matplotlib, yang digunakan untuk membuat visualisasi data dalam bentuk grafik. 
**3.import numpy as np**
Perintah ini berfungsi mengimpor pustaka NumPy dan memberi alias np. NumPy adalah pustaka fundamental untuk komputasi ilmiah di Python yang mendukung array multidimensi dan berbagai fungsi matematika yang efisien.
**4.import skimage**
Perintah ini berfungsi mengimpor pustaka scikit-image, yang digunakan untuk pengolahan citra. Scikit-image menyediakan algoritma yang efisien dan mudah digunakan untuk berbagai tugas pengolahan citra, seperti segmentasi, penajaman, transformasi geometris, dll.

**from skimage.feature import graycomatrix, graycoprops**
graycomatrix: Fungsi ini menghitung matriks co-occurrence tingkat abu-abu (GLCM) dari sebuah citra.
graycoprops: Fungsi ini digunakan untuk menghitung sifat-sifat statistik dari matriks GLCM yang dihasilkan oleh graycomatrix. 


def mean_filter(image, kernel_size=3):
    padded_image = np.pad(image, ((kernel_size // 2, kernel_size // 2), (kernel_size // 2, kernel_size // 2)), mode='constant')
    filtered_image = np.zeros_like(image)
    
    for i in range(image.shape[0]):
        for j in range(image.shape[1]):
            region = padded_image[i:i + kernel_size, j:j + kernel_size]
            filtered_image[i, j] = np.mean(region)
    
    return filtered_image

    PENJELASAN:
**1.mean_filter**
image merupakan perintah untuk Citra input yang akan difilter.
kernel_size berfungsi untuk mengatur ukuran kernel untuk filter mean.
np.pad berfungsi menambahkan padding di sekitar citra asli untuk memungkinkan operasi filter pada tepi citra. Padding dilakukan dengan nilai nol (constant).
np.zeros_like(image) berfungsi untuk membuat citra keluaran (filtered_image) yang memiliki ukuran dan tipe data yang sama dengan citra input.
for i dan for j berfungsi untuk mengiterasi setiap pixel pada citra asli.
region = padded_image[i:i + kernel_size, j:j + kernel_size] berfungsi menentukan wilayah
di sekitar pixel yang sedang diproses sesuai ukuran kernel.
np.mean(region) berfngsi untuk menghitung rata-rata nilai pixel dalam region tersebut dan menyimpannya di citra keluaran.

image_path = 'foto diri.jpg'
img = io.imread(image_path)
img_gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

PENJELASAN:
**io.imread(image_path)** berfungsi untuk membaca citra dari file yang ditentukan oleh image_path.
**cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)** berfungsi untuk mengonversi citra warna (RGB) menjadi citra skala abu-abu (grayscale) menggunakan OpenCV.

median_filtered = cv2.medianBlur(img, 5)
mean_filtered_gray = mean_filter(img_gray, kernel_size=3)
mean_filtered_rgb = cv2.cvtColor(mean_filtered_gray, cv2.COLOR_GRAY2RGB)

PENJELASAN:
**cv2.medianBlur(img, 5)** berfungsi untuk menerapkan filter median pada citra dengan ukuran kernel 5x5.
**mean_filter(img_gray, kernel_size=3)** berfungsi untuk menerapkan filter mean pada citra skala abu-abu dengan ukuran kernel 3x3 menggunakan fungsi mean_filter yang telah didefinisikan sebelumnya.
**cv2.cvtColor(mean_filtered_gray, cv2.COLOR_GRAY2RGB)**  berfungsi untuk Mengonversi citra hasil filter mean (grayscale) kembali ke citra warna (RGB) untuk keperluan visualisasi.


fig, axs = plt.subplots(2, 2, figsize=(14, 12))
ax = axs.ravel()

ax[0].imshow(img)
ax[0].set_title('Citra Asli')


ax[1].imshow(img_gray, cmap='gray')
ax[1].set_title('Original Image')


ax[2].imshow(median_filtered)
ax[2].set_title('After Filter Median')


ax[3].imshow(mean_filtered_rgb)
ax[3].set_title('Mean Filtered Image')


plt.tight_layout()
plt.show()

PENJELASAN:

**plt.subplots(2, 2, figsize=(14, 12))** untuk embuat grid subplots 2x2 untuk menampilkan citra.
**ax = axs.ravel()** untuk mengubah array 2D axs menjadi array 1D untuk mempermudah iterasi.
**ax[0].imshow(img)** berfungsi untuk menampilkan citra asli.
**ax[0].set_title('Citra Asli')**  untuk memberikan judul pada subplot pertama.
**ax[1].imshow(img_gray, cmap='gray')** berfungsi untuk Menampilkan citra grayscale.
**ax[1].set_title('Original Image')** berfungsi untuk memberikan judul pada subplot kedua.
**ax[2].imshow(median_filtered)** berfungsi untuk menampilkan citra hasil filter median.
**ax[2].set_title('After Filter Median')** memiliki fungsi memberikan judul pada subplot ketiga.
**ax[3].imshow(mean_filtered_rgb)** untuk menampilkan citra hasil filter mean yang telah dikonversi kembali ke RGB.
**ax[3].set_title('Mean Filtered Image')** untuk memberikan judul pada subplot keempat.
**plt.tight_layout()** untuk mengatur tata letak subplot agar tidak tumpang tindih.
**plt.show()** untuk menampilkan semua subplot.
