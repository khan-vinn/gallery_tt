<template>
  <div class="photos" v-if="photos?.length>0">
    <div v-for="photo  in photos" :key="photo">
      <img :src=photo.urls.small :alt=photo.user.name @click="select(photo)" class="picture">
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
    select: Function
  }
}
</script>

<style scoped>

</style>
