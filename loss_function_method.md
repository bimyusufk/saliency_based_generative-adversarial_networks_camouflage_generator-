## Camouflage Generation via Differentiable Perceptual Loss

Repositori ini berisi implementasi modular untuk Generative Adversarial Network (GAN) yang dirancang khusus untuk menggenerasi pola kamuflase yang efektif. Sistem ini menggunakan fungsi kerugian majemuk (multi-objective loss function) yang bersifat differentiable, memungkinkan optimasi gradien langsung terhadap simulasi visual manusia.

### Struktur Direktori
Berikut adalah struktur teknis dari modul optimasi dan evaluasi proyek ini:

```
project_root/
│
├── losses/                  # [CORE] Modul Loss Function (Differentiable)
│   ├── __init__.py
│   ├── saliency_loss.py     # Optimasi penghindaran deteksi (via SALICON)
│   ├── style_loss.py        # Optimasi kemiripan tekstur (via VGG Gram Matrix)
│   ├── smoothness_loss.py   # Regularisasi noise (via Total Variation)
│   └── composite_loss.py    # Manajer pembobotan loss (Weighted Sum)
│
├── metrics/                 # [EVAL] Modul Validasi (Inference Only)
│   ├── __init__.py
│   └── deepgaze_metric.py   # Evaluator "Gold Standard" (via DeepGaze IIE)
│
└── train.py                 # Loop pelatihan utama
```

### Deskripsi Teknis Modul
Setiap modul dalam folder losses/ diturunkan dari torch.nn.Module untuk memastikan kompatibilitas dengan mekanisme autograd PyTorch.

#### 1. losses/saliency_loss.py (Detection Evasion)

Modul ini bertanggung jawab untuk meminimalkan probabilitas deteksi visual manusia.

Model Basis: SALICON (Saliency in Context).
Alasan Teknis: Dipilih menggantikan DeepGaze untuk fase training karena arsitekturnya yang lebih ringan (efisiensi VRAM) dan gradien yang lebih stabil untuk backpropagation.

Mekanisme: Menghitung Mean Saliency Score hanya pada area mask kamuflase. Generator dihukum jika area kamuflase memiliki nilai saliency tinggi.

#### 2. losses/style_loss.py (Texture Blending)

Modul ini memaksa pola kamuflase untuk "melebur" secara statistik dengan latar belakang.
Model Basis: VGG-19 (Pre-trained on ImageNet).
Konsep Matematis: Menggunakan Gram Matrix ($G$) dari feature maps layer konvolusi.

Metrik: Frobenius Norm dari selisih antara $G_{generated}$ dan $G_{background}$. Ini memastikan statistik tekstur (bukan posisi piksel) identik.

#### 3. losses/smoothness_loss.py (Adversarial Defense)

Modul regularisasi untuk mencegah adversarial artifacts.
Metode: Total Variation (TV) Loss.

Fungsi: Menghukum perbedaan nilai piksel tetangga yang ekstrem. Tanpa ini, GAN cenderung memproduksi high-frequency noise yang menipu model saliency tetapi terlihat tidak natural bagi mata manusia.

#### 4. losses/composite_loss.py (Loss Manager)

Modul orkestrasi yang menggabungkan ketiga loss di atas menjadi satu skalar untuk optimasi Generator.

Formulasi:
$$L_{total} = \alpha \cdot L_{saliency} + \beta \cdot L_{style} + \gamma \cdot L_{TV}$$

Fleksibilitas: Memungkinkan penyetelan hyperparameter ($\alpha, \beta, \gamma$) secara dinamis tanpa mengubah kode inti model.

#### 5. metrics/deepgaze_metric.py (Validation)

Modul ini TIDAK digunakan untuk training, melainkan sebagai validator independen.

Model Basis: DeepGaze IIE.
Peran: Bertindak sebagai "Juri Akhir". Karena DeepGaze dilatih pada data eye-tracking biologis (bukan 
proksi mouse seperti SALICON), skor dari modul ini memberikan validitas ilmiah yang lebih tinggi untuk klaim efektivitas kamuflase dalam paper.