# HR Employee Attrition Analysis

> **Kenapa karyawan resign, dan siapa yang paling berisiko resign berikutnya?**
> Analisis end-to-end (cleaning → EDA → risk segmentation → rekomendasi bisnis) pada 1,470 karyawan.

![Risk Segmentation](images/chart_risk_segmentation.png)

## Business Problem

Sebuah perusahaan teknologi menengah mencatat **attrition rate 16.1%**, sedikit di atas rata-rata industri (10-15%). Tim HR ingin tahu:

1. Di bagian mana attrition paling parah?
2. Faktor apa yang paling berkorelasi dengan keputusan resign?
3. Bisakah karyawan berisiko tinggi diidentifikasi **sebelum** mereka resign?
4. Aksi retensi apa yang bisa langsung dijalankan?

*(Skenario bisnis ini fiktif, dibuat untuk keperluan studi kasus portofolio.)*

## Key Findings

| Temuan | Angka |
|---|---|
| Attrition rate keseluruhan | **16.1%** (237 dari 1,470 karyawan) |
| Role paling berisiko | **Sales Representative: 39.8%** |
| Efek overtime | **30.5%** (lembur) vs **10.4%** (tidak lembur), sekitar 3x lipat |
| Periode paling kritis | 2 tahun pertama masa kerja (**29.8%**) |
| Gaji di bawah 3K | **28.6%** |
| Segmen **High Risk** (126 karyawan) | **52.4%** vs **5.8%** di segmen Low Risk |

![Attrition by Job Role](images/chart_jobrole.png)

![Overtime](images/chart_overtime.png)

## Approach

1. **Data Cleaning**: tidak ada missing value maupun duplikat. 3 kolom konstan dibuang (`EmployeeCount`, `Over18`, `StandardHours`). Ditambah kolom turunan `IncomeBand`, `TenureBand`, `AttritionFlag`.
2. **EDA**: attrition rate dipecah per departemen, job role, overtime, income, tenure.
3. **Risk Segmentation**: skor risiko rule-based (0-7) dari 7 faktor: overtime, kepuasan kerja rendah, work-life balance buruk, tenure pendek, gaji rendah, jarak rumah jauh, lama tidak dipromosikan. Skor lalu dikelompokkan jadi Low (0-1), Medium (2-3), High (4+).
4. **Rekomendasi**: diterjemahkan jadi aksi konkret untuk HR.

Skor dibuat sengaja sederhana dan mudah dijelaskan ke non-teknis, bukan black-box model.

## Business Recommendations

1. Audit beban kerja dan kebijakan lembur, terutama di Sales dan Laboratory.
2. Perkuat onboarding dan mentoring di 24 bulan pertama.
3. Evaluasi struktur gaji untuk role dengan income di bawah 3K.
4. Program retensi khusus (1-on-1 check-in, jalur karier jelas) untuk 126 karyawan High Risk.
5. Review siklus promosi bagi karyawan yang lebih dari 5 tahun belum naik jabatan.

## Repository Contents

| File | Isi |
|---|---|
| `HR_Attrition_Analysis.ipynb` | Notebook Python lengkap (cleaning, EDA, segmentation) dengan narasi dan visualisasi |
| `HR_Attrition_Dashboard.xlsx` | Dashboard Excel berbasis formula (COUNTIFS) dengan chart |
| `HR_Attrition_Case_Study.docx` | Laporan case study naratif |
| `cleaned_hr_attrition.csv` | Dataset hasil cleaning (dipakai oleh notebook) |
| `images/` | Chart yang dipakai di README |

## Tools

Python (pandas, matplotlib), Excel (formula COUNTIFS dan native chart), Jupyter Notebook.

## How to Run

```bash
pip install pandas matplotlib jupyter
jupyter notebook HR_Attrition_Analysis.ipynb
```

Pastikan `cleaned_hr_attrition.csv` berada di folder yang sama dengan notebook.

## Limitations

- Dataset adalah snapshot satu titik waktu, sehingga tren dari waktu ke waktu tidak tertangkap.
- Analisis bersifat korelasional, bukan kausal. Perlu data pendukung seperti exit interview untuk memastikan sebab-akibat.
- Risk score berbasis aturan. Langkah lanjutan yang masuk akal: model klasifikasi (Logistic Regression / Random Forest) untuk probabilitas yang lebih presisi.

## Dataset

[IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) (Kaggle). Dataset fiktif buatan IBM data scientists.

## Author

**Joshua Naibaho**, Sistem Informasi
GitHub: [@joshnaibaho294-svg](https://github.com/joshnaibaho294-svg)
