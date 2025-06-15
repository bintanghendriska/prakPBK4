<template>
  <div class="kartu-formulir">
    <h3>Informasi Alamat</h3>
    <div class="grup-input">
      <label for="jalan">Jalan:</label>
      <input type="text" id="jalan" v-model="jalan" @input="validasiInput" :class="{ 'input-error': !validJalan && jalan !== '' }">
      <p v-if="!validJalan && jalan !== ''" class="pesan-error">Jalan tidak boleh kosong.</p>
    </div>
    <div class="grup-input">
      <label for="kota">Kota:</label>
      <input type="text" id="kota" v-model="kota" @input="validasiInput" :class="{ 'input-error': !validKota && kota !== '' }">
      <p v-if="!validKota && kota !== ''" class="pesan-error">Kota tidak boleh kosong.</p>
    </div>
    <div class="grup-input">
      <label for="kode-pos">Kode Pos:</label>
      <input type="text" id="kode-pos" v-model="kodePos" @input="validasiInput" :class="{ 'input-error': !validKodePos && kodePos !== '' }">
      <p v-if="!validKodePos && kodePos !== ''" class="pesan-error">Kode Pos harus 5 digit angka.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'KomponenAlamat',
  data() {
    return {
      jalan: '',
      kota: '',
      kodePos: '',
      validJalan: false,
      validKota: false,
      validKodePos: false
    };
  },
  watch: {
    jalan() {
      this.validasiInput();
    },
    kota() {
      this.validasiInput();
    },
    kodePos() {
      this.validasiInput();
    }
  },
  methods: {
    validasiInput() {
      this.validJalan = this.jalan.trim() !== '';
      this.validKota = this.kota.trim() !== '';

      const kodePosRegex = /^\d{5}$/;
      this.validKodePos = kodePosRegex.test(this.kodePos);

      this.$emit('data-alamat-update', {
        jalan: this.jalan,
        kota: this.kota,
        kodePos: this.kodePos,
        isValid: this.validJalan && this.validKota && this.validKodePos
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

input[type="text"] {
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