Dokumen ini berisi panduan langkah demi langkah untuk menginstal dan menggunakan LabelMe, alat anotasi grafis berbasis Python, untuk keperluan pelabelan dataset.

### 1. Prasyarat
Pastikan Python sudah terinstal di komputer Anda.

Cek dengan mengetik di terminal: 
```python --version```

### 2. Membuat Virtual Environment
Buat virtual environment agar software LabelMe dapat berjalan dengan lancar: 
```python -m venv venv```

### 3. Aktifkan Virtual Environment
Perintah ini akan mengubah tampilan terminal Anda (biasanya ada tanda (venv) di sebelah kiri).

Untuk Windows : 
```venv\Scripts\activate```

macOS / Linux: 
```source venv/bin/activate```

### 4. Instalasi LabelMe
Setelah (venv) aktif, instal LabelMe menggunakan pip:
```pip install labelme```
