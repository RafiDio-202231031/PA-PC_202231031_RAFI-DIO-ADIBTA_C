# PA-PC_202231031_RAFI-DIO-ADIBTA_C
<br>import cv2<br>
<br>import matplotlib.pyplot as plt<br>
<br>import numpy as np<br>
<br>import skimage<br>
<br>from skimage.feature import graycomatrix,graycoprops<br>

<br>PENJELASAN:<br>
<br>**1.import cv2**<br>
<br>Perintah ini mengimpor library OpenCV.OpenCV mendukung berbagai operasi pengolahan citra seperti pemfilteran, deteksi tepi, deteksi objek, transformasi geometris,<br>
<br>**2.import Matplotlib.pyplot as plt**<br>
<br>Perintah ini mengimpor modul pyplot dari library Matplotlib, yang digunakan untuk membuat visualisasi data dalam bentuk grafik. 
<br>**3.import numpy as np**<br>
<br>Perintah ini berfungsi mengimpor pustaka NumPy dan memberi alias np. NumPy adalah pustaka fundamental untuk komputasi ilmiah di Python yang mendukung array multidimensi dan berbagai fungsi matematika yang efisien.<br>
<br>**4.import skimage**<br>
<br>Perintah ini berfungsi mengimpor pustaka scikit-image, yang digunakan untuk pengolahan citra. Scikit-image menyediakan algoritma yang efisien dan mudah digunakan untuk berbagai tugas pengolahan citra, seperti segmentasi, penajaman, transformasi geometris, dll.<br>

<br>**from skimage.feature import graycomatrix, graycoprops**<br>
<br>graycomatrix: Fungsi ini menghitung matriks co-occurrence tingkat abu-abu (GLCM) dari sebuah citra.<br>
<br>graycoprops: Fungsi ini digunakan untuk menghitung sifat-sifat statistik dari matriks GLCM yang dihasilkan oleh graycomatrix. <br>


<br>def mean_filter(image, kernel_size=3):<br>
  <br>  padded_image = np.pad(image, ((kernel_size // 2, kernel_size // 2), (kernel_size // 2, kernel_size // 2)), mode='constant')<br>
   <br> filtered_image = np.zeros_like(image)<br>
    
  <br> for i in range(image.shape[0]):<br>
        <br>for j in range(image.shape[1]):<br>
          <br>  region = padded_image[i:i + kernel_size, j:j + kernel_size]<br>
            <br>filtered_image[i, j] = np.mean(region)<br>
    
   <br> return filtered_image<br>

  <br>  PENJELASAN:<br>
<br>**1.mean_filter**<br>
<br>image merupakan perintah untuk Citra input yang akan difilter.<br>
<br>kernel_size berfungsi untuk mengatur ukuran kernel untuk filter mean.<br>
<br>np.pad berfungsi menambahkan padding di sekitar citra asli untuk memungkinkan operasi filter pada tepi citra. Padding dilakukan dengan nilai nol (constant).<br>
<br>np.zeros_like(image) berfungsi untuk membuat citra keluaran (filtered_image) yang memiliki ukuran dan tipe data yang sama dengan citra input.
for i dan for j berfungsi untuk mengiterasi setiap pixel pada citra asli.<br>
<br>region = padded_image[i:i + kernel_size, j:j + kernel_size] berfungsi menentukan wilayah
di sekitar pixel yang sedang diproses sesuai ukuran kernel.<br>
<br>np.mean(region) berfngsi untuk menghitung rata-rata nilai pixel dalam region tersebut dan menyimpannya di citra keluaran.<br>

<br>image_path = 'foto diri.jpg'<br>
<br>img = io.imread(image_path)<br>
<br>img_gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)<br>

<br>PENJELASAN:<br>
<br>**io.imread(image_path)** berfungsi untuk membaca citra dari file yang ditentukan oleh image_path.<br>
<br>**cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)** berfungsi untuk mengonversi citra warna (RGB) menjadi citra skala abu-abu (grayscale) menggunakan OpenCV.<br>

<br>median_filtered = cv2.medianBlur(img, 5)<br>
<br>mean_filtered_gray = mean_filter(img_gray, kernel_size=3)<br>
<br>mean_filtered_rgb = cv2.cvtColor(mean_filtered_gray, cv2.COLOR_GRAY2RGB)<br>

<br>PENJELASAN:<br>
<br>**cv2.medianBlur(img, 5)** berfungsi untuk menerapkan filter median pada citra dengan ukuran kernel 5x5.<br>
<br>**mean_filter(img_gray, kernel_size=3)** berfungsi untuk menerapkan filter mean pada citra skala abu-abu dengan ukuran kernel 3x3 menggunakan fungsi mean_filter yang telah didefinisikan sebelumnya.<br>
<br>**cv2.cvtColor(mean_filtered_gray, cv2.COLOR_GRAY2RGB)**  berfungsi untuk Mengonversi citra hasil filter mean (grayscale) kembali ke citra warna (RGB) untuk keperluan visualisasi.<br>


<br>fig, axs = plt.subplots(2, 2, figsize=(14, 12))<br>
<br>ax = axs.ravel()<br>

<br>ax[0].imshow(img)<br>
<br>ax[0].set_title('Citra Asli')<br>


<br>ax[1].imshow(img_gray, cmap='gray')<br>
<br>ax[1].set_title('Original Image')<br>


<br>ax[2].imshow(median_filtered)<br>
<br>ax[2].set_title('After Filter Median')<br>


<br>ax[3].imshow(mean_filtered_rgb)<br>
<br>ax[3].set_title('Mean Filtered Image')<br>


<br>plt.tight_layout()<br>
<br>plt.show()<br>

<br>PENJELASAN:<br>

<br>**plt.subplots(2, 2, figsize=(14, 12))** untuk embuat grid subplots 2x2 untuk menampilkan citra.<br>
<br>**ax = axs.ravel()** untuk mengubah array 2D axs menjadi array 1D untuk mempermudah iterasi.<br>
<br>**ax[0].imshow(img)** berfungsi untuk menampilkan citra asli.<br>
<br>**ax[0].set_title('Citra Asli')**  untuk memberikan judul pada subplot pertama.<br>
<br>**ax[1].imshow(img_gray, cmap='gray')** berfungsi untuk Menampilkan citra grayscale.<br>
<br>**ax[1].set_title('Original Image')** berfungsi untuk memberikan judul pada subplot kedua.<br>
<br>**ax[2].imshow(median_filtered)** berfungsi untuk menampilkan citra hasil filter median.<br>
<br>**ax[2].set_title('After Filter Median')** memiliki fungsi memberikan judul pada subplot ketiga.<br>
<br>**ax[3].imshow(mean_filtered_rgb)** untuk menampilkan citra hasil filter mean yang telah dikonversi kembali ke RGB.<br>
<br>**ax[3].set_title('Mean Filtered Image')** untuk memberikan judul pada subplot keempat.<br>
<br>**plt.tight_layout()** untuk mengatur tata letak subplot agar tidak tumpang tindih.<br>
<br>**plt.show()** untuk menampilkan semua subplot.<br>
