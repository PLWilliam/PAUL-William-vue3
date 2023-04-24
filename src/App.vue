<script setup>

import {ref} from 'vue'
import TheHeader from './components/TheHeader.vue';
import TheFooter from './components/TheFooter.vue';

const status = ref(true)

const clicked = (bool)=>{
   status.value = bool
}

const homeClick = (bool)=>{
   status.value = bool
   // console.log(status.value);
}

const listClick = (bool)=>{
   status.value = bool
   // console.log(status.value);
}

</script>

<template>
<body class="homepage is-preload">
		<div id="page-wrapper">

      <TheHeader :status="status" @homeClick="homeClick" @listClick="listClick"/>
      
      <router-view @onClick="clicked"/>
      
      <TheFooter/>




		</div>

	</body>
</template>

<style scoped>

</style>
