<template>
  <div class="control">
    <input type="text" class="search" v-model="searchInput">
    <button @click="searchPhotos()">Search</button>
  </div>
  <div class="content">
    <div class="photos" v-if="randomPhotos?.length>0">
      <div v-for="photo  in randomPhotos" :key="photo">
        <div @click="addToFavourite(photo)"> {{ photo.user.id }}</div>
        <img :src=photo.urls.small :alt=photo.user.name>
      </div>
    </div>
  </div>
</template>

<script>
import {createApi} from "unsplash-js";
import config from "../config";

export default {
  name: 'App',
  data() {
    return {
      randomPhotos: [],
      favourite_photos: [],
      searchInput: "cat"
    }
  },
  mounted() {
    this.unsplash = createApi({
      accessKey: config.UNSPLASH_ACCESS_KEY
    })
    this.unsplash.photos.getRandom({count: 8}).then(data => {
      this.randomPhotos = data.response
    }).catch(e => {
      console.log(e)
    })
  },
  methods: {
    addToFavourite(item) {
      console.log(item)
      this.favourite_photos.push(item)
      console.log(this.favourite_photos)
    },
    searchPhotos() {
      this.unsplash.search.getPhotos({
        query: this.searchInput || "",
        perPage: 8
      })
          .then(data => {
            console.log(data)
            this.randomPhotos = data.response.results
          })
          .catch(e => {
            console.log(e)
          })
    }
  }
}
</script>

<style>

</style>
