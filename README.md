# Saliency Based Generative-Adversarial-Networks (GAN) Camouflage Generator
## Generator Corak Kamuflase dengan GAN (Generative-Adversarial-Networks) berbasis Model Saliency
oleh Bim Yusuf Karang

Teknik Informatika

Universitas Padjadjaran

Repo ini berisi penelitian tentang pengembangan model GAN (Generative-Adversarial-Networks) untuk mengenerasi corak kamuflase yang paling efektif berdasarkan input lingkungan. Penelitian ini dibagi menjadi dua tahap, tahap pembuktian kalau model prediksi atensi (saliency) dapat digunakan sebagai loss function pada GAN, lalu tahap pengembangan GAN itu sendiri. Sebelum memulai pengembangan model GAN, machine learning perlu mengetahui apakah hasil generasi sudah efektif untuk kemudian dievalusi untuk mengenerasi model yang lebih efektif. Oleh karena itu, kita membutuhkan sebuah fungsi differentiable yang dapat menilai efektivitas desain kamuflase.

## Tahap 1 : Pengembangan Model Saliency Mapping / Attention Prediction

Tujuan dari paper ini adalah komparasi 2 dimenasi antara model attention prediction dan metrik evaluasi yang dapat meniru penilaian manusia terhadap efektivitas kamuflase. Sebuah model dan metrik dikatakan berhasil meniru penilaian manusia jika mampu mengklasifikasikan dataset kamuflase sesuai dengan 4 kategori : Baseline, High, Medium, Low. Hasil akhir dari Tahap 1 ini adalah sebuah kesimpulan berupa "Metrik [X] yang dihitung menggunakan Model [Y] terbukti paling valid dengan korelasi [Z] terhadap persepsi manusia". Langkah-langkah pekerjaan tahap 1 ini dijabarkan sebagai berikut : 

  1. Pengumpulan dataset gambar berupa kamuflase dengan latar belakang
  2. Anotasi masking dataset gambar dengan class uniform, skin, property
  3. Preprocessing gambar
  4. Mapping Prediksi atensi pada gambar dengan kandidat model
  5. Evaluasi hasil mapping prediksi atensi dengan kandidat metrik evaluasi
  6. Mengevaluasi korelasi terbaik antara model prediksi atensi dan metrik evaluasi dengan persepsi manusia
  7. Melanjutkan pembangunan model GAN dengan loss function dari model prediksi atensi dan metrik evaluasi terpilih pada tahap 2

Tahap anotasi dan preprocessing data memiliki banyak kandidat metode. Seluruh kandidat metode ini akan dicoba sampai menghasilkan korelasi yang terbaik untuk menciptakan model yang semirip mungkin dengan hasil persepsi manusia.

Mengenai tata cara anotasi dataset dapat di lihat pada [Panduan Anotasi](panduan_anotasi.md)





