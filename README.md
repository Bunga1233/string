# STRING
![Cuplikan layar 2025-04-14 143026](https://github.com/user-attachments/assets/1bd74e2f-b539-43fa-a768-7817f3b3086b)

# Deskripsi
Program ini adalah contoh sederhana yang ditulis dalam bahasa Assembly untuk Linux 32-bit. Program ini mencetak string "bellshade" ke terminal dan kemudian keluar dengan status sukses.

# Cara Compile dan Jalankan
Untuk mengompilasi dan menjalankan program ini di Linux (32-bit), ikuti langkah-langkah berikut:

**1. Compile file Assembly:**
bash
Copy
Edit
nasm -f elf32 -o bellshade.o bellshade.asm

**2. Link file objek menjadi executable:**
bash
Copy
Edit
ld -m elf_i386 -o bellshade bellshade.o

**3. Jalankan program:**
bash
Copy
Edit
./bellshade

# Struktur Program
Program ini terdiri dari dua bagian utama:

**1. Bagian** .text: Di sini kita menulis kode program yang akan dijalankan.

**2.Bagian** .data: Berisi data statis, seperti string yang ingin ditampilkan.

# Penjelasan Kode
**1. Bagian** .*text* — **Kode Program**

section .text

    global _start       ; Titik masuk untuk linker

 • section .text: Bagian kode yang berisi instruksi untuk dijalankan.

 • global _start: Menandai _start sebagai titik masuk utama program, yang dibutuhkan oleh linker.

**2. Label** _start — **Titik Masuk Program**

   _start:

 • Label _*start* adalah titik awal eksekusi program yang akan dipanggil pertama kali setelah program dijalankan.

**3. Menulis Pesan ke Layar (stdout)**

  mov edx, len     ; Panjang pesan

  mov ecx, msg     ; Alamat pesan

  mov ebx, 1       ; File descriptor 1 (stdout)

  mov eax, 4       ; Syscall write

  int 0x80         ; Panggil kernel

 • mov edx, len: Memasukkan panjang pesan ke dalam register EDX.

 • mov ecx, msg: Menyimpan alamat pesan (msg) dalam register ECX.

 • mov ebx, 1: Menetapkan stdout (terminal) sebagai tempat output.

 • mov eax, 4: Menetapkan syscall write (nomor 4) ke dalam register EAX.

 • int 0x80: Melakukan interrupt untuk memanggil kernel dan menulis pesan ke layar terminal.

**4. Keluar dari Program**

 
 mov eax, 1       ; Syscall exit
 
 xor ebx, ebx     ; Nilai keluar 0
 
 int 0x80         ; Panggil kernel
 
 • mov eax, 1: Menetapkan syscall exit (nomor 1) untuk mengakhiri program.

 • xor ebx, ebx: Mengatur register EBX ke 0, yang menandakan keluar dengan status 0 (berhasil).

 • int 0x80: Melakukan interrupt untuk memanggil kernel dan keluar dari program.

**5. Bagian** .data — **Data Pesan**


 section .data
 
 msg db "bellshade", 0xA     ; Pesan + newline
 
 len equ $ - msg              ; Hitung panjang pesan
 
 • msg db "bellshade", 0xA: Mendefinisikan string "bellshade" dengan tambahan newline (0xA).

 • len equ $ - msg: Menghitung panjang string dengan mengurangkan alamat string (msg) dari posisi saat ini ($).

# Kesimpulan
 Program ini adalah contoh sederhana yang menunjukkan bagaimana cara menulis program di Assembly untuk Linux, menampilkan pesan di terminal, dan keluar dengan status sukses


