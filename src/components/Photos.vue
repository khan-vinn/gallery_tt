<template>
  <div class="photos" v-if="photos?.length>0">
    <div v-for="photo  in photos" :key="photo">
      <div @click="addToFavourite(photo)"> {{ photo.user.id }}</div>
      <img :src=photo.urls.small :alt=photo.user.name @click="select(photo)">
    </div>
  </div>
  <div v-else>
    No photos
  </div>
</template>

<script>
export default {
  name: "PhotosComponent",
  props:{
    photos: Array,
    addToFavourite: Function,
    select: Function
  }
}
</script>

<style scoped>

</style>
