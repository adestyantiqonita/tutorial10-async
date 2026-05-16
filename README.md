# Tutorial 10 - Asynchronous Programming

## Experiment 1.2: Understanding how it works

Output:
![Experiment 1.2](images/experiment1-2.png)

"hey hey!" muncul duluan sebelum "howdy!" padahal kodenya ditulis setelah spawn.
Ini karena spawn cuma mendaftarkan task ke antrian, belum langsung dijalankan.
Task baru beneran jalan waktu executor.run() dipanggil.
Jadi "hey hey!" di main thread langsung keeksekusi duluan, async task-nya nyusul belakangan.