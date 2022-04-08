<template>
  <div>
    <img :src="photo.urls.small" :alt="photo.user.id" @click="addToFavourite(photo)"/>
    <div>
      <p> {{ photo.user.name }}</p>
      <img :src="photo.user.profile_image.small" :alt="photo.user.portfolio_url" >
    </div>
  </div>
</template>

<script>
export default {
  name: "PhotoComponent",
  props: {
    photo: Object,
    addToFavourite: Function
  }
}
</script>

<style scoped>

</style>
