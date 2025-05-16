# Tutorial 8: Game Polishing and Balancing

## Proses Pengerjaan

Dalam tutorial ini, saya telah mengerjakan dua aspek penting dalam pengembangan game: game polishing dengan particle effects dan game balancing.

### 1. Creating Particles

#### 1.1 Environment Particle (Hujan)

Saya menambahkan efek hujan pada level dengan langkah-langkah berikut:

1. Menambahkan node `GPUParticles2D` ke root node Level 1
2. Menambahkan `ParticleProcessMaterial` pada node tersebut
3. Mengkonfigurasi properties particle untuk menciptakan efek hujan:
   - Amount: 100 (untuk memperbanyak jumlah partikel)
   - Lifetime: 4.0 (untuk membuat partikel bertahan lebih lama)
   - Scale max: 10.0 (untuk memperbesar ukuran partikel)
   - Emission Shape: Box dengan extents 2000 pada sumbu x (untuk menciptakan area hujan yang lebar)
   - Color: Biru keabu-abuan (#84a6b6)
   - Spread: 20 derajat (untuk mengontrol persebaran partikel)
   - Gravity: -500 (x) dan 500 (y) untuk membuat hujan miring ke kiri bawah
   - Visibility Rect: 2000 x 500 (untuk memastikan hujan tetap terlihat saat kamera bergerak)
   - Trail Enabled: True (untuk memberikan efek ekor pada partikel hujan)

#### 1.2 Player Trail Particle

Saya menambahkan efek trail saat player berjalan dengan langkah-langkah berikut:

1. Menambahkan node `GPUParticles2D` ke scene Player.tscn
2. Mengkonfigurasi properties untuk menciptakan efek trail:
   - Texture: brickGrey_small.png
   - Amount: 4 (jumlah partikel yang lebih sedikit untuk trail)
   - Lifetime: 0.5 (waktu hidup yang lebih singkat)
   - Gravity: -200 pada sumbu y (untuk membuat partikel terbang ke atas)
   - Spread: 180 derajat (untuk menyebar ke segala arah)
   - Initial Velocity: 50
   - Emission Shape: Box dengan extents 30 pada sumbu x
   - Posisi: di bagian kaki player (y = 30)

3. Mengubah script Player.gd untuk mengontrol emisi partikel:
   - Menambahkan referensi ke node partikel: `@onready var particle = $GPUParticles2D`
   - Mengaktifkan emisi hanya ketika player di lantai dan bergerak: `particle.set_emitting(true)`
   - Menonaktifkan emisi ketika player diam: `particle.set_emitting(false)`

### 2. Game Balancing

Untuk menyeimbangkan tingkat kesulitan game, saya melakukan balancing pada Spawner dengan langkah-langkah berikut:

1. Menempatkan spawner pada posisi strategis di level (x=1700, y=280)
2. Menguji game dengan spawn rate default (0.3 detik) dan menemukan bahwa terlalu sulit karena terlalu banyak musuh muncul
3. Mencoba spawn rate 2 detik dan menemukan bahwa terlalu mudah
4. Menemukan nilai optimal 1 detik yang memberikan tantangan namun masih memungkinkan player untuk menyelesaikan level

## Hasil Akhir

Setelah mengimplementasikan particle effects dan melakukan game balancing, game sekarang memiliki:

1. Efek visual hujan yang dinamis di sepanjang level
2. Trail partikel saat player berjalan yang menambah feedback visual
3. Tingkat kesulitan yang seimbang dengan spawn rate musuh yang optimal

Implementasi ini berhasil meningkatkan kualitas visual game dan memberikan pengalaman bermain yang lebih seimbang dan menyenangkan bagi pemain.

## Referensi

1. Dokumentasi Godot tentang GPUParticles2D: https://docs.godotengine.org/en/stable/classes/class_gpuparticles2d.html
2. Kenney Platformer Pack untuk aset tekstur partikel: https://kenney.nl/assets/platformer-pack-redux
