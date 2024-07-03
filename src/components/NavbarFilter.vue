<template>
  <nav class="filter-nav">
    <button @click="filterGuncelle('hepsi')" :class="{active:aktifSekme==='hepsi'}">Bütün Yapilacaklar</button>
    <button @click="filterGuncelle('tamamlandi')" :class="{active:aktifSekme==='tamamlandi'}">Tamamlanan Yapilacaklar</button>
    <button @click="filterGuncelle('yapiliyor')" :class="{active:aktifSekme==='yapiliyor'}">Devam Eden Yapilacaklar</button>
  </nav>
</template>




<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps(['aktifSekme'])
const emit = defineEmits(['filterDurum'])

const filterGuncelle = (durum) => {
    emit('filterDurum', durum)
}

</script>














<style>
.filter-nav button {
    @apply bg-inherit rounded-none text-stone-400 outline-0 text-xs uppercase mr-10 tracking-widest font-bold cursor-pointer
}
.filter-nav button.active {
    @apply text-red-600
}

</style>