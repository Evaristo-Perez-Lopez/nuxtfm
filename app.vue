<script setup>
import { ref, computed } from "vue";

let photoGallery = ref([]);
function fetchPhotoGallery() {
  fetch("https://jsonplaceholder.typicode.com/photos")
    .then((response) => response.json())
    .then((json) => (photoGallery.value = json));
}
const numberOfPhotos = computed(() => photoGallery.value.length);
const evenPhotos = computed(
  () => photoGallery.value.filter((item) => item.id % 2 === 0).length
);
const displayContent = computed(() => {
  return photoGallery.value.length > 0;
});
</script>
<template>
  <div>
    <h1>Photo Gallery</h1>
    <button @click="fetchPhotoGallery">Obtener los datos</button>
    <ul v-if="displayContent">
      <p>Even Photos: {{ evenPhotos }}</p>
      <p>Photos in this collection: {{ numberOfPhotos }}</p>
      <li v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
        <img :src="photo.thumbnailUrl" alt="" />
      </li>
    </ul>
  </div>
</template>
