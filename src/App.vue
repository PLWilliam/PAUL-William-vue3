<script setup>

import {ref} from 'vue'
import TheHeader from './components/TheHeader.vue';
import TheFooter from './components/TheFooter.vue';

</script>

<template>
<body class="homepage is-preload">
		<div id="page-wrapper">

      <TheHeader/>
      
      <router-view/>
      
      <TheFooter/>




		</div>

	</body>
</template>

<style scoped>

</style>
