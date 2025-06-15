<template>
  <div class="kontainer-formulir">
    <h2>Formulir Pendaftaran</h2>

    <form @submit.prevent="kirimFormulir">
      <KomponenInformasiPribadi @data-personal-update="updateDataPersonal" />
      <KomponenAlamat @data-alamat-update="updateDataAlamat" />

      <button type="submit" :disabled="!isFormulirValid" class="tombol-kirim">
        Kirim Formulir
      </button>

      <div v-if="pesanSukses" class="pesan-sukses">
        {{ pesanSukses }}
        <pre>{{ JSON.stringify(dataFormulirLengkap, null, 2) }}</pre>
      </div>
      <div v-if="pesanError" class="pesan-error-umum">
        {{ pesanError }}
      </div>
    </form>
  </div>
</template>

<script>
import KomponenInformasiPribadi from './KomponenInformasiPribadi.vue';
import KomponenAlamat from './KomponenAlamat.vue';

export default {
  name: 'KomponenInduk',
  components: {
    KomponenInformasiPribadi,
    KomponenAlamat
  },
  data() {
    return {
      dataPersonal: {
        nama: '',
        email: '',
        isValid: false
      },
      dataAlamat: {
        jalan: '',
        kota: '',
        kodePos: '',
        isValid: false
      },
      pesanSukses: '',
      pesanError: ''
    };
  },
  computed: {
    isFormulirValid() {
      return this.dataPersonal.isValid && this.dataAlamat.isValid;
    },
    dataFormulirLengkap() {
      return {
        ...this.dataPersonal,
        ...this.dataAlamat
      };
    }
  },
  methods: {
    updateDataPersonal(data) {
      this.dataPersonal = data;
      this.resetPesan();
    },
    updateDataAlamat(data) {
      this.dataAlamat = data;
      this.resetPesan();
    },
    kirimFormulir() {
      this.resetPesan();
      if (this.isFormulirValid) {
        console.log('Formulir Valid, data dikirim:', this.dataFormulirLengkap);
        this.pesanSukses = 'Formulir berhasil dikirim!';
      } else {
        this.pesanError = 'Mohon lengkapi semua bidang formulir dengan benar.';
        console.log('Formulir tidak valid.');
      }
    },
    resetPesan() {
      this.pesanSukses = '';
      this.pesanError = '';
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f7f6;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
  margin: 0;
  padding: 30px 0;
}

.kontainer-formulir {
  background-color: #fff;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 600px;
}

h2 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 30px;
}

.tombol-kirim {
  display: block;
  width: 100%;
  padding: 12px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 1.1em;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.tombol-kirim:hover:not(:disabled) {
  background-color: #45a049;
}

.tombol-kirim:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.pesan-sukses {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
  border-radius: 5px;
  padding: 15px;
  margin-top: 20px;
  font-weight: bold;
}

.pesan-sukses pre {
  background-color: #e9ecef;
  padding: 10px;
  border-radius: 5px;
  margin-top: 10px;
  overflow-x: auto;
  font-size: 0.9em;
  color: #333;
}

.pesan-error-umum {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
  border-radius: 5px;
  padding: 15px;
  margin-top: 20px;
  font-weight: bold;
}
</style>