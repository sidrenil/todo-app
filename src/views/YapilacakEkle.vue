<template>
  <form @submit.prevent="yapilacakEkle">
    <label>Başlik:</label>
    <input v-model="baslik" type="text" required />
    <br />
    <br />
    <label>İcerik:</label>
    <input v-model="icerik" type="text" required />
    <br />
    <button>Ekle</button>
  </form>
</template>
<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const baslik = ref("");
const icerik = ref("");
const router = useRouter();

function yapilacakEkle() {
  let yapilacak = {
    id: Math.floor(Math.random() * 100000),
    baslik: baslik.value,
    icerik: icerik.value,
    yapildi: false,
  };
  fetch("http://localhost:3000/yapilacaklar", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(yapilacak),
  });
  router.push("/");
}
</script>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  max-width: 400px;
  margin: 0 auto;
}

.form-box {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 12px;
  margin-bottom: 15px;
}

.form-label {
  display: block;
  color: #4a5568;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
  margin-bottom: 5px;
}

.form-input {
  padding: 10px;
  border: 2px solid #718096;
  width: 100%;
  box-sizing: border-box;
  border-radius: 6px;
  margin-bottom: 15px;
  font-size: 14px;
}

.form-button {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #48bb78;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s ease;
}

.form-button:hover {
  background-color: #38a169;
}
</style>
