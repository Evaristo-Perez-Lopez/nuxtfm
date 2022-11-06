<script>
import { defineNuxtComponent } from "#app";
export default defineNuxtComponent({
  data: () => ({
    photoGallery: [],
  }),
  methods: {
    fetchPhotoGallery() {
      fetch("https://jsonplaceholder.typicode.com/photos")
        .then((response) => response.json())
        .then((json) => (this.photoGallery = json));
    },
  },
  computed: {
    numberOfPhotos() {
      return this.photoGallery.length;
    },
    evenPhotos() {
      return this.photoGallery.filter((item) => item.id % 2 === 0).length;
    },
    displayContent() {
      return this.photoGallery.length > 0;
    },
  },
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
