<template>
  <form @submit.prevent="yapilacakEkle">
    <label>Başlik:</label>
    <input v-model="baslik" type="text" required />

    <label>İcerik:</label>
    <input v-model="icerik" type="text" required />

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
  // console.log(this.baslik, this.icerik);
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

<style>
form {
  @apply bg-white p-20 rounded-xl;
}
label {
  @apply block text-slate-200 uppercase text-sm font-bold;
}
input {
  @apply p-10 border-0 border-2 border-solid border-slate-950 w-full box-border;
}
textarea {
  @apply border-2 border-solid border-zinc-950 p-10 w-full box-border h-full;
}
form button {
  @apply block m-20 mx-auto mt-10 bg-green-600 text-white p-10 border-0 rounded-md text-base;
}
</style>
