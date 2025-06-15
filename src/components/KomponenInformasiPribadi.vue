<template>
  <div class="kartu-formulir">
    <h3>Informasi Pribadi</h3>
    <div class="grup-input">
      <label for="nama">Nama Lengkap:</label>
      <input type="text" id="nama" v-model="nama" @input="validasiInput" :class="{ 'input-error': !validNama && nama !== '' }">
      <p v-if="!validNama && nama !== ''" class="pesan-error">Nama tidak boleh kosong.</p>
    </div>
    <div class="grup-input">
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="email" @input="validasiInput" :class="{ 'input-error': !validEmail && email !== '' }">
      <p v-if="!validEmail && email !== ''" class="pesan-error">Email harus valid.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'KomponenInformasiPribadi',
  data() {
    return {
      nama: '',
      email: '',
      validNama: false,
      validEmail: false
    };
  },
  watch: {
    nama() {
      this.validasiInput();
    },
    email() {
      this.validasiInput();
    }
  },
  methods: {
    validasiInput() {
      this.validNama = this.nama.trim() !== '';

      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      this.validEmail = emailRegex.test(this.email);

      this.$emit('data-personal-update', {
        nama: this.nama,
        email: this.email,
        isValid: this.validNama && this.validEmail
      });
    }
  },
  mounted() {
    this.validasiInput();
  }
}
</script>

<style scoped>
.kartu-formulir {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  background-color: #f9f9f9;
}

h3 {
  color: #333;
  margin-top: 0;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

.grup-input {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #555;
}

input[type="text"],
input[type="email"] {
  width: calc(100% - 22px);
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1em;
}

input.input-error {
  border-color: #e74c3c;
  box-shadow: 0 0 0 0.2rem rgba(231, 76, 60, 0.25);
}

.pesan-error {
  color: #e74c3c;
  font-size: 0.85em;
  margin-top: 5px;
}
</style>