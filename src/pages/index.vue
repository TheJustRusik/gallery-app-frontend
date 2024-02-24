<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <div>Welcome to</div>
      <h1>Gallery</h1>
      <div>
        <img v-for="url in data" :src="'http://localhost:8080/' + url" alt="">
      </div>
      <v-btn
        color="pink"
        dark
        absolute
        bottom
        right
        fab
      >
        Admin
      </v-btn>
    </v-responsive>
    
  </v-container>
  
</template>

<script setup>
  import {ref} from 'vue'
  import axios from 'axios';

  let data = ref([])

  async function load_galery(){
    const response = await axios.get('http://localhost:8080/api/content_images');
    data.value = response.data
  }
  load_galery()
  
    
</script>
