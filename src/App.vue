<script setup lang="ts">
import { Modal, type ModalOptions } from 'flowbite';
import { onMounted, ref } from 'vue';

const modal = ref<Modal>();

interface IUser {
  username: string;
  password: string;
}

const message = ref<string>("");

const form = ref<IUser>({
  username: "",
  password: ""
})

const initModal = () => {


  // set the modal menu element
  const $targetEl = document.getElementById('authentication-modal');

  // options with default values
  const options: ModalOptions = {
    placement: "center",
    backdropClasses:
      'bg-gray-900/50 dark:bg-gray-900/80 fixed inset-0 z-40 w-screen',
    closable: false,
  };

  // instance options object
  const instanceOptions = {
    id: 'authentication-modal',
    override: true
  };

  modal.value = new Modal($targetEl, options, instanceOptions)

}
const logged = ref<boolean>(true);

const login = () => {
  if (form.value.username == 'dayyan syauqi' && form.value.password == 'password') {
    modal.value?.hide();
    localStorage.setItem('logged', 'true');
    logged.value = true;
  } else {
    message.value = "! Username is 'dayyan syauqi' & password is 'password'"
  }
}

const logout = () => {
  localStorage.clear();
  modal.value?.show();
  logged.value = false;
}
onMounted(() => {
  initModal();
  const loggedin = localStorage.getItem('logged');
  if (!loggedin) {
    logged.value = false;
    setTimeout(() => {
      modal.value?.show();
    }, 100);
  }
})
</script>

<template>
  <nav class="border-gray-100 bg-gray-500/30 backdrop:blur-md">
    <div class="flex flex-wrap items-center justify-between w-full p-4 mx-auto">
      <a href="https://flowbite.com/" class="flex items-center space-x-3 rtl:space-x-reverse">
        <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">Dayyan Syauqi</span>
      </a>
      <button data-collapse-toggle="navbar-default" type="button"
        class="inline-flex items-center justify-center w-10 h-10 p-2 text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
        aria-controls="navbar-default" aria-expanded="false">
        <span class="sr-only">Open main menu</span>
        <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M1 1h15M1 7h15M1 13h15" />
        </svg>
      </button>
      <div class="hidden w-full md:block md:w-auto" id="navbar-default">
        <ul
          class="flex flex-col p-4 mt-4 font-medium border border-gray-100 rounded-lg md:p-0 bg-gray-50/30 md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-transparent">
          <li>
            <p class="block px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              aria-current="page">10223055</p>
          </li>
          <li>
            <p
              class="block px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">
              IM23A</p>
          </li>
          <li v-if="logged">
            <button @click="logout"
              class="block px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">
              <span class="block md:hidden">
                Logout
              </span>
              <svg class="hidden w-6 h-6 text-red-800 dark:text-white md:block" aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M20 12H8m12 0-4 4m4-4-4-4M9 4H7a3 3 0 0 0-3 3v10a3 3 0 0 0 3 3h2" />
              </svg>

            </button>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <!-- Modal toggle -->
  <button data-modal-target="authentication-modal" data-modal-toggle="authentication-modal"
    class="text-white bg-blue-700 hover:bg-blue-800 hidden focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
    type="button">
    Toggle modal
  </button>
  <div id="authentication-modal" tabindex="-1" aria-hidden="true"
    class="hidden overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
    <div class="relative w-full max-w-md max-h-full p-4">
      <!-- Modal content -->
      <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
        <!-- Modal header -->
        <div class="flex items-center justify-between p-4 border-b rounded-t md:p-5 dark:border-gray-600">
          <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
            Sign in to our platform
          </h3>
        </div>
        <!-- Modal body -->
        <div class="p-4 md:p-5">
          <div class="space-y-4">
            <div>
              <label for="username" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                username</label>
              <input type="text" name="username" id="username" v-model="form.username" @keyup.enter="login"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                placeholder="dayan syauqi" required />
            </div>
            <div>
              <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                password</label>
              <input type="password" name="password" id="password" placeholder="password" v-model="form.password"
                @keyup.enter="login"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                required />
            </div>
            <p class="text-sm text-red-500">{{ message }}</p>
            <button type="button" @click="login"
              class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Login
              to your account</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <main class="min-h-screen px-16 py-12">
    <h1 class="my-4 text-3xl font-bold text-center">Organisasi & Arsitektur Komputer</h1>
    <div id="accordion-collapse" data-accordion="collapse">
      <h2 id="accordion-collapse-heading-1">
        <button type="button"
          class="flex items-center justify-between w-full gap-3 p-5 font-medium text-gray-500 border border-b-0 border-gray-200 rtl:text-right rounded-t-xl focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
          data-accordion-target="#accordion-collapse-body-1" aria-expanded="true"
          aria-controls="accordion-collapse-body-1">
          <span>Apa yang dimaksud dengan arbitration dalam konteks sistem bus?</span>
          <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M9 5 5 1 1 5" />
          </svg>
        </button>
      </h2>
      <div id="accordion-collapse-body-1" class="hidden" aria-labelledby="accordion-collapse-heading-1">
        <div class="p-5 border border-b-0 border-gray-200 dark:border-gray-700 dark:bg-gray-900">
          <p class="mb-2 text-gray-500 dark:text-gray-400">
            <span
              class="font-medium first-letter:text-7xl first-letter:font-bold first-letter:text-gray-900 dark:first-letter:text-gray-100 first-letter:me-3 first-letter:float-start">
              Dalam konteks sistem bus, arbitration atau arbitrase mengacu pada proses pengaturan akses ke bus oleh
              beberapa perangkat yang ingin berkomunikasi secara bersamaan. Bus adalah jalur komunikasi yang
              menghubungkan
              berbagai komponen komputer, seperti CPU, memori, dan perangkat I/O. Karena hanya satu perangkat yang dapat
              menggunakan bus pada waktu tertentu, diperlukan mekanisme arbitrase untuk menentukan perangkat mana yang
              akan mendapatkan akses dan kapan.
            </span>
            <br>
            <span class="font-medium text-gray-500">
              Ada dua jenis utama metode arbitrase:
            </span>
          <ul class="space-y-1 list-decimal list-insid etext-gray-500 dark:text-gray-400">
            <li>
              <span class="text-lg font-semibold">
                Arbitrase Tersentralisasi
              </span>
              <p class="font-medium text-gray-500 first-letter:ms-4">
                Dikendalikan oleh perangkat khusus yang disebut pengontrol bus atau arbiter.
                Arbiter menentukan perangkat mana yang akan mendapatkan akses berdasarkan aturan yang telah ditentukan,
                seperti:
                Prioritas: Perangkat tertentu memiliki prioritas lebih tinggi dan dilayani terlebih dahulu.
                Round-robin: Setiap perangkat diberi giliran untuk mengakses bus.
                First-come-first-served: Perangkat yang pertama kali meminta akses dilayani terlebih dahulu.
              </p>
            </li>
            <li>
              <span class="text-lg font-semibold">
                Arbitrase Terdistribusi
              </span>
              <p class="font-medium text-gray-500 first-letter:ms-4">
                Tidak ada pengontrol bus pusat.
                Setiap perangkat memiliki logika arbitrase sendiri untuk menentukan kapan akan meminta akses bus.
                Perangkat bernegosiasi satu sama lain untuk menentukan siapa yang akan mendapatkan akses.
                Metode arbitrase yang digunakan dalam sistem bus tertentu tergantung pada berbagai faktor, seperti:
              <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
                <li>
                  Jumlah perangkat yang terhubung ke bus
                </li>
                <li>
                  Jenis perangkat yang terhubung ke bus
                </li>
                <li>
                  Performa yang diinginkan dari sistem bus
                </li>
              </ul>
              <span class="font-medium text-gray-500">
                Berikut beberapa contoh metode arbitrase yang umum digunakan:
              </span>
              <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
                <li>
                  Daisy chain: Perangkat dihubungkan secara berantai, dan sinyal permintaan bus diwariskan dari satu
                  perangkat
                  ke perangkat berikutnya. Perangkat pertama yang memiliki sinyal permintaan yang diakui akan
                  mendapatkan
                  akses bus.
                </li>
                <li>
                  Token passing: Perangkat bergiliran memegang token khusus. Perangkat yang memiliki token diizinkan
                  untuk
                  mengakses bus.
                </li>
                <li>
                  Polling: Pengontrol bus menanyakan setiap perangkat secara berurutan apakah mereka ingin mengakses
                  bus.
                  Perangkat yang pertama kali merespons dengan permintaan akan mendapatkan akses bus.
                </li>
              </ul>
              <span class="font-medium text-gray-500">
                Arbitrase adalah aspek penting dari desain sistem bus karena memastikan bahwa semua perangkat yang
                terhubung
                dapat mengakses bus secara adil dan efisien.
              </span>
              </p>
            </li>
          </ul>
          </p>
        </div>
      </div>
      <h2 id="accordion-collapse-heading-2">
        <button type="button"
          class="flex items-center justify-between w-full gap-3 p-5 font-medium text-gray-500 border border-b-0 border-gray-200 rtl:text-right focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
          data-accordion-target="#accordion-collapse-body-2" aria-expanded="false"
          aria-controls="accordion-collapse-body-2">
          <span>Bagaimana penggunaan buffer dapat meningkatkan efisiensi operasi I/O?</span>
          <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M9 5 5 1 1 5" />
          </svg>
        </button>
      </h2>
      <div id="accordion-collapse-body-2" class="hidden" aria-labelledby="accordion-collapse-heading-2">
        <div class="p-5 border border-b-0 border-gray-200 dark:border-gray-700">
          <p class="mb-2 text-gray-500 dark:text-gray-400">
            <span
              class="font-medium text-gray-500 first-letter:text-7xl first-letter:font-bold first-letter:text-gray-900 dark:first-letter:text-gray-100 first-letter:me-3 first-letter:float-start">
              Buffer adalah area penyimpanan sementara di memori yang digunakan untuk menyimpan data saat sedang
              ditransfer antara perangkat atau antara perangkat dan aplikasi. Penggunaan buffer dapat meningkatkan
              efisiensi operasi input/output (I/O) melalui beberapa cara:
            </span>
          <ul class="space-y-1 list-decimal list-insid etext-gray-500 dark:text-gray-400">
            <li>
              <span class="text-lg font-semibold">
                Mengurangi Ketidakcocokan Kecepatan
              </span>
              <p class="font-medium text-gray-500 first-letter:ms-4">
                Perangkat I/O vs. Prosesor: Perangkat I/O (seperti hard disk atau jaringan) biasanya beroperasi jauh
                lebih
                lambat daripada prosesor. Buffer memungkinkan prosesor untuk melanjutkan tugas lain sementara data
                ditransfer ke atau dari buffer. Setelah transfer selesai, prosesor dapat memproses data dalam buffer
                tanpa
                menunggu perangkat I/O.
                <br>
                Transfer Data Berukuran Kecil: Tanpa buffer, setiap operasi I/O akan memerlukan interaksi langsung
                dengan
                perangkat, yang memakan waktu. Buffer memungkinkan pengumpulan data berukuran kecil menjadi blok yang
                lebih
                besar sebelum ditransfer, mengurangi jumlah interaksi dengan perangkat.

              </p>
            </li>
            <li>
              <span class="text-lg font-semibold">
                Mengatasi Latensi
              </span>
              <p class="font-medium text-gray-500 first-letter:ms-4">
                Akses Disk: Akses ke hard disk melibatkan pergerakan fisik kepala baca/tulis, yang menimbulkan latensi.
                Buffer dapat menyimpan data yang baru dibaca dari disk, sehingga jika data yang sama diminta lagi, dapat
                diakses langsung dari buffer tanpa harus mengakses disk lagi.
                <br>
                Jaringan: Dalam komunikasi jaringan, latensi dapat terjadi karena jarak fisik dan kemacetan. Buffer
                dapat
                menyimpan data yang diterima dari jaringan sementara aplikasi memproses data sebelumnya, mengurangi
                dampak
                latensi pada kinerja aplikasi.
              </p>
            </li>
            <li>
              <span class="text-lg font-semibold">
                Meningkatkan Throughput
              </span>
              <p class="font-medium text-gray-500 first-letter:ms-4">
                Double Buffering (Buffer Ganda): Dengan menggunakan dua buffer, satu buffer dapat digunakan untuk
                menerima
                data masuk sementara buffer lainnya digunakan untuk mengirim data keluar. Ini memungkinkan operasi I/O
                terjadi secara paralel, meningkatkan throughput secara keseluruhan.
                <br>
                Prefetching (Pengambilan Awal): Buffer dapat digunakan untuk membaca data dari disk atau jaringan
                sebelum
                benar-benar diminta oleh aplikasi. Ini dapat mengurangi waktu tunggu ketika aplikasi akhirnya
                membutuhkan
                data tersebut.
              </p>
            </li>
            <li>
              <span class="text-lg font-semibold">
                Menyederhanakan Pemrograman
              </span>
              <p class="font-medium text-gray-500 first-letter:ms-4">
                Abstraksi Perangkat: Buffer menyembunyikan detail perangkat I/O dari aplikasi. Aplikasi dapat membaca
                atau
                menulis data ke buffer tanpa harus khawatir tentang bagaimana data tersebut ditransfer ke atau dari
                perangkat.
              </p>
            </li>
          </ul>
          <span class="font-medium text-gray-500">
            Contoh Penerapan:
          </span>
          <br>
          <span class="font-medium text-gray-500 ">
            Streaming Video: Buffer digunakan untuk menyimpan sebagian video yang diunduh sehingga pemutaran dapat
            dimulai sebelum seluruh video diunduh.
            <br>
            Web Browser: Buffer digunakan untuk menyimpan halaman web yang sedang diunduh sehingga pengguna dapat mulai
            melihat halaman sebelum pengunduhan selesai.
          </span>
          </p>
        </div>
      </div>
      <h2 id="accordion-collapse-heading-3">
        <button type="button"
          class="flex items-center justify-between w-full gap-3 p-5 font-medium text-gray-500 border border-gray-200 rtl:text-right focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
          data-accordion-target="#accordion-collapse-body-3" aria-expanded="false"
          aria-controls="accordion-collapse-body-3">
          <span>Bagaimana cara kerja sebuah ALU (Arithmetic Logic Unit)? Berikan contoh operasi yang
            dapat dilakukan oleh ALU.</span>
          <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M9 5 5 1 1 5" />
          </svg>
        </button>
      </h2>
      <div id="accordion-collapse-body-3" class="hidden" aria-labelledby="accordion-collapse-heading-3">
        <div class="p-5 border border-t-0 border-gray-200 dark:border-gray-700">
          <p class="mb-2 text-gray-500 dark:text-gray-400">
            <span class="font-medium text-gray-500 ">
              Arithmetic Logic Unit (ALU) adalah komponen inti dalam sebuah prosesor yang bertanggung jawab untuk
              melakukan operasi aritmatika (seperti penjumlahan, pengurangan, perkalian, pembagian) dan operasi logika
              (seperti AND, OR, XOR, NOT) pada data biner. Berikut adalah gambaran umum tentang cara kerja ALU:
            </span>
          <ul class="space-y-1 font-medium text-gray-500 list-decimal list-inside dark:text-gray-400">
            <li>
              Input: ALU menerima dua input data biner, biasanya disebut operand A dan operand B. Operand ini bisa
              berasal dari register prosesor atau langsung dari memori.

            </li>
            <li>
              Instruksi: ALU juga menerima instruksi dari unit kontrol prosesor yang menentukan operasi apa yang harus
              dilakukan pada operand. Instruksi ini biasanya berupa kode biner yang disebut opcode.

            </li>
            <li>
              Operasi: Berdasarkan opcode yang diterima, ALU melakukan operasi yang sesuai pada operand A dan B.
              Operasi ini dilakukan oleh rangkaian logika digital yang terdiri dari gerbang logika seperti AND, OR, XOR,
              dan NOT.

            </li>
            <li>
              Output: Hasil dari operasi disimpan dalam register output ALU. Hasil ini kemudian dapat digunakan oleh
              instruksi selanjutnya atau disimpan kembali ke memori.

            </li>
          </ul>
          <span class="font-medium text-gray-500 ">
            Contoh Operasi yang Dapat Dilakukan oleh ALU:
          </span>
          <ul class="space-y-1 font-medium text-gray-500 list-decimal list-inside dark:text-gray-400">
            <li>
              Operasi Aritmatika:
              <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
                <li>
                  Penjumlahan: Menambahkan nilai operand A dan B.
                </li>
                <li>
                  Pengurangan: Mengurangi nilai operand B dari operand A.
                </li>
                <li>
                  Perkalian: Mengalikan nilai operand A dan B.
                </li>
                <li>
                  Pembagian: Membagi nilai operand A dengan operand B.
                </li>
                <li>
                  Increment: Menambah nilai operand A dengan satu.
                </li>
                <li>
                  Decrement: Mengurangi nilai operand A dengan satu.
                </li>
              </ul>
            </li>
            <li>
              Operasi Logika:
              <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
                <li>
                  AND: Menghasilkan 1 jika kedua bit pada posisi yang sama dari operand A dan B adalah 1, jika tidak
                  menghasilkan 0.
                </li>
                <li>
                  OR: Menghasilkan 1 jika setidaknya satu bit pada posisi yang sama dari operand A dan B adalah 1, jika
                  tidak
                  menghasilkan 0.
                </li>
                <li>
                  XOR: Menghasilkan 1 jika hanya satu bit pada posisi yang sama dari operand A dan B adalah 1, jika
                  tidak
                  menghasilkan 0.
                </li>
                <li>
                  NOT: Membalik nilai setiap bit dalam operand A (0 menjadi 1, 1 menjadi 0).
                </li>
              </ul>
            </li>
            <li>
              Operasi Lainnya:
              <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
                <li>
                  Pergeseran Bit (Shift): Menggeser bit-bit dalam operand ke kiri atau ke kanan.
                </li>
                <li>
                  Perbandingan: Membandingkan nilai operand A dan B (misalnya, apakah A lebih besar, lebih kecil, atau
                  sama
                  dengan B).
                </li>
              </ul>
            </li>
          </ul>
          </p>
        </div>
      </div>
      <h2 id="accordion-collapse-heading-4">
        <button type="button"
          class="flex items-center justify-between w-full gap-3 p-5 font-medium text-gray-500 border border-gray-200 rtl:text-right focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
          data-accordion-target="#accordion-collapse-body-4" aria-expanded="false"
          aria-controls="accordion-collapse-body-4">
          <span>Bagaimana operasi bit-level (bit-level operations) diimplementasikan dalam sebuah
            CPU?Bagaimana set instruksi mempengaruhi kinerja sebuah CPU? Berikan contoh.</span>
          <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M9 5 5 1 1 5" />
          </svg>
        </button>
      </h2>
      <div id="accordion-collapse-body-4" class="hidden" aria-labelledby="accordion-collapse-heading-4">
        <div class="p-5 border border-t-0 border-gray-200 dark:border-gray-700">
          <span class="font-medium text-gray-500 ">
            Operasi Bit-Level dalam CPU:
          </span>
          <p class="font-medium text-gray-500">
            Operasi bit-level, seperti AND, OR, XOR, NOT, dan pergeseran bit (shift), diimplementasikan dalam CPU
            menggunakan gerbang logika (logic gates). Gerbang logika adalah rangkaian elektronik dasar yang melakukan
            operasi Boolean pada satu atau lebih input biner (0 atau 1) dan menghasilkan satu output biner.
          </p>
          <span class="font-medium text-gray-500 ">
            Berikut adalah contoh bagaimana operasi bit-level AND diimplementasikan menggunakan gerbang logika AND:
          </span>
          <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
            <li>
              Input: Dua bit, A dan B.
            </li>
            <li>
              Gerbang Logika: Gerbang AND.
            </li>
            <li>
              Output: Satu bit, Y.
            </li>
            <li>
              Tabel Kebenaran:
              <table>
                <thead>
                  <tr>
                    <td>A</td>
                    <td>B</td>
                    <td>Y</td>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>0</td>
                    <td>0</td>
                    <td>0</td>
                  </tr>
                  <tr>
                    <td>0</td>
                    <td>1</td>
                    <td>0</td>
                  </tr>
                  <tr>
                    <td>1</td>
                    <td>0</td>
                    <td>0</td>
                  </tr>
                  <tr>
                    <td>1</td>
                    <td>1</td>
                    <td>1</td>
                  </tr>
                </tbody>
              </table>
            </li>
          </ul>
          <p class="font-medium text-gray-500">
            Dalam CPU, gerbang logika ini dihubungkan dalam rangkaian yang lebih kompleks untuk membentuk unit
            aritmatika dan logika (ALU). ALU adalah komponen yang bertanggung jawab untuk melakukan semua operasi
            aritmatika dan logika dalam CPU.
          </p>
          <span class="font-medium text-gray-500">
            Pengaruh Set Instruksi pada Kinerja CPU:
          </span>

          <p class="font-medium text-gray-500">
            Set instruksi (instruction set) adalah kumpulan instruksi yang dapat dieksekusi oleh CPU. Setiap instruksi
            menentukan operasi tertentu yang harus dilakukan oleh CPU, seperti membaca data dari memori, menulis data ke
            memori, melakukan operasi aritmatika atau logika, atau melompat ke instruksi lain.
          </p>
          <span class="font-medium text-gray-500">
            Set instruksi memiliki pengaruh besar pada kinerja CPU karena beberapa alasan:
          </span>
          <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
            <li>
              Kompleksitas Instruksi: Instruksi yang lebih kompleks membutuhkan lebih banyak siklus clock untuk
              dieksekusi, yang dapat memperlambat CPU.
            </li>
            <li>
              Jumlah Instruksi: Semakin banyak instruksi yang diperlukan untuk menyelesaikan tugas tertentu, semakin
              lama
              waktu yang dibutuhkan CPU.
            </li>
            <li>
              Efisiensi Instruksi: Beberapa instruksi mungkin lebih efisien daripada yang lain dalam hal jumlah siklus
              clock yang diperlukan atau jumlah data yang dapat diproses.
            </li>
          </ul>
          <span class="font-medium text-gray-500">Contoh:</span>
          <p class="font-medium text-gray-500">
            Misalkan kita memiliki dua CPU yang berbeda, CPU A dan CPU B. CPU A memiliki set instruksi yang lebih
            kompleks daripada CPU B, tetapi CPU A juga memiliki instruksi yang lebih efisien untuk tugas-tugas tertentu.
          </p>
          <p class="font-medium text-gray-500">
            Dalam skenario ini, CPU A mungkin berkinerja lebih baik daripada CPU B untuk tugas-tugas yang dapat
            memanfaatkan instruksi efisien CPU A. Namun, untuk tugas-tugas lain, CPU B mungkin berkinerja lebih baik
            karena set instruksinya yang lebih sederhana.
          </p>
        </div>
      </div>
      <h2 id="accordion-collapse-heading-5">
        <button type="button"
          class="flex items-center justify-between w-full gap-3 p-5 font-medium text-gray-500 border border-gray-200 rtl:text-right focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-800 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800"
          data-accordion-target="#accordion-collapse-body-5" aria-expanded="false"
          aria-controls="accordion-collapse-body-5">
          <span>Bagaimana sebuah CPU memproses instruksi yang kompleks dalam set instruksi?</span>
          <svg data-accordion-icon class="w-3 h-3 rotate-180 shrink-0" aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M9 5 5 1 1 5" />
          </svg>
        </button>
      </h2>
      <div id="accordion-collapse-body-5" class="hidden" aria-labelledby="accordion-collapse-heading-4">
        <div class="p-5 border border-t-0 border-gray-200 dark:border-gray-700">
          <span class="font-medium text-gray-500">
            CPU memproses instruksi kompleks dalam set instruksi melalui kombinasi beberapa mekanisme:
          </span>
          <ul class="space-y-1 font-medium text-gray-500 list-decimal list-inside dark:text-gray-400">
            <li>
              <span class="font-medium text-gray-500">
                Dekomposisi Instruksi Kompleks:
              </span>
              <p class="font-medium text-gray-500">
                Instruksi kompleks sering kali dipecah menjadi serangkaian instruksi yang lebih sederhana dan mendasar.
                Misalnya, instruksi perkalian floating-point dapat dipecah menjadi beberapa instruksi penjumlahan,
                pengurangan, dan pergeseran bit.
              </p>
            </li>
            <li>
              <span class="font-medium text-gray-500">
                Microcode:
              </span>
              <p class="font-medium text-gray-500">
                Beberapa CPU menggunakan microcode, yaitu lapisan instruksi yang lebih rendah dan tersembunyi. Instruksi
                kompleks diterjemahkan menjadi serangkaian instruksi microcode yang lebih sederhana, yang kemudian
                dieksekusi oleh CPU.
              </p>
            </li>
            <li>
              <span class="font-medium text-gray-500">
                Pipeline (Saluran Instruksi):
              </span>
              <p class="font-medium text-gray-500">
                CPU modern menggunakan pipeline untuk mengeksekusi beberapa instruksi secara bersamaan. Setiap tahap
                dalam
                pipeline bertanggung jawab untuk bagian tertentu dari proses eksekusi instruksi (misalnya, pengambilan
                instruksi, dekode, eksekusi, penulisan kembali). Dengan membagi eksekusi instruksi menjadi beberapa
                tahap,
                CPU dapat meningkatkan throughput secara signifikan.
              </p>
            </li>
            <li>
              <span class="font-medium text-gray-500">
                Unit Eksekusi Khusus:
              </span>
              <p class="font-medium text-gray-500">
                Beberapa CPU memiliki unit eksekusi khusus untuk jenis instruksi tertentu, seperti instruksi
                floating-point
                atau instruksi SIMD (Single Instruction Multiple Data). Unit eksekusi ini dioptimalkan untuk jenis
                instruksi
                tertentu dan dapat mengeksekusinya lebih cepat daripada unit eksekusi umum.
              </p>
            </li>
            <li>
              <span class="font-medium text-gray-500">
                Prediksi Cabang (Branch Prediction):
              </span>
              <p class="font-medium text-gray-500">
                Instruksi percabangan (misalnya, instruksi "if") dapat mengganggu aliran eksekusi instruksi. CPU modern
                menggunakan prediksi cabang untuk menebak hasil dari instruksi percabangan dan mulai mengeksekusi
                instruksi
                berikutnya sebelum hasil percabangan diketahui. Jika prediksi salah, CPU harus membatalkan instruksi
                yang
                telah dieksekusi dan memulai kembali dari instruksi yang benar.
              </p>
            </li>
            <li>
              <span class="font-medium text-gray-500">
                Cache Instruksi:
              </span>
              <p class="font-medium text-gray-500">
                Cache instruksi adalah memori kecil dan cepat yang menyimpan salinan instruksi yang sering digunakan.
                Dengan
                menyimpan instruksi dalam cache, CPU dapat mengaksesnya lebih cepat daripada harus mengambilnya dari
                memori
                utama.
              </p>
            </li>
          </ul>
          <span class="font-medium text-gray-500">
            Contoh:
          </span>
          <p class="font-medium text-gray-500">
            Misalkan kita memiliki instruksi kompleks untuk menghitung akar kuadrat dari sebuah bilangan floating-point.
            Instruksi ini dapat dipecah menjadi serangkaian instruksi yang lebih sederhana:
          </p>
          <ul class="space-y-1 font-medium text-gray-500 list-disc list-inside dark:text-gray-400">
            <li>
              Memuat bilangan floating-point ke dalam register.
            </li>
            <li>
              Memanggil fungsi perpustakaan matematika untuk menghitung akar kuadrat.
            </li>
            <li>
              Menyimpan hasil kembali ke memori.
            </li>
            <li>
              Setiap instruksi yang lebih sederhana ini kemudian dapat dieksekusi oleh CPU menggunakan mekanisme yang
              dijelaskan di atas.
            </li>
          </ul>
          <p class="font-medium text-gray-500">
            Dengan menggabungkan mekanisme ini, CPU dapat mengeksekusi instruksi kompleks dengan efisien dan
            meningkatkan kinerja secara keseluruhan.
          </p>
        </div>
      </div>
    </div>
  </main>
  <footer class="m-4 bg-white rounded-lg shadow dark:bg-gray-900">
    <div class="w-full p-4 mx-auto md:py-8">
      <div class="sm:flex sm:items-center sm:justify-between">
        <a href="https://flowbite.com/" class="flex items-center mb-4 space-x-3 sm:mb-0 rtl:space-x-reverse">
          <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">Dayan Syauqi</span>
        </a>
        <ul class="flex flex-wrap items-center mb-6 text-sm font-medium text-gray-500 sm:mb-0 dark:text-gray-400">
          <li>
            <a href="#" class="hover:underline me-4 md:me-6">102230055</a>
          </li>
          <li>
            <a href="#" class="hover:underline me-4 md:me-6">IM23A</a>
          </li>
        </ul>
      </div>
      <hr class="my-6 border-gray-200 sm:mx-auto dark:border-gray-700 lg:my-8" />
      <span class="block text-sm text-gray-500 sm:text-center dark:text-gray-400">© 2023 <a href="https://flowbite.com/"
          class="hover:underline">Iamdayy™</a>. All Rights Reserved.</span>
    </div>
  </footer>
</template>

<style scoped></style>
