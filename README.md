# Visi-Komputer

Berikut adalah hasil proses dari paper yang saya pilih yang berjudul **Analysis of Image Processing Using Morphological Erosion and Dilation**

Platfrom yang saya gunakan disini adalah Google Colab

## Langkah Pertama
Install dan import library terlebih dahulu

```python
  !pip install opencv-python-headless
  import cv2
  import numpy as np
  import matplotlib.pyplot as plt
```

## Langkah Kedua
Upload gambar yang diinginkan

```python
  from google.colab import files
  uploaded = files.upload()
```

Untuk contoh gambar yang saya gunakan adalah seperti berikut:

![contoh gambar](https://github.com/user-attachments/assets/64cfcef5-da0d-41f2-8035-157b500bf170)

## Langkah Ketiga
Membaca dan mengkonversi ke Grayscale + Threshold Biner

```python
  image = cv2.imread(next(iter(uploaded)))
  gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
  _, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY_INV)
```

## Langkah Keempat
Structuring element dalam bentuk kernel

```python
  kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5,5))
```

## Langkah Kelima
Menjalankan Operasi Morfologi nya

```python
  dilation = cv2.dilate(binary, kernel, iterations=1)
  erosion = cv2.erode(binary, kernel, iterations=1)
  opening = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)
  closing = cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)
```

## Langkah Keenam
Menampilkan hasilnya

```python
  titles = ['Original', 'Dilation', 'Erosion', 'Opening', 'Closing']
  images = [binary, dilation, erosion, opening, closing]

  plt.figure(figsize=(15,5))
  for i in range(5):
      plt.subplot(1,5,i+1)
      plt.imshow(images[i], cmap='gray')
      plt.title(titles[i])
      plt.axis('off')
  plt.show()
```

dan berikut adalah hasil dari Google Colab nya
![image](https://github.com/user-attachments/assets/ecb98ebc-6e6d-44ed-aa7a-ed72f7a0355d)

### Penjelasan Secara Sederhana
Gambar Original  : Belum mengalami proses apapun

Gambar Dilation  : Objek membesar, celah kecil tersambung

Gambar Erosion   : Objek menyusut, noise kecil menghilang

Gambar Opening   : Menghilangkan noise latar depan (bintik kecil)

Gambar Closing   : Menutup celah dan lubang dalam objek
