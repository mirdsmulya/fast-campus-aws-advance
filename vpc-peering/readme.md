# Panduan Setup VPC Peering

## Ringkasan

Panduan ini akan membantu Anda dalam mengatur VPC peering antara dua region AWS: Jakarta (`ap-southeast-3`) dan Singapura (`ap-southeast-1`). Setelah menyelesaikan langkah-langkah ini, VPC di kedua region tersebut akan terhubung, memungkinkan instance EC2 di dalamnya untuk saling berkomunikasi secara privat.

## Prasyarat

- AWS Management Console.
- Akun AWS yang sudah ada dengan izin yang sesuai.

## Langkah 1: Buat Key Pair untuk Akses EC2

1. **Buat Key Pair di Jakarta (`ap-southeast-3`):**
   - Masuk ke layanan **EC2** di AWS Management Console.
   - Pilih **Key Pairs** dari menu di sebelah kiri.
   - Klik **Create Key Pair**.
   - Beri nama key pair (misalnya, `jakarta-keypair`).
   - Unduh file `.pem` dan simpan dengan aman.

2. **Buat Key Pair di Singapura (`ap-southeast-1`):**
   - Pindah ke region Singapura di AWS Management Console.
   - Ulangi langkah di atas untuk membuat key pair baru (misalnya, `singapore-keypair`).
   - Unduh file `.pem` dan simpan dengan aman.

## Langkah 2: Deploy Script CloudFormation

1. **Deploy Script CloudFormation untuk Jakarta:**
   - Pindah ke region Jakarta (`ap-southeast-3`).
   - Buka **CloudFormation** di AWS Management Console.
   - Klik **Create Stack** dan unggah script YAML untuk Jakarta.
   - Masukkan parameter yang diperlukan, termasuk `KeyPairName` yang Anda buat untuk Jakarta.
   - Selesaikan proses pembuatan stack.

2. **Deploy Script CloudFormation untuk Singapura:**
   - Pindah ke region Singapura (`ap-southeast-1`).
   - Buka **CloudFormation** dan ulangi proses dengan script YAML untuk Singapura.
   - Masukkan parameter yang diperlukan, termasuk `KeyPairName` yang Anda buat untuk Singapura.
   - Selesaikan proses pembuatan stack.

## Langkah 3: Request VPC Peering

1. **Mulai Request VPC Peering di Jakarta:**
   - Di AWS Management Console, navigasikan ke **VPC** -> **Peering Connections** di region Jakarta.
   - Klik **Create Peering Connection**.
   - Setel requester VPC sebagai VPC Jakarta dan pilih VPC Singapura sebagai accepter.
   - Ajukan request tersebut.

## Langkah 4: Terima Request VPC Peering

1. **Terima Request Peering di Singapura:**
   - Pindah ke region Singapura di AWS Management Console.
   - Navigasikan ke **VPC** -> **Peering Connections**.
   - Temukan request peering dari Jakarta dan klik **Accept Request**.

## Langkah 5: Perbarui Route Tables untuk VPC Peering

1. **Perbarui Route Table di Singapura:**
   - Di region Singapura, navigasikan ke **VPC** -> **Route Tables**.
   - Pilih route table yang terkait dengan VPC Singapura.
   - Klik **Edit Routes**.
   - Tambahkan rute baru:
     - **Destination:** `10.0.0.0/16` (CIDR block dari VPC Jakarta).
     - **Target:** Pilih VPC Peering Connection (misalnya, `pcx-XXX`).
   - Simpan perubahan.

2. **Perbarui Route Table di Jakarta:**
   - Pindah kembali ke region Jakarta.
   - Navigasikan ke **VPC** -> **Route Tables**.
   - Pilih route table yang terkait dengan VPC Jakarta.
   - Klik **Edit Routes**.
   - Tambahkan rute baru:
     - **Destination:** `10.1.0.0/16` (CIDR block dari VPC Singapura).
     - **Target:** Pilih VPC Peering Connection (misalnya, `pcx-XXX`).
   - Simpan perubahan.

## Langkah 6: Uji Koneksi VPC Peering

1. **SSH ke Instance EC2 di Jakarta:**
   - Gunakan file `.pem` yang terkait dengan key pair Jakarta untuk SSH ke instance EC2 di region Jakarta.

2. **Uji Koneksi:**
   - Ping alamat IP privat dari instance EC2 di region Singapura dari instance EC2 di Jakarta.
   - Contoh perintah:
     ```bash
     ping <IP-Privat-Singapura>
     ```
   - Jika ping berhasil, koneksi VPC peering berfungsi dengan baik.

## Kesimpulan

Setelah menyelesaikan langkah-langkah ini, VPC Anda di Jakarta dan Singapura seharusnya sudah terpeering dan dapat berkomunikasi secara privat. Pastikan security group dan network ACL dikonfigurasi untuk memungkinkan lalu lintas antar instance sesuai kebutuhan.
