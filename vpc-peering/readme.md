
## Step Setup VPC Peering
1. Buat keypair untuk akses EC2 di kedua Region (jakarta & singapore)
2. Sesuaikan cloudformation script untuk part jakarta dan singapore 
2. Deploy tiap yaml script di masing2 region (jakarta & singapore) di cloudformation
3. Request VPC Peering di salah satu region (e.g. jakarta)
4. Masuk ke VPC region lainnya (e.g. singapore) dan accept VPC peering request
5. Masuk ke VPC -> Route table -> pilih routing terkait VPC Peering, tambahkan rule ke destination 10.0.0.0/16 target kan ke pcx-XXX
6. Pindah region ke (e.g. jakarta) masuk ke VPC -> Route table -> pilih routing terkait VPC Peering, tambahkan rule ke destination 10.1.0.0/16 target kan ke pcx-XXX
7. Masuk ke instance (e.g. jakarta EC2) and test the connection using ping using IP private