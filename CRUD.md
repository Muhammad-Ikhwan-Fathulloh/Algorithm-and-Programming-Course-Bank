# Todo CRUD

## **Langkah 1: Versi Sederhana (Tanpa Fungsi)**

```python
# ============================================
# STEP 1: PROGRAM DASAR TODO LIST
# ============================================

# 1.1 Inisialisasi data
# Kita menggunakan list untuk menyimpan semua todo
todos = []  # List kosong untuk menyimpan tugas-tugas

# 1.2 Program utama dengan perulangan while
while True:
    # Tampilkan menu
    print("\n=== TODO LIST ===")
    print("1. Lihat semua tugas")
    print("2. Tambah tugas baru")
    print("3. Hapus tugas")
    print("4. Keluar")
    
    # Minta input dari pengguna
    pilihan = input("Pilih menu (1-4): ")
    
    # 1.3 Gunakan if untuk menangani pilihan menu
    
    # Pilihan 1: LIHAT SEMUA TUGAS
    if pilihan == "1":
        print("\n--- Daftar Tugas ---")
        
        # Cek apakah list kosong
        if len(todos) == 0:  # Jika tidak ada data
            print("Tidak ada tugas")
        else:
            # Tampilkan semua tugas dengan perulangan for
            for i, tugas in enumerate(todos, 1):  # enumerate memberi nomor
                print(f"{i}. {tugas}")
    
    # Pilihan 2: TAMBAH TUGAS BARU
    elif pilihan == "2":
        print("\n--- Tambah Tugas Baru ---")
        
        # Minta input tugas baru
        tugas_baru = input("Masukkan tugas: ")
        
        # Validasi: jangan tambah jika kosong
        if tugas_baru.strip() != "":  # .strip() menghapus spasi di awal/akhir
            todos.append(tugas_baru)  # tambah ke list
            print(f"Tugas '{tugas_baru}' berhasil ditambahkan!")
        else:
            print("Tugas tidak boleh kosong!")
    
    # Pilihan 3: HAPUS TUGAS
    elif pilihan == "3":
        print("\n--- Hapus Tugas ---")
        
        # Cek dulu apakah ada tugas
        if len(todos) == 0:
            print("Tidak ada tugas untuk dihapus")
        else:
            # Tampilkan semua tugas untuk dipilih
            print("Daftar tugas:")
            for i, tugas in enumerate(todos, 1):
                print(f"{i}. {tugas}")
            
            # Minta nomor tugas yang akan dihapus
            try:
                # Coba konversi input ke angka
                nomor = int(input("Nomor tugas yang akan dihapus: "))
                
                # Validasi nomor
                if 1 <= nomor <= len(todos):
                    # Hapus tugas (kurangi 1 karena list mulai dari 0)
                    tugas_terhapus = todos.pop(nomor - 1)
                    print(f"Tugas '{tugas_terhapus}' berhasil dihapus!")
                else:
                    print(f"Nomor harus antara 1 sampai {len(todos)}")
                    
            except ValueError:  # Jika input bukan angka
                print("Masukkan nomor yang valid!")
    
    # Pilihan 4: KELUAR
    elif pilihan == "4":
        print("Terima kasih! Program selesai.")
        break  # Keluar dari perulangan while
    
    # Pilihan tidak valid
    else:
        print("Pilihan tidak valid! Pilih 1-4.")
```

## **Langkah 2: Tambahkan Fitur Status (Selesai/Belum)**

```python
# ============================================
# STEP 2: TODO DENGAN STATUS
# ============================================

# 2.1 Ubah struktur data dari string menjadi dictionary
todos = []  # Sekarang setiap todo adalah dictionary

while True:
    print("\n=== TODO LIST DENGAN STATUS ===")
    print("1. Lihat semua tugas")
    print("2. Tambah tugas baru")
    print("3. Tandai selesai/belum")
    print("4. Hapus tugas")
    print("5. Lihat tugas aktif (belum selesai)")
    print("6. Keluar")
    
    pilihan = input("Pilih menu (1-6): ")
    
    # Pilihan 1: LIHAT SEMUA
    if pilihan == "1":
        print("\n--- Semua Tugas ---")
        
        if len(todos) == 0:
            print("Tidak ada tugas")
        else:
            for i, tugas in enumerate(todos, 1):
                # Tugas sekarang adalah dictionary
                status = "(Selesai)" if tugas['selesai'] else "(Belum)"
                print(f"{i}. {tugas['nama']} {status}")
    
    # Pilihan 2: TAMBAH TUGAS BARU
    elif pilihan == "2":
        print("\n--- Tambah Tugas Baru ---")
        nama_tugas = input("Masukkan nama tugas: ")
        
        if nama_tugas.strip() != "":
            # Buat dictionary untuk tugas baru
            tugas_baru = {
                'nama': nama_tugas,
                'selesai': False  # Default: belum selesai
            }
            
            todos.append(tugas_baru)
            print(f"Tugas '{nama_tugas}' ditambahkan!")
    
    # Pilihan 3: UBAH STATUS
    elif pilihan == "3":
        print("\n--- Ubah Status Tugas ---")
        
        if len(todos) == 0:
            print("Tidak ada tugas")
        else:
            # Tampilkan tugas yang bisa diubah statusnya
            for i, tugas in enumerate(todos, 1):
                status = "Selesai" if tugas['selesai'] else "Belum"
                print(f"{i}. {tugas['nama']} - Status: {status}")
            
            try:
                nomor = int(input("Nomor tugas yang diubah: "))
                
                if 1 <= nomor <= len(todos):
                    # Ubah status (jika True jadi False, jika False jadi True)
                    todos[nomor - 1]['selesai'] = not todos[nomor - 1]['selesai']
                    
                    status_baru = "selesai" if todos[nomor - 1]['selesai'] else "belum selesai"
                    print(f"Status '{todos[nomor - 1]['nama']}' diubah menjadi {status_baru}")
                else:
                    print("Nomor tidak valid!")
                    
            except ValueError:
                print("Masukkan angka!")
    
    # Pilihan 4: HAPUS TUGAS
    elif pilihan == "4":
        # Sama seperti sebelumnya
        print("\n--- Hapus Tugas ---")
        
        if len(todos) == 0:
            print("Tidak ada tugas")
        else:
            for i, tugas in enumerate(todos, 1):
                print(f"{i}. {tugas['nama']}")
            
            try:
                nomor = int(input("Nomor tugas yang dihapus: "))
                
                if 1 <= nomor <= len(todos):
                    tugas_terhapus = todos.pop(nomor - 1)
                    print(f"Tugas '{tugas_terhapus['nama']}' dihapus!")
                else:
                    print("Nomor tidak valid!")
                    
            except ValueError:
                print("Masukkan angka!")
    
    # Pilihan 5: LIHAT TUGAS AKTIF
    elif pilihan == "5":
        print("\n--- Tugas Aktif (Belum Selesai) ---")
        
        # Cari tugas yang belum selesai
        tugas_aktif = []
        for tugas in todos:
            if not tugas['selesai']:  # Jika selesai = False
                tugas_aktif.append(tugas)
        
        if len(tugas_aktif) == 0:
            print("Semua tugas sudah selesai!")
        else:
            for i, tugas in enumerate(tugas_aktif, 1):
                print(f"{i}. {tugas['nama']}")
    
    # Pilihan 6: KELUAR
    elif pilihan == "6":
        print("Sampai jumpa!")
        break
    
    else:
        print("Pilihan tidak valid!")
```

## **Langkah 3: Tambahkan ID Unik untuk Setiap Tugas**

```python
# ============================================
# STEP 3: TODO DENGAN ID UNIK
# ============================================

# 3.1 Inisialisasi
todos = []
id_counter = 1  # Untuk membuat ID yang unik

while True:
    print("\n=== TODO LIST DENGAN ID ===")
    print("1. Lihat semua tugas")
    print("2. Tambah tugas")
    print("3. Ubah status")
    print("4. Hapus tugas")
    print("5. Cari tugas")
    print("6. Keluar")
    
    pilihan = input("Pilih: ")
    
    # Pilihan 1: LIHAT SEMUA
    if pilihan == "1":
        print("\nID | Tugas | Status")
        print("-" * 30)
        
        for tugas in todos:
            status = "Selesai" if tugas['selesai'] else "Belum"
            print(f"{tugas['id']}  | {tugas['nama']} | {status}")
    
    # Pilihan 2: TAMBAH
    elif pilihan == "2":
        nama = input("\nNama tugas: ")
        
        if nama:
            # Buat tugas dengan ID unik
            tugas_baru = {
                'id': id_counter,
                'nama': nama,
                'selesai': False
            }
            
            todos.append(tugas_baru)
            print(f"Tugas ditambahkan dengan ID: {id_counter}")
            id_counter += 1  # Naikkan ID untuk tugas berikutnya
    
    # Pilihan 3: UBAH STATUS
    elif pilihan == "3":
        print("\n--- Ubah Status ---")
        
        # Tampilkan tugas yang belum selesai
        print("Tugas yang belum selesai:")
        for tugas in todos:
            if not tugas['selesai']:
                print(f"ID: {tugas['id']} - {tugas['nama']}")
        
        try:
            cari_id = int(input("Masukkan ID tugas: "))
            
            # Cari tugas berdasarkan ID
            ditemukan = False
            for tugas in todos:
                if tugas['id'] == cari_id:
                    tugas['selesai'] = not tugas['selesai']
                    status = "selesai" if tugas['selesai'] else "belum selesai"
                    print(f"Status tugas ID {cari_id} diubah menjadi {status}")
                    ditemukan = True
                    break
            
            if not ditemukan:
                print(f"Tugas dengan ID {cari_id} tidak ditemukan")
                
        except ValueError:
            print("Masukkan angka untuk ID!")
    
    # Pilihan 4: HAPUS
    elif pilihan == "4":
        try:
            hapus_id = int(input("\nMasukkan ID tugas yang dihapus: "))
            
            # Cari index tugas yang akan dihapus
            index_hapus = -1
            for i, tugas in enumerate(todos):
                if tugas['id'] == hapus_id:
                    index_hapus = i
                    break
            
            if index_hapus != -1:
                nama_hapus = todos[index_hapus]['nama']
                todos.pop(index_hapus)
                print(f"Tugas '{nama_hapus}' (ID: {hapus_id}) dihapus")
            else:
                print(f"Tugas dengan ID {hapus_id} tidak ditemukan")
                
        except ValueError:
            print("Masukkan angka!")
    
    # Pilihan 5: CARI
    elif pilihan == "5":
        keyword = input("\nCari tugas (nama): ").lower()
        
        hasil = []
        for tugas in todos:
            if keyword in tugas['nama'].lower():
                hasil.append(tugas)
        
        if len(hasil) == 0:
            print("Tidak ditemukan")
        else:
            print(f"Ditemukan {len(hasil)} hasil:")
            for tugas in hasil:
                status = "Selesai" if tugas['selesai'] else "Belum"
                print(f"ID: {tugas['id']} - {tugas['nama']} ({status})")
    
    # Pilihan 6: KELUAR
    elif pilihan == "6":
        print("Program selesai")
        break
```

## **Langkah 4: Program Lengkap dengan Fungsi**

```python
# ============================================
# STEP 4: PROGRAM LENGKAP DENGAN FUNGSI
# ============================================

# 4.1 Data Global
todos = []
next_id = 1

# 4.2 Definisi Fungsi

def tampilkan_menu():
    """Menampilkan menu utama"""
    print("\n" + "="*40)
    print("APLIKASI TODO LIST")
    print("="*40)
    print("1. Lihat semua tugas")
    print("2. Tambah tugas baru")
    print("3. Tandai selesai/belum")
    print("4. Hapus tugas")
    print("5. Lihat statistik")
    print("0. Keluar")

def lihat_semua_tugas():
    """Menampilkan semua tugas"""
    print("\n--- DAFTAR SEMUA TUGAS ---")
    
    if len(todos) == 0:
        print("Belum ada tugas")
        return
    
    print("No | ID | Tugas | Status")
    print("-" * 40)
    
    for i, tugas in enumerate(todos, 1):
        status = "Selesai" if tugas['selesai'] else "Belum"
        print(f"{i:2} | {tugas['id']:2} | {tugas['nama']:20} | {status}")

def tambah_tugas():
    """Menambahkan tugas baru"""
    global next_id
    
    print("\n--- TAMBAH TUGAS BARU ---")
    nama = input("Masukkan nama tugas: ").strip()
    
    if nama == "":
        print("Nama tugas tidak boleh kosong!")
        return
    
    # Buat tugas baru
    tugas_baru = {
        'id': next_id,
        'nama': nama,
        'selesai': False,
        'tanggal_dibuat': '2024-01-01'  # Contoh data tambahan
    }
    
    todos.append(tugas_baru)
    print(f"Tugas '{nama}' berhasil ditambahkan (ID: {next_id})")
    next_id += 1

def ubah_status_tugas():
    """Mengubah status tugas"""
    print("\n--- UBAH STATUS TUGAS ---")
    
    if len(todos) == 0:
        print("Belum ada tugas")
        return
    
    # Tampilkan tugas
    for tugas in todos:
        status = "✓" if tugas['selesai'] else " "
        print(f"ID: {tugas['id']} [{status}] {tugas['nama']}")
    
    try:
        cari_id = int(input("Masukkan ID tugas: "))
        
        # Cari tugas berdasarkan ID
        for tugas in todos:
            if tugas['id'] == cari_id:
                # Toggle status
                tugas['selesai'] = not tugas['selesai']
                
                if tugas['selesai']:
                    print(f"Tugas '{tugas['nama']}' ditandai SELESAI")
                else:
                    print(f"Tugas '{tugas['nama']}' ditandai BELUM SELESAI")
                return
        
        print(f"Tidak ditemukan tugas dengan ID {cari_id}")
        
    except ValueError:
        print("ID harus berupa angka!")

def hapus_tugas():
    """Menghapus tugas berdasarkan ID"""
    print("\n--- HAPUS TUGAS ---")
    
    if len(todos) == 0:
        print("Belum ada tugas")
        return
    
    try:
        hapus_id = int(input("Masukkan ID tugas yang akan dihapus: "))
        
        # Cari index tugas
        for i, tugas in enumerate(todos):
            if tugas['id'] == hapus_id:
                # Konfirmasi penghapusan
                konfirmasi = input(f"Yakin hapus '{tugas['nama']}'? (y/t): ")
                
                if konfirmasi.lower() == 'y':
                    tugas_terhapus = todos.pop(i)
                    print(f"Tugas '{tugas_terhapus['nama']}' berhasil dihapus")
                else:
                    print("Penghapusan dibatalkan")
                return
        
        print(f"Tidak ditemukan tugas dengan ID {hapus_id}")
        
    except ValueError:
        print("ID harus berupa angka!")

def lihat_statistik():
    """Menampilkan statistik tugas"""
    print("\n--- STATISTIK TUGAS ---")
    
    total = len(todos)
    
    if total == 0:
        print("Belum ada tugas")
        return
    
    # Hitung tugas selesai dan belum
    selesai = 0
    belum = 0
    
    for tugas in todos:
        if tugas['selesai']:
            selesai += 1
        else:
            belum += 1
    
    # Hitung persentase
    if total > 0:
        persen_selesai = (selesai / total) * 100
    else:
        persen_selesai = 0
    
    print(f"Total tugas     : {total}")
    print(f"Selesai         : {selesai}")
    print(f"Belum selesai   : {belum}")
    print(f"Persentase selesai: {persen_selesai:.1f}%")
    
    # Tampilkan tugas yang belum selesai
    if belum > 0:
        print("\nTugas yang belum selesai:")
        for tugas in todos:
            if not tugas['selesai']:
                print(f"  - {tugas['nama']} (ID: {tugas['id']})")

# 4.3 Program Utama
def main():
    """Fungsi utama yang menjalankan program"""
    print("SELAMAT DATANG DI APLIKASI TODO LIST")
    
    # Tambah data contoh
    global todos, next_id
    todos = [
        {'id': 1, 'nama': 'Belajar Python', 'selesai': True},
        {'id': 2, 'nama': 'Buat program CRUD', 'selesai': False},
        {'id': 3, 'nama': 'Baca dokumentasi', 'selesai': False}
    ]
    next_id = 4
    
    # Loop utama program
    while True:
        tampilkan_menu()
        pilihan = input("\nPilih menu (0-5): ")
        
        if pilihan == "1":
            lihat_semua_tugas()
        elif pilihan == "2":
            tambah_tugas()
        elif pilihan == "3":
            ubah_status_tugas()
        elif pilihan == "4":
            hapus_tugas()
        elif pilihan == "5":
            lihat_statistik()
        elif pilihan == "0":
            print("\nTerima kasih telah menggunakan program!")
            break
        else:
            print("Pilihan tidak valid! Silakan pilih 0-5.")
        
        # Tunggu sebelum kembali ke menu
        input("\nTekan Enter untuk kembali ke menu...")

# 4.4 Jalankan Program
if __name__ == "__main__":
    main()
```

## **Ringkasan Konsep yang Digunakan:**

### 1. **List** untuk menyimpan data:
```python
todos = []  # List kosong
todos.append(item)  # Menambah item
todos.pop(index)    # Menghapus item
```

### 2. **Dictionary** untuk struktur data yang kompleks:
```python
tugas = {
    'id': 1,
    'nama': 'Belajar Python',
    'selesai': False
}
```

### 3. **Perulangan** untuk mengakses data:
```python
# For loop biasa
for tugas in todos:
    print(tugas['nama'])

# For loop dengan index
for i, tugas in enumerate(todos, 1):
    print(f"{i}. {tugas['nama']}")
```

### 4. **Percabangan if** untuk logika program:
```python
if len(todos) == 0:  # Cek apakah kosong
    print("Tidak ada data")
elif pilihan == "1":  # Cek pilihan menu
    lihat_semua()
else:  # Default case
    print("Pilihan tidak valid")
```

### 5. **Fungsi** untuk modularitas:
```python
def nama_fungsi(parameter):
    # Kode fungsi
    return hasil
```
3. Jalankan program dan coba semua fitur
4. Lanjut ke **Langkah 2**, **3**, dan **4** untuk menambah kompleksitas
5. Modifikasi sesuai kebutuhan Anda sendiri
