# Tutorial testnet Exorde Airdrop Finder

<p style="font-size:14px" align="right">
<a href="https://t.me/airdropfind" target="_blank">Join Telegram Airdrop Finder<img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
</p>

<p align="center">
  <img height="auto" width="auto" src="https://raw.githubusercontent.com/bayy420-999/airdropfind/main/NavIcon.png">
</p>

## Referensi

[Github resmi Exorde-Labs](https://github.com/exorde-labs/ExordeModuleCLI/)

[Pemasangan Anaconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)

[Pemasangan Docker](https://docs.docker.com/engine/install/ubuntu/)

## Persyaratan perangkat keras

| Komponen | Spesifikasi minimal |
|----------|---------------------|
|CPU|Intel Core i3 or i5|
|RAM|4 GB DDR4 RAM|
|Penyimpanan|500 GB HDD|
|Koneksi|100 Mbit/s port|

| Komponen | Spesifikasi rekomendasi |
|----------|---------------------|
|CPU|Intel Core i7-8700 Hexa-Core|
|RAM|64 GB DDR4 RAM|
|Penyimpanan|2 x 1 TB NVMe SSD|
|Koneksi|1 Gbit/s port|

## Persyaratan perangkat lunak

| Komponen | Spesifikasi minimal |
|----------|---------------------|
|Sistem Operasi|Ubuntu 16.04|

| Komponen | Spesifikasi rekomendasi |
|----------|---------------------|
|Sistem Operasi|Ubuntu 18.04 atau lebih tinggi|

Terdapat 2 opsi pemasang yaitu pemasangan menggunakan `Anaconda` dan pemasangan menggunakan `Docker`, Anda hanya perlu memilih salah satu opsi.

## Pemasangan menggunakan Anaconda

### Pasang dependensi

Jalankan perintah dibawah untuk memasang dependensi

```
apt install python3 python3-pip git screen
pip install --upgrade pip
```

### Unduh dan jalankan Anaconda

```
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
bash Anaconda3-2022.10-Linux-x86_64.sh
bash
```

> Jika ada prompt pertanyaan ketik `yes` sampai proses pemasangan selesai


### Unduh paket Exorde

```
git clone https://github.com/exorde-labs/ExordeModuleCLI.git
```

### Masuk ke folder Exorde

```
cd ExordeModuleCLI
```

### Buat enviromen Exorde

```
conda create --name exorde-env python=3.9
```

### Aktifkan enviromen Exorde

```
conda activate exorde-env
```

### Pasang dependensi python

```
pip install -r requirements.txt
```

### Jalankan validator

Buka layar baru menggunakan `screen`

```
screen -Rd exorde
```

Lalu jalankan perintah dibawah

```
python Launcher.py -m ALAMAT_ETH_ANDA -l LEVEL_LOGGING
```

contoh:

```
python Launcher.py -m 0x0000002bf118391ebe8d37f7ab2a4d8ae1c45aa3 -l 4
```

Jika anda ingin keluar dari terminal tekan 

```CTRL + A + D```

Jika anda ingin masuk ke terminal gunakan perintah 

```
screen -r exorde
```

> Ganti `ALAMAT_ETH_ANDA` dengan alamat eth anda, untuk logging bisa diisi 0, 1, 2, 3, 4 detail logging akan saya jelaskan [dibawah](https://github.com/bayy420-999/tutorial-testnet-exorde-airdropfinder#logging)

## Pemasangan menggunakan Docker

### Update apt

```
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    screen \
    git
```

### Tambahkan kunci GPG Docker resmi

```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```


### Setting repositori

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Unduh dan pasang Docker

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Cek apakah Docker sudah terpasang

```
docker --version
```

> Jika keluar pesan seperti ini `Docker version 20.10.20, build 9fdeb9c` artinya Docker sudah terpasang

### Unduh paket Exorde

```
git clone https://github.com/exorde-labs/ExordeModuleCLI.git
```

### Masuk ke folder Exorde

```
cd ExordeModuleCLI
```

### Bangun Docker

```
docker build -t exorde-cli . 
```

### Jalankan validator

Buka layar baru menggunakan `screen`

```
screen -Rd exorde
```

Lalu jalankan perintah dibawah

```
docker run -it exorde-cli -m ALAMAT_ETH_ANDA -l LEVEL_LOGGING
```

contoh:

```
docker run -it exorde-cli -m 0x0000002bf118391ebe8d37f7ab2a4d8ae1c45aa3 -l 4
```

Jika anda ingin keluar dari terminal tekan 

```CTRL + A + D```

Jika anda ingin masuk ke terminal gunakan perintah 

```
screen -r exorde
```

> Ganti `ALAMAT_ETH_ANDA` dengan alamat eth anda, untuk logging bisa diisi 0, 1, 2, 3, 4 detail logging akan saya jelaskan [dibawah](https://github.com/bayy420-999/tutorial-testnet-exorde-airdropfinder#logging)


## Logging

| Logging level | Keterangan |
|---------------|------------|
|0|Tidak ada log|
|1|Log biasa|
|2|Log validasi|
|3|Log validasi dan scrapping|
|4|Log validasi (detail) + log scrapping (untuk troubleshoot)

> Saya menyarankan menggunakan Logging level 4 agar mempermudah troubleshoot jika ada masalah

