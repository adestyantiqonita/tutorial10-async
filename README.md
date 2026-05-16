# Tutorial 10 - Asynchronous Programming

## Experiment 1.2: Understanding how it works

Output:
![Experiment 1.2](images/experiment1-2.png)

"hey hey!" muncul duluan sebelum "howdy!" padahal kodenya ditulis setelah spawn.
Ini karena spawn cuma mendaftarkan task ke antrian, belum langsung dijalankan.
Task baru beneran jalan waktu executor.run() dipanggil.
Jadi "hey hey!" di main thread langsung keeksekusi duluan, async task-nya nyusul belakangan.

## Experiment 1.3: Multiple Spawn and removing drop

### Multiple Spawn
![Experiment 1.3 Multiple Spawn](images/experiment1-3-spawn.png)

Ketiga task jalan secara concurrent. howdy1, howdy2, howdy3 muncul berurutan,
tapi urutan done-nya tidak tentu karena ketiga task berjalan bersamaan dan selesai
sesuai jadwal masing-masing.

### Removing drop(spawner)
![Experiment 1.3 No Drop](images/experiment1-3-nodrop.png)

Tanpa drop(spawner), program tetap berjalan normal karena spawner otomatis di-drop
saat keluar dari scope main(). Fungsi drop(spawner) dipakai untuk memberi sinyal
ke executor bahwa tidak ada task baru lagi, sehingga executor tahu kapan harus berhenti.

## Experiment 2.1: Original code, and how it run

### Cara menjalankan:
- Jalankan server: `cargo run --bin server` di folder `broadcast-chat`
- Jalankan client (bisa lebih dari satu): `cargo run --bin client`

### Hasil:
![Server](images/experiment2-1-server.png)
![Client](images/experiment2-1-client.png)

Server menerima koneksi dari semua client dan mem-broadcast setiap pesan yang masuk
ke semua client yang terhubung. Jadi kalau satu client kirim pesan, semua client lain
bakal nerima pesan yang sama.