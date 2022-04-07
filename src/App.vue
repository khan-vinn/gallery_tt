<template>
  <div class="content">
    <div class="photos">
      <div v-for="photo  in this.randomPhotos" :key="photo">
       <div> {{photo.user.id}} </div>
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
      searchInput: ""
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
