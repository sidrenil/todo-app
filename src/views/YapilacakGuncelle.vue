<template>
  <h1>Yapilacak Guncelle {{ route.params.id }}</h1>
  <form @submit.prevent="handleSubmit">
    <label>Başlık:</label>
    <input type="text" v-model="baslik" />

    <label>İçerik:</label>
    <input type="text" v-model="icerik" />

    <button>Güncelle</button>
  </form>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();
const baslik = ref("");
const icerik = ref("");
const uri = `http://localhost:3000/yapilacaklar/${route.params.id}`;

onMounted(() => {
  fetch(uri)
    .then((res) => {
      if (!res.ok) {
        throw new Error(`HTTP error! Status: ${res.status}`);
      }
      return res.json();
    })
    .then((data) => {
      baslik.value = data.baslik;
      icerik.value = data.icerik;
    })
    .catch((err) => console.error("Error fetching data:", err));
});

const handleSubmit = () => {
  fetch(uri, {
    method: "PATCH",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ baslik: baslik.value, icerik: icerik.value }),
  })
    .then((res) => {
      if (!res.ok) {
        throw new Error(`HTTP error! Status: ${res.status}`);
      }
      router.push("/");
    })
    .catch((err) => console.error("Error updating data:", err));
};
</script>

<style></style>
