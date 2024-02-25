<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <div>Welcome to</div>
      <h1>Gallery</h1>
      <div>
        <img v-for="url in data" :src="'http://localhost:8080/images' + url" alt="">
      </div>
      <h2>Uppload your image!</h2>
      <div style="padding-bottom: 45px;">
        <v-file-input v-model="file" clearable label="File input" variant="underlined"></v-file-input>
        <v-btn @click="uploadFile">Upload</v-btn>
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
  let file = ref()

  function uploadFile(){
    const formData = new FormData();
    formData.append('image', file.value);
    axios.post('http://localhost:8080/images', formData, {
      headers: {
        'Content-Type': 'multipart/form-data'
      }
    })
      
  }

  async function load_galery(){
    const response = await axios.get('http://localhost:8080/');
    data.value = response.data
  }
  load_galery()
  
    
</script>
