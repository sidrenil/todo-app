<template>
  <div class="home">
    <NavbarFilter @filterDurum="aktifSekme = $event" :aktifSekme="aktifSekme" />
    <div v-if="yapilacaklar.length">
      <div v-for="yap in filtrelenmisYapilacaklar" :key="yap.id">
        <Yapilacak :yapilacak="yap" @sil="silHandle" @yapildi="yapildiHandle" />
      </div>
    </div>
    <div v-else>
      <p>Yapilacaklar yukleniyor</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import Yapilacak from "../components/Yapilacak.vue";
import NavbarFilter from "../components/NavbarFilter.vue";

const yapilacaklar = ref([]);
const aktifSekme = ref("hepsi");

const fetchData = async () => {
  try {
    const response = await fetch("http://localhost:3000/yapilacaklar");
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    yapilacaklar.value = data;
  } catch (err) {
    console.error("Error fetching data:", err);
  }
};

const silHandle = (id) => {
  yapilacaklar.value = yapilacaklar.value.filter((yap) => yap.id !== id);
};

const yapildiHandle = (id) => {
  const yap = yapilacaklar.value.find((yapilacak) => yapilacak.id === id);
  yap.yapildi = !yap.yapildi;
};

const filtrelenmisYapilacaklar = computed(() => {
  if (aktifSekme.value === "tamamlandi") {
    return yapilacaklar.value.filter((yapilacak) => yapilacak.yapildi);
  }
  if (aktifSekme.value === "yapiliyor") {
    return yapilacaklar.value.filter((yapilacak) => !yapilacak.yapildi);
  }
  return yapilacaklar.value;
});

fetchData();
</script>
