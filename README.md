Berikut adalah penjelasan Hasil UTS Praktikum yang telah saya buat:
-
#1
-
*cv2*: Library OpenCV digunakan untuk pemrosesan gambar.
*numpy*: Library ini digunakan untuk manipulasi data array.
*matplotlib.pyplot*: Library ini digunakan untuk membuat plot dan visualisasi data.
*matplotlib.image*: Fungsi ini dari matplotlib khusus untuk membaca dan menampilkan gambar.

#2
-
*color_image = img.imread('Nama.jpg')*: digunakan untuk mengambil gambar dengan nama file 'Nama.jpg' menggunakan fungsi imread dari modul image dari matplotlib, dan menyimpannya dalam variabel color_image.
*plt.imshow(color_image): menggunakan plt.imshow()*: untuk menampilkan gambar yang telah diambil pada langkah sebelumnya.

#3
-
*R = color_image[:, :, 0]*: mengambil salinan dari masing-masing komponen warna (merah) dari gambar yang disimpan dalam variabel color_image.
*G = color_image[:, :, 1]*: mengambil salinan dari masing-masing komponen warna (hijau) dari gambar yang disimpan dalam variabel color_image.
*B = color_image[:, :, 2]*: mengambil salinan dari masing-masing komponen warna (biru) dari gambar yang disimpan dalam variabel color_image.

*f, (c1, c2, c3, c4) = plt.subplots(1, 4, figsize = (20,10))*: untuk membuat subplot dengan ukuran 1 baris dan 4 kolom, dengan ukuran figur 20x10 inci.

*c1.set_title('Citra Kontras')
c1.imshow(color_image)                  : menetapkan judul "Citra Kontras" untuk subplot pertama (c1), kemudian menampilkan gambar warna utuh (color_image) pada subplot tersebut.
c1.axis('off')*

*c2.set_title('Merah') 
c2.imshow(R, cmap="gray")               : menetapkan judul "Merah" untuk subplot kedua (c2), lalu menampilkan komponen warna merah (R) dalam citra menggunakan colormap "gray".
c2.axis('off')*

*c3.set_title('Hijau') 
c3.imshow(G, cmap="gray")               : menetapkan judul "Hijau" untuk subplot ketiga (c3), dan menampilkan komponen warna hijau (G) dalam citra dengan colormap "gray".
c3.axis('off')*

*c4.set_title('Biru') 
c4.imshow(B, cmap="gray")               : menetapkan judul "Biru" untuk subplot keempat (c4), dan menampilkan komponen warna biru (B) dalam citra dengan colormap "gray".
c4.axis('off')*

#4
-
*color_image = cv2.imread('Nama.jpg')*: membaca gambar dengan nama file 'Nama.jpg' menggunakan fungsi imread dari OpenCV (cv2) dan menyimpannya dalam variabel color_image.
*color_image = cv2.cvtColor(color_image, cv2.COLOR_BGR2RGB)*: mengonversi skema warna gambar dari BGR (Blue-Green-Red) ke RGB (Red-Green-Blue) menggunakan fungsi cvtColor dari OpenCV.

#5
-
*Histogram_Biru = cv2.calcHist([B], [0], None, [256], [0, 256])*: menghitung histogram untuk komponen warna biru dengan rentang nilai 0 hingga 256.
*Histogram_Hijau = cv2.calcHist([G], [0], None,[256],[0,256])*: menghitung histogram untuk komponen warna hijau dengan rentang nilai 0 hingga 256.
*Histogram_Merah = cv2.calcHist([R], [0], None,[256],[0,256])*: menghitung histogram untuk komponen warna merah dengan rentang nilai 0 hingga 256.
*Histogram_CitraKontras = cv2.calcHist([color_image], [0,1,2], None, [256, 256, 256], [0, 256, 0, 256, 0, 256])*: menghitung histogram untuk seluruh citra dengan menggabungkan informasi histogram dari ketiga komponen warna. Ini dilakukan dengan menentukan saluran warna [0,1,2] dan menggunakan 256x256x256 bins dengan rentang nilai 0 hingga 256

#6
-
*plt.figure(figsize=(14, 10))*: membuat figur dengan ukuran 14x10 inci menggunakan plt.figure(figsize=(14, 10)).

*plt.subplot(2, 2, 1) 
plt.plot(Histogram_Biru, color='b')
plt.title( 'Histogram Biru')                          : menampilkan histogram untuk komponen warna biru dengan menggunakan fungsi plot & judul subplot diatur sebagai "Histogram Biru". 
plt.xlim([0, 256])*

*plt.subplot (2, 2, 2)
plt.plot(Histogram_Hijau, color='g')
plt.title( 'Histogram Hijau')                         : menampilkan histogram untuk komponen warna hijau dengan menggunakan fungsi plot & judul subplot diatur sebagai "Histogram Hijau".
plt.xlim([0, 256])*

*plt.subplot (2, 2, 3) 
plt.plot(Histogram_Merah, color='r')
plt.title( 'Histogram Merah')                         : menampilkan histogram untuk komponen warna merah dengan menggunakan fungsi plot & judul subplot diatur sebagai "Histogram Merah".
plt.xlim([0, 256])*

*plt.subplot (2, 2, 4)
plt.plot(Histogram_CitraKontras.flatten(), color='gray')
plt.title('Histogram Citra Kontras')
plt.xlim([0, 256])*: menampilkan histogram untuk seluruh citra kontras dengan memanfaatkan histogram tiga dimensi yang sudah dihitung sebelumnya. Histogram di-flatten menjadi satu dimensi dengan flatten(), kemudian digambar dengan warna abu-abu ('gray'). Judul subplot diatur sebagai "Histogram Citra Kontras" dan rentang sumbu x diatur dari 0 hingga 256.

#7
-
*def detect_and_highlight_colors(image, lower, upper)*: digunakan untuk mendeteksi dan menyorot area dalam gambar yang memiliki warna dalam rentang tertentu yang ditentukan oleh parameter lower dan upper.
    *hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)*: untuk mengonversi gambar dari skema warna BGR ke HSV. 
    *mask = cv2.inRange(hsv, lower, upper)*: Untuk menggunakan mask.
    *result = cv2.bitwise_and(image, image, mask=mask)*: untuk melakukan operasi bitwise AND antara gambar asli dan mask.
    *return result*: untuk mengembalikan gambar hasil yang telah disorot.

#8
-
*def increase_brightness(image, value=30):  digunakan untuk meningkatkan kecerahan gambar dengan nilai yang ditentukan atau default sebesar 30.
    *hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)*: untuk mengonversi gambar dari skema warna BGR ke HSV.
    *v = hsv[:, :, 2] + value*: Menambahkan nilai ke komponen kecerahan (value) dalam gambar HSV ini akan meningkatkan kecerahan gambarnya.
    *hsv[:, :, 2] = np.clip(v, 0, 255)*: untuk memastikan bahwa nilai kecerahan yang diperoleh tidak melebihi rentang yang diizinkan 
   *return cv2.cvtColor(hsv, cv2.COLOR_HSV2BGR)*: untuk mengembalikan gambar yang sudah jadi.

#9
-
*image = cv2.imread('Nama.jpg')
brightened_image = increase_brightness(image)*

*blue_lower = np.array([100, 50, 50])
blue_upper = np.array([130, 255, 255])*

*red_lower1 = np.array([0, 50, 50])
red_upper1 = np.array([10, 255, 255])
red_lower2 = np.array([170, 50, 50])
red_upper2 = np.array([180, 255, 255])*

*green_lower = np.array([40, 50, 50])
green_upper = np.array([80, 255, 255])* <br>

Kode di atas membaca gambar dengan nama 'Nama.jpg' menggunakan OpenCV (cv2.imread('Nama.jpg')). Gambar tersebut kemudian dimasukkan ke dalam fungsi increase_brightness untuk meningkatkan kecerahannya, dan hasilnya disimpan dalam variabel brightened_image.
> Rentang warna biru ditentukan dengan blue_lower dan blue_upper.
> Rentang warna merah dibagi menjadi dua bagian. Rentang pertama adalah red_lower1 dan red_upper1, sementara rentang kedua adalah red_lower2 dan red_upper2.
> Rentang warna hijau ditentukan dengan green_lower dan green_upper.

#10
-
*blue_detection = detect_and_highlight_colors(brightened_image, blue_lower, blue_upper)*: untuk mendeteksi dan menyorot area dengan warna biru dalam gambar yang cerah.
*red_detection = detect_and_highlight_colors(brightened_image, red_lower1, red_upper1) + \
                detect_and_highlight_colors(brightened_image, red_lower2, red_upper2)*: untuk mendeteksi dan menyorot area dengan warna merah dalam gambar yang telah dicerahkan dan warna dibagi 2 bagian
*green_detection = detect_and_highlight_colors(brightened_image, green_lower, green_upper)*: untuk mendeteksi dan menyorot area dengan warna hijau dalam gambar yang cerah.

#11
-
*plt.figure(figsize=(10, 8))
plt.subplot(221), plt.imshow(cv2.cvtColor(brightened_image, cv2.COLOR_BGR2RGB)), plt.title('Citra Kontras')
plt.subplot(222), plt.imshow(cv2.cvtColor(blue_detection, cv2.COLOR_BGR2RGB)), plt.title('Biru')
plt.subplot(223), plt.imshow(cv2.cvtColor(red_detection, cv2.COLOR_BGR2RGB)), plt.title('Merah')
plt.subplot(224), plt.imshow(cv2.cvtColor(green_detection, cv2.COLOR_BGR2RGB)), plt.title('Hijau')
plt.show()*<br>
Kode di atas menggunakan plt.subplot untuk menampilkan empat subplot secara berdampingan dalam satu figur.
> Subplot pertama menampilkan citra kontras (brightened_image) dengan judul "Citra Kontras".
> Subplot kedua menampilkan hasil deteksi warna biru (blue_detection) dengan judul "Biru".
> Subplot ketiga menampilkan hasil deteksi warna merah (red_detection) dengan judul "Merah".
> Subplot keempat menampilkan hasil deteksi warna hijau (green_detection) dengan judul "Hijau".
plt.show() digunakan untuk menampilkan figur, keempat subplot tersebut.

#Konsep teori yang terkait pada project diatas
-
1. skema warna HSV
2. histogram warna
3. mendeteksi warna
4. operasi peningkatan kecerahan

sumber:
https://www.w3schools.com/python/
https://stackoverflow.com/questions/24852345/hsv-to-rgb-color-conversion
https://www.geeksforgeeks.org/visualizing-colors-in-images-using-histogram-in-python/
https://medium.com/@gowtham180502/how-to-detect-colors-using-opencv-python-98aa0241e713
https://www.google.co.id/?hl=id
https://stackoverflow.com/questions/32609098/how-to-fast-change-image-brightness-with-python-opencv
