<template>
  <div class="control">
    <input type="text" class="search" v-model="searchInput">
    <button @click="searchPhotos()">Search</button>
  </div>
  <div class="content">
    <div class="photos">
      <div v-for="photo  in this.randomPhotos" :key="photo">
       <div @click="addToFavourites(photo)"> {{photo.user.id}} </div>
        <img :src=photo.urls.small>
      </div>
    </div>
  </div>
</template>

<script>
import {createApi} from "unsplash-js";
import config from "../config";

export default {
  name: 'App',
  data(){
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
    this.unsplash.photos.getRandom({count:8}).then(data=> {
      this.randomPhotos = data.response
    }).catch(e=> {
      console.log(e)
    })
  },
  methods:{
    addToFavourites(item){
      try{
        this.favourite_photos.push(item)
        console.log(this.favourite_photos)
        return true
      }catch (e) {
        console.log(e)
        return false
      }
    },
    searchPhotos(){
      this.unsplash.search.getPhotos({
        query:this.searchInput || "",
        perPage: 8
      }).then(data=> {
        this.randomPhotos = data.response
      }).catch(e=> {
        console.log(e)
      })
    }
  }
}
</script>

<style>

</style>
