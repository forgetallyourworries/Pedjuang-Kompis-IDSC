---
name: 'Feature Request: OptiGuard Enhancement'
about: Suggest an idea for this projectGunakan template ini untuk mengusulkan penambahan
  fitur baru pada pipeline AI OptiGuard.
title: '[FEATURE] Implement MathGradCAM to Enable "Transparent Screening" in OptiGuard
  ("The Insights")'
labels: ''
assignees: forgetallyourworries

---

### Is your feature request related to a problem? Please describe.
Ya, fitur ini adalah langkah final untuk mewujudkan visi utama proyek kita: **OptiGuard**. Sesuai dengan spesifikasi *Tech Report* IDSC 2026, model ini harus bertransisi dari *black-box* AI menjadi sistem yang **"Clinical-Ready"** dan **"Transparent"**. 

Saat ini, OptiGuard telah berhasil mencapai status **"Quality-Aware"** (mengintegrasikan *Quality Score* FundusQ-Net dari dataset HYGD) dan mencetak performa klasifikasi yang tinggi (AUROC 0.9296) melalui optimasi *Focal Loss* dan *F1-Max Thresholding* di angka 0.4555. Namun, untuk memenuhi kriteria penyampaian **"The Insights"**, OptiGuard harus mampu memberikan penjelasan visual (*saliency maps*) mengenai area anatomi mata mana yang memicu prediksi Glaucomatous Optic Neuropathy (GON+). Transparansi ini mutlak diperlukan agar keputusan AI dapat dipercaya dan diverifikasi oleh tenaga medis profesional.

### Describe the solution you'd like
Saya mengusulkan implementasi modul kustom **MathGradCAM** secara *from-scratch* pada arsitektur OptiGuard untuk mewujudkan fitur *"Transparent Screening"*. Rencana eksekusi teknisnya meliputi:

1. **Gradient Unlocking:** Memaksa pelacakan parameter (`requires_grad_()`) pada blok *attention / transformer* terakhir dari *backbone* Swin Transformer milik OptiGuard yang sebelumnya di-*freeze*.
2. **Feature Extraction:** Mengekstrak gradien spasial untuk menghasilkan peta aktivasi panas (*heatmap*) berwarna.
3. **Clinical Overlay:** Melakukan *overlay* (penumpukan) *heatmap* tersebut di atas citra fundus asli pasien (resolusi 224x224).
4. **Reporting:** Menyimpan dan menampilkan citra hasil *overlay* yang memuat informasi tebakan, label asli, dan probabilitas klinis ke dalam direktori `/insights` di repositori.

Tujuannya adalah membuktikan secara transparan bahwa OptiGuard mendiagnosis GON dengan berfokus pada fitur anatomi yang benar di area *optic disc*, bukan karena *shortcut learning*, artefak, atau *noise* pencahayaan pada citra.

### Describe alternatives you've considered
Beberapa alternatif visualisasi yang telah dievaluasi:
* **Occlusion Testing:** Metode yang menggeser sebuah jendela (*window*) ke seluruh area citra untuk memetakan bagian yang paling memengaruhi probabilitas model. Komputasinya jauh lebih berat dan kurang efisien untuk inferensi *real-time* dibandingkan Grad-CAM.
* **Attention Rollout:** Teknik bawaan untuk Vision Transformer. Namun, teknik ini terkadang kurang spesifik dan cenderung menyebar saat melokalisasi area kecil di sekitar *optic disc* jika dibandingkan dengan pendekatan kalkulus berbasis gradien.

### Additional context
Dalam praktik klinis, dokter spesialis mata mendiagnosis glaukoma dengan mengevaluasi perubahan struktural pada *optic disc*, khususnya dengan mendeteksi kerusakan atau penipisan pada tepi neuroretinal bagian inferior dan superior (*inferior and superior regions of the neuroretinal rim*).

Melalui eksekusi **Tahap 6** dari *pipeline* kita, kita akan memverifikasi apakah *hot spots* (titik nyala) dari `MathGradCAM` OptiGuard secara presisi selaras dengan area inferior dan superior tersebut. Jika terbukti, justifikasi klinis kita pada sesi presentasi final IDSC 2026 (**The Impact**) akan menjadi sangat solid dan tidak terbantahkan.
